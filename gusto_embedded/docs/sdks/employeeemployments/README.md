# EmployeeEmployments

## Overview

### Available Operations

* [getTerminations](#getterminations) - Get terminations for an employee
* [createTermination](#createtermination) - Create an employee termination
* [deleteTermination](#deletetermination) - Delete an employee termination
* [updateTermination](#updatetermination) - Update an employee termination
* [getRehire](#getrehire) - Get an employee rehire
* [createRehire](#createrehire) - Create an employee rehire
* [rehire](#rehire) - Update an employee rehire
* [deleteRehire](#deleterehire) - Delete an employee rehire
* [getHistory](#gethistory) - Get employment history for an employee
* [getV1TerminationsEmployeeId](#getv1terminationsemployeeid) - Get an employee termination

## getTerminations

Terminations are created whenever an employee is scheduled to leave the company. The only things required are an effective date (their last day of work) and whether they should receive their wages in a one-off termination payroll or with the rest of the company.

Note that some states require employees to receive their final wages within 24 hours (unless they consent otherwise,) in which case running a one-off payroll may be the only option.

scope: `employments:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees-employee_id-terminations" method="get" path="/v1/employees/{employee_id}/terminations" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdTerminationsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdTerminationsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesEmployeeIdTerminationsResponse res = sdk.employeeEmployments().getTerminations()
                .xGustoAPIVersion(GetV1EmployeesEmployeeIdTerminationsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .call();

        if (res.terminations().isPresent()) {
            System.out.println(res.terminations().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1EmployeesEmployeeIdTerminationsHeaderXGustoAPIVersion>](../../models/operations/GetV1EmployeesEmployeeIdTerminationsHeaderXGustoAPIVersion.md)                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |

### Response

**[GetV1EmployeesEmployeeIdTerminationsResponse](../../models/operations/GetV1EmployeesEmployeeIdTerminationsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## createTermination

Create a termination for an employee. The only things required are an effective date (their last day of work) and whether they should receive their wages in a one-off termination payroll or with the rest of the company.

Note that some states require employees to receive their final wages within 24 hours (unless they consent otherwise,) in which case running a one-off payroll may be the only option.

scope: `employments:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-terminations" method="post" path="/v1/employees/{employee_id}/terminations" example="Basic" -->
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

        PostV1EmployeesEmployeeIdTerminationsResponse res = sdk.employeeEmployments().createTermination()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdTerminationsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .requestBody(PostV1EmployeesEmployeeIdTerminationsRequestBody.builder()
                    .effectiveDate("<value>")
                    .build())
                .call();

        if (res.termination().isPresent()) {
            System.out.println(res.termination().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-terminations" method="post" path="/v1/employees/{employee_id}/terminations" example="Example" -->
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

        PostV1EmployeesEmployeeIdTerminationsResponse res = sdk.employeeEmployments().createTermination()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdTerminationsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .requestBody(PostV1EmployeesEmployeeIdTerminationsRequestBody.builder()
                    .effectiveDate("2020-06-30")
                    .runTerminationPayroll(true)
                    .build())
                .call();

        if (res.termination().isPresent()) {
            System.out.println(res.termination().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-terminations" method="post" path="/v1/employees/{employee_id}/terminations" example="Nested" -->
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

        PostV1EmployeesEmployeeIdTerminationsResponse res = sdk.employeeEmployments().createTermination()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdTerminationsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .requestBody(PostV1EmployeesEmployeeIdTerminationsRequestBody.builder()
                    .effectiveDate("<value>")
                    .build())
                .call();

        if (res.termination().isPresent()) {
            System.out.println(res.termination().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-terminations" method="post" path="/v1/employees/{employee_id}/terminations" example="Resource" -->
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

        PostV1EmployeesEmployeeIdTerminationsResponse res = sdk.employeeEmployments().createTermination()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdTerminationsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .requestBody(PostV1EmployeesEmployeeIdTerminationsRequestBody.builder()
                    .effectiveDate("<value>")
                    .build())
                .call();

        if (res.termination().isPresent()) {
            System.out.println(res.termination().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  | Example                                                                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1EmployeesEmployeeIdTerminationsHeaderXGustoAPIVersion>](../../models/operations/PostV1EmployeesEmployeeIdTerminationsHeaderXGustoAPIVersion.md)                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |                                                                                                                                                                                                                              |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |                                                                                                                                                                                                                              |
| `requestBody`                                                                                                                                                                                                                | [PostV1EmployeesEmployeeIdTerminationsRequestBody](../../models/operations/PostV1EmployeesEmployeeIdTerminationsRequestBody.md)                                                                                              | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          | {<br/>"effective_date": "2020-06-30",<br/>"run_termination_payroll": false<br/>}                                                                                                                                             |

### Response

**[PostV1EmployeesEmployeeIdTerminationsResponse](../../models/operations/PostV1EmployeesEmployeeIdTerminationsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## deleteTermination

Delete an employee termination.

scope: `employments:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-employees-employee_id-terminations" method="delete" path="/v1/employees/{employee_id}/terminations" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.DeleteV1EmployeesEmployeeIdTerminationsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.DeleteV1EmployeesEmployeeIdTerminationsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1EmployeesEmployeeIdTerminationsResponse res = sdk.employeeEmployments().deleteTermination()
                .xGustoAPIVersion(DeleteV1EmployeesEmployeeIdTerminationsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1EmployeesEmployeeIdTerminationsHeaderXGustoAPIVersion>](../../models/operations/DeleteV1EmployeesEmployeeIdTerminationsHeaderXGustoAPIVersion.md)                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |

### Response

**[DeleteV1EmployeesEmployeeIdTerminationsResponse](../../models/operations/DeleteV1EmployeesEmployeeIdTerminationsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## updateTermination

Terminations are created whenever an employee is scheduled to leave the company. The only things required are an effective date (their last day of work) and whether they should receive their wages in a one-off termination payroll or with the rest of the company.

Note that some states require employees to receive their final wages within 24 hours (unless they consent otherwise,) in which case running a one-off payroll may be the only option.

scope: `employments:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-terminations-employee_id" method="put" path="/v1/terminations/{employee_id}" example="Basic" -->
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

        PutV1TerminationsEmployeeIdResponse res = sdk.employeeEmployments().updateTermination()
                .xGustoAPIVersion(PutV1TerminationsEmployeeIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .requestBody(PutV1TerminationsEmployeeIdRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .effectiveDate("<value>")
                    .build())
                .call();

        if (res.termination().isPresent()) {
            System.out.println(res.termination().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-terminations-employee_id" method="put" path="/v1/terminations/{employee_id}" example="Example" -->
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

        PutV1TerminationsEmployeeIdResponse res = sdk.employeeEmployments().updateTermination()
                .xGustoAPIVersion(PutV1TerminationsEmployeeIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .requestBody(PutV1TerminationsEmployeeIdRequestBody.builder()
                    .version("1928d0c378e519e9c03fb959bc959a6b")
                    .effectiveDate("2020-06-30")
                    .runTerminationPayroll(true)
                    .build())
                .call();

        if (res.termination().isPresent()) {
            System.out.println(res.termination().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-terminations-employee_id" method="put" path="/v1/terminations/{employee_id}" example="Nested" -->
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

        PutV1TerminationsEmployeeIdResponse res = sdk.employeeEmployments().updateTermination()
                .xGustoAPIVersion(PutV1TerminationsEmployeeIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .requestBody(PutV1TerminationsEmployeeIdRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .effectiveDate("<value>")
                    .build())
                .call();

        if (res.termination().isPresent()) {
            System.out.println(res.termination().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-terminations-employee_id" method="put" path="/v1/terminations/{employee_id}" example="Resource" -->
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

        PutV1TerminationsEmployeeIdResponse res = sdk.employeeEmployments().updateTermination()
                .xGustoAPIVersion(PutV1TerminationsEmployeeIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .requestBody(PutV1TerminationsEmployeeIdRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .effectiveDate("<value>")
                    .build())
                .call();

        if (res.termination().isPresent()) {
            System.out.println(res.termination().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  | Example                                                                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1TerminationsEmployeeIdHeaderXGustoAPIVersion>](../../models/operations/PutV1TerminationsEmployeeIdHeaderXGustoAPIVersion.md)                                                                                 | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |                                                                                                                                                                                                                              |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |                                                                                                                                                                                                                              |
| `requestBody`                                                                                                                                                                                                                | [PutV1TerminationsEmployeeIdRequestBody](../../models/operations/PutV1TerminationsEmployeeIdRequestBody.md)                                                                                                                  | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          | {<br/>"version": "d487dd0b55dfcacdd920ccbdaeafa351",<br/>"effective_date": "2020-06-30",<br/>"run_termination_payroll": false<br/>}                                                                                          |

### Response

**[PutV1TerminationsEmployeeIdResponse](../../models/operations/PutV1TerminationsEmployeeIdResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getRehire

Retrieve an employee's rehire, which contains information on when the employee returns to work.

scope: `employments:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees-employee_id-rehire" method="get" path="/v1/employees/{employee_id}/rehire" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdRehireResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesEmployeeIdRehireResponse res = sdk.employeeEmployments().getRehire()
                .xGustoAPIVersion(GetV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .call();

        if (res.rehire().isPresent()) {
            System.out.println(res.rehire().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion>](../../models/operations/GetV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion.md)                                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |

### Response

**[GetV1EmployeesEmployeeIdRehireResponse](../../models/operations/GetV1EmployeesEmployeeIdRehireResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## createRehire

Rehire is created whenever an employee is scheduled to return to the company.

scope: `employments:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-rehire" method="post" path="/v1/employees/{employee_id}/rehire" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.RehireBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdRehireResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdRehireResponse res = sdk.employeeEmployments().createRehire()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .rehireBody(RehireBody.builder()
                    .effectiveDate("<value>")
                    .fileNewHireReport(false)
                    .workLocationUuid("<id>")
                    .build())
                .call();

        if (res.rehire().isPresent()) {
            System.out.println(res.rehire().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-rehire" method="post" path="/v1/employees/{employee_id}/rehire" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.RehireBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdRehireResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdRehireResponse res = sdk.employeeEmployments().createRehire()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .rehireBody(RehireBody.builder()
                    .effectiveDate("2023-06-30")
                    .fileNewHireReport(true)
                    .workLocationUuid("b6ae9d93-d4b8-4119-8c96-dba595dd8c30")
                    .build())
                .call();

        if (res.rehire().isPresent()) {
            System.out.println(res.rehire().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-rehire" method="post" path="/v1/employees/{employee_id}/rehire" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.RehireBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdRehireResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdRehireResponse res = sdk.employeeEmployments().createRehire()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .rehireBody(RehireBody.builder()
                    .effectiveDate("<value>")
                    .fileNewHireReport(false)
                    .workLocationUuid("<id>")
                    .build())
                .call();

        if (res.rehire().isPresent()) {
            System.out.println(res.rehire().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-rehire" method="post" path="/v1/employees/{employee_id}/rehire" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.RehireBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdRehireResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdRehireResponse res = sdk.employeeEmployments().createRehire()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .rehireBody(RehireBody.builder()
                    .effectiveDate("<value>")
                    .fileNewHireReport(false)
                    .workLocationUuid("<id>")
                    .build())
                .call();

        if (res.rehire().isPresent()) {
            System.out.println(res.rehire().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion>](../../models/operations/PostV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion.md)                                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `rehireBody`                                                                                                                                                                                                                 | [RehireBody](../../models/components/RehireBody.md)                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1EmployeesEmployeeIdRehireResponse](../../models/operations/PostV1EmployeesEmployeeIdRehireResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## rehire

Update an employee's rehire.

scope: `employments:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-rehire" method="put" path="/v1/employees/{employee_id}/rehire" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.RehireUpdateRequestBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1EmployeesEmployeeIdRehireResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdRehireResponse res = sdk.employeeEmployments().rehire()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .rehireUpdateRequestBody(RehireUpdateRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .effectiveDate("<value>")
                    .fileNewHireReport(true)
                    .workLocationUuid("<id>")
                    .build())
                .call();

        if (res.rehire().isPresent()) {
            System.out.println(res.rehire().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-rehire" method="put" path="/v1/employees/{employee_id}/rehire" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.RehireUpdateRequestBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1EmployeesEmployeeIdRehireResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdRehireResponse res = sdk.employeeEmployments().rehire()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .rehireUpdateRequestBody(RehireUpdateRequestBody.builder()
                    .version("1928d0c378e519e9c03fb959bc959a6b")
                    .effectiveDate("2023-06-30")
                    .fileNewHireReport(true)
                    .workLocationUuid("b6ae9d93-d4b8-4119-8c96-dba595dd8c30")
                    .build())
                .call();

        if (res.rehire().isPresent()) {
            System.out.println(res.rehire().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-rehire" method="put" path="/v1/employees/{employee_id}/rehire" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.RehireUpdateRequestBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1EmployeesEmployeeIdRehireResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdRehireResponse res = sdk.employeeEmployments().rehire()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .rehireUpdateRequestBody(RehireUpdateRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .effectiveDate("<value>")
                    .fileNewHireReport(true)
                    .workLocationUuid("<id>")
                    .build())
                .call();

        if (res.rehire().isPresent()) {
            System.out.println(res.rehire().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-rehire" method="put" path="/v1/employees/{employee_id}/rehire" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.RehireUpdateRequestBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1EmployeesEmployeeIdRehireResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdRehireResponse res = sdk.employeeEmployments().rehire()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .rehireUpdateRequestBody(RehireUpdateRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .effectiveDate("<value>")
                    .fileNewHireReport(true)
                    .workLocationUuid("<id>")
                    .build())
                .call();

        if (res.rehire().isPresent()) {
            System.out.println(res.rehire().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion>](../../models/operations/PutV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion.md)                                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `rehireUpdateRequestBody`                                                                                                                                                                                                    | [RehireUpdateRequestBody](../../models/components/RehireUpdateRequestBody.md)                                                                                                                                                | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1EmployeesEmployeeIdRehireResponse](../../models/operations/PutV1EmployeesEmployeeIdRehireResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## deleteRehire

Delete an employee rehire. An employee rehire cannot be deleted if it's active (past effective date).

scope: `employments:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-employees-employee_id-rehire" method="delete" path="/v1/employees/{employee_id}/rehire" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.DeleteV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.DeleteV1EmployeesEmployeeIdRehireResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1EmployeesEmployeeIdRehireResponse res = sdk.employeeEmployments().deleteRehire()
                .xGustoAPIVersion(DeleteV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion>](../../models/operations/DeleteV1EmployeesEmployeeIdRehireHeaderXGustoAPIVersion.md)                                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |

### Response

**[DeleteV1EmployeesEmployeeIdRehireResponse](../../models/operations/DeleteV1EmployeesEmployeeIdRehireResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getHistory

Retrieve the employment history for a given employee, which includes termination and rehire.

scope: `employments:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees-employee_id-employment_history" method="get" path="/v1/employees/{employee_id}/employment_history" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdEmploymentHistoryHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdEmploymentHistoryResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesEmployeeIdEmploymentHistoryResponse res = sdk.employeeEmployments().getHistory()
                .xGustoAPIVersion(GetV1EmployeesEmployeeIdEmploymentHistoryHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .call();

        if (res.employmentHistoryList().isPresent()) {
            System.out.println(res.employmentHistoryList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1EmployeesEmployeeIdEmploymentHistoryHeaderXGustoAPIVersion>](../../models/operations/GetV1EmployeesEmployeeIdEmploymentHistoryHeaderXGustoAPIVersion.md)                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |

### Response

**[GetV1EmployeesEmployeeIdEmploymentHistoryResponse](../../models/operations/GetV1EmployeesEmployeeIdEmploymentHistoryResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## getV1TerminationsEmployeeId

Terminations are created whenever an employee is scheduled to leave the company. The only things required are an effective date (their last day of work) and whether they should receive their wages in a one-off termination payroll or with the rest of the company.

Note that some states require employees to receive their final wages within 24 hours (unless they consent otherwise,) in which case running a one-off payroll may be the only option.

scope: `employments:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-terminations-employee_id" method="get" path="/v1/terminations/{employee_id}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1TerminationsEmployeeIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1TerminationsEmployeeIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1TerminationsEmployeeIdResponse res = sdk.employeeEmployments().getV1TerminationsEmployeeId()
                .xGustoAPIVersion(GetV1TerminationsEmployeeIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .call();

        if (res.termination().isPresent()) {
            System.out.println(res.termination().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1TerminationsEmployeeIdHeaderXGustoAPIVersion>](../../models/operations/GetV1TerminationsEmployeeIdHeaderXGustoAPIVersion.md)                                                                                 | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |

### Response

**[GetV1TerminationsEmployeeIdResponse](../../models/operations/GetV1TerminationsEmployeeIdResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |