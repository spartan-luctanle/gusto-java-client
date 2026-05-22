# EmployeeAddresses

## Overview

### Available Operations

* [get](#get) - Get an employee's home addresses
* [create](#create) - Create an employee's home address
* [retrieveHomeAddress](#retrievehomeaddress) - Get an employee's home address
* [update](#update) - Update an employee's home address
* [delete](#delete) - Delete an employee's home address
* [getWorkAddresses](#getworkaddresses) - Get an employee's work addresses
* [createWorkAddress](#createworkaddress) - Create an employee work address
* [retrieveWorkAddress](#retrieveworkaddress) - Get an employee work address
* [updateWorkAddress](#updateworkaddress) - Update an employee work address
* [deleteWorkAddress](#deleteworkaddress) - Delete an employee's work address

## get

The home address of an employee is used to determine certain tax information about them. Addresses are geocoded on create and update to ensure validity.

Supports home address effective dating and courtesy withholding.

scope: `employees:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees-employee_id-home_addresses" method="get" path="/v1/employees/{employee_id}/home_addresses" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdHomeAddressesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdHomeAddressesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesEmployeeIdHomeAddressesResponse res = sdk.employeeAddresses().get()
                .employeeId("<id>")
                .xGustoAPIVersion(GetV1EmployeesEmployeeIdHomeAddressesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.employeeAddressList().isPresent()) {
            System.out.println(res.employeeAddressList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1EmployeesEmployeeIdHomeAddressesHeaderXGustoAPIVersion>](../../models/operations/GetV1EmployeesEmployeeIdHomeAddressesHeaderXGustoAPIVersion.md)                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1EmployeesEmployeeIdHomeAddressesResponse](../../models/operations/GetV1EmployeesEmployeeIdHomeAddressesResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## create

The home address of an employee is used to determine certain tax information about them. Addresses are geocoded on create and update to ensure validity.

Supports home address effective dating and courtesy withholding.

scope: `employees:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-home_addresses" method="post" path="/v1/employees/{employee_id}/home_addresses" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdHomeAddressesResponse res = sdk.employeeAddresses().create()
                .employeeId("<id>")
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdHomeAddressesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PostV1EmployeesEmployeeIdHomeAddressesRequestBody.builder()
                    .street1("300 3rd Street")
                    .city("San Francisco")
                    .state("CA")
                    .zip("94107")
                    .effectiveDate(LocalDate.parse("2022-01-31"))
                    .build())
                .call();

        if (res.employeeAddress().isPresent()) {
            System.out.println(res.employeeAddress().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1EmployeesEmployeeIdHomeAddressesHeaderXGustoAPIVersion>](../../models/operations/PostV1EmployeesEmployeeIdHomeAddressesHeaderXGustoAPIVersion.md)                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `requestBody`                                                                                                                                                                                                                | [PostV1EmployeesEmployeeIdHomeAddressesRequestBody](../../models/operations/PostV1EmployeesEmployeeIdHomeAddressesRequestBody.md)                                                                                            | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1EmployeesEmployeeIdHomeAddressesResponse](../../models/operations/PostV1EmployeesEmployeeIdHomeAddressesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## retrieveHomeAddress

The home address of an employee is used to determine certain tax information about them. Addresses are geocoded on create and update to ensure validity.

Supports home address effective dating and courtesy withholding.

scope: `employees:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-home_addresses-home_address_uuid" method="get" path="/v1/home_addresses/{home_address_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1HomeAddressesHomeAddressUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1HomeAddressesHomeAddressUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1HomeAddressesHomeAddressUuidResponse res = sdk.employeeAddresses().retrieveHomeAddress()
                .homeAddressUuid("<id>")
                .xGustoAPIVersion(GetV1HomeAddressesHomeAddressUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.employeeAddress().isPresent()) {
            System.out.println(res.employeeAddress().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `homeAddressUuid`                                                                                                                                                                                                            | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the home address                                                                                                                                                                                                 |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1HomeAddressesHomeAddressUuidHeaderXGustoAPIVersion>](../../models/operations/GetV1HomeAddressesHomeAddressUuidHeaderXGustoAPIVersion.md)                                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1HomeAddressesHomeAddressUuidResponse](../../models/operations/GetV1HomeAddressesHomeAddressUuidResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## update

The home address of an employee is used to determine certain tax information about them. Addresses are geocoded on create and update to ensure validity.

Supports home address effective dating and courtesy withholding.

scope: `employees:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-home_addresses-home_address_uuid" method="put" path="/v1/home_addresses/{home_address_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1HomeAddressesHomeAddressUuidResponse res = sdk.employeeAddresses().update()
                .xGustoAPIVersion(PutV1HomeAddressesHomeAddressUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .homeAddressUuid("<id>")
                .requestBody(PutV1HomeAddressesHomeAddressUuidRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .build())
                .call();

        if (res.employeeAddress().isPresent()) {
            System.out.println(res.employeeAddress().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1HomeAddressesHomeAddressUuidHeaderXGustoAPIVersion>](../../models/operations/PutV1HomeAddressesHomeAddressUuidHeaderXGustoAPIVersion.md)                                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `homeAddressUuid`                                                                                                                                                                                                            | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the home address                                                                                                                                                                                                 |
| `requestBody`                                                                                                                                                                                                                | [PutV1HomeAddressesHomeAddressUuidRequestBody](../../models/operations/PutV1HomeAddressesHomeAddressUuidRequestBody.md)                                                                                                      | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1HomeAddressesHomeAddressUuidResponse](../../models/operations/PutV1HomeAddressesHomeAddressUuidResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## delete

Used for deleting an employee's home address. Cannot delete the employee's active home address.

scope: `employees:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-home_addresses-home_address_uuid" method="delete" path="/v1/home_addresses/{home_address_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.DeleteV1HomeAddressesHomeAddressUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.DeleteV1HomeAddressesHomeAddressUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1HomeAddressesHomeAddressUuidResponse res = sdk.employeeAddresses().delete()
                .xGustoAPIVersion(DeleteV1HomeAddressesHomeAddressUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .homeAddressUuid("<id>")
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1HomeAddressesHomeAddressUuidHeaderXGustoAPIVersion>](../../models/operations/DeleteV1HomeAddressesHomeAddressUuidHeaderXGustoAPIVersion.md)                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `homeAddressUuid`                                                                                                                                                                                                            | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the home address                                                                                                                                                                                                 |

### Response

**[DeleteV1HomeAddressesHomeAddressUuidResponse](../../models/operations/DeleteV1HomeAddressesHomeAddressUuidResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getWorkAddresses

Returns a list of an employee's work addresses. Each address includes its effective
date and a boolean signifying if it is the currently active work address.

scope: `employees:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees-employee_id-work_addresses" method="get" path="/v1/employees/{employee_id}/work_addresses" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdWorkAddressesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdWorkAddressesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesEmployeeIdWorkAddressesResponse res = sdk.employeeAddresses().getWorkAddresses()
                .employeeId("<id>")
                .xGustoAPIVersion(GetV1EmployeesEmployeeIdWorkAddressesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.employeeWorkAddressesList().isPresent()) {
            System.out.println(res.employeeWorkAddressesList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1EmployeesEmployeeIdWorkAddressesHeaderXGustoAPIVersion>](../../models/operations/GetV1EmployeesEmployeeIdWorkAddressesHeaderXGustoAPIVersion.md)                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1EmployeesEmployeeIdWorkAddressesResponse](../../models/operations/GetV1EmployeesEmployeeIdWorkAddressesResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## createWorkAddress

The work address of an employee describes when an employee began working at an associated company location.

scope: `employees:manage`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-work_addresses" method="post" path="/v1/employees/{employee_id}/work_addresses" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdWorkAddressesResponse res = sdk.employeeAddresses().createWorkAddress()
                .employeeId("<id>")
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdWorkAddressesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PostV1EmployeesEmployeeIdWorkAddressesRequestBody.builder()
                    .locationUuid("6a119be7-b4b0-4e27-aaa0-89d5f2524635")
                    .effectiveDate(LocalDate.parse("2023-05-15"))
                    .build())
                .call();

        if (res.employeeWorkAddress().isPresent()) {
            System.out.println(res.employeeWorkAddress().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1EmployeesEmployeeIdWorkAddressesHeaderXGustoAPIVersion>](../../models/operations/PostV1EmployeesEmployeeIdWorkAddressesHeaderXGustoAPIVersion.md)                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `requestBody`                                                                                                                                                                                                                | [PostV1EmployeesEmployeeIdWorkAddressesRequestBody](../../models/operations/PostV1EmployeesEmployeeIdWorkAddressesRequestBody.md)                                                                                            | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1EmployeesEmployeeIdWorkAddressesResponse](../../models/operations/PostV1EmployeesEmployeeIdWorkAddressesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## retrieveWorkAddress

The work address of an employee is used for payroll tax purposes.

scope: `employees:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-work_addresses-work_address_uuid" method="get" path="/v1/work_addresses/{work_address_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1WorkAddressesWorkAddressUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1WorkAddressesWorkAddressUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1WorkAddressesWorkAddressUuidResponse res = sdk.employeeAddresses().retrieveWorkAddress()
                .workAddressUuid("<id>")
                .xGustoAPIVersion(GetV1WorkAddressesWorkAddressUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.employeeWorkAddress().isPresent()) {
            System.out.println(res.employeeWorkAddress().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `workAddressUuid`                                                                                                                                                                                                            | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the work address                                                                                                                                                                                                 |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1WorkAddressesWorkAddressUuidHeaderXGustoAPIVersion>](../../models/operations/GetV1WorkAddressesWorkAddressUuidHeaderXGustoAPIVersion.md)                                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1WorkAddressesWorkAddressUuidResponse](../../models/operations/GetV1WorkAddressesWorkAddressUuidResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## updateWorkAddress

The work address of an employee is used for payroll tax purposes.

scope: `employees:manage`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-work_addresses-work_address_uuid" method="put" path="/v1/work_addresses/{work_address_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1WorkAddressesWorkAddressUuidResponse res = sdk.employeeAddresses().updateWorkAddress()
                .workAddressUuid("<id>")
                .xGustoAPIVersion(PutV1WorkAddressesWorkAddressUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PutV1WorkAddressesWorkAddressUuidRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .locationUuid("6a119be7-b4b0-4e27-aaa0-89d5f2524635")
                    .effectiveDate(LocalDate.parse("2023-05-15"))
                    .build())
                .call();

        if (res.employeeWorkAddress().isPresent()) {
            System.out.println(res.employeeWorkAddress().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `workAddressUuid`                                                                                                                                                                                                            | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the work address                                                                                                                                                                                                 |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1WorkAddressesWorkAddressUuidHeaderXGustoAPIVersion>](../../models/operations/PutV1WorkAddressesWorkAddressUuidHeaderXGustoAPIVersion.md)                                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `requestBody`                                                                                                                                                                                                                | [PutV1WorkAddressesWorkAddressUuidRequestBody](../../models/operations/PutV1WorkAddressesWorkAddressUuidRequestBody.md)                                                                                                      | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1WorkAddressesWorkAddressUuidResponse](../../models/operations/PutV1WorkAddressesWorkAddressUuidResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## deleteWorkAddress

Used for deleting an employee's work address. Cannot delete the employee's active work address.

scope: `employees:manage`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-work_addresses-work_address_uuid" method="delete" path="/v1/work_addresses/{work_address_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.DeleteV1WorkAddressesWorkAddressUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.DeleteV1WorkAddressesWorkAddressUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1WorkAddressesWorkAddressUuidResponse res = sdk.employeeAddresses().deleteWorkAddress()
                .workAddressUuid("<id>")
                .xGustoAPIVersion(DeleteV1WorkAddressesWorkAddressUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `workAddressUuid`                                                                                                                                                                                                            | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the work address                                                                                                                                                                                                 |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1WorkAddressesWorkAddressUuidHeaderXGustoAPIVersion>](../../models/operations/DeleteV1WorkAddressesWorkAddressUuidHeaderXGustoAPIVersion.md)                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[DeleteV1WorkAddressesWorkAddressUuidResponse](../../models/operations/DeleteV1WorkAddressesWorkAddressUuidResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |