# Garnishments

## Overview

### Available Operations

* [list](#list) - Get garnishments for an employee
* [create](#create) - Create a garnishment
* [get](#get) - Get a garnishment
* [update](#update) - Update a garnishment
* [getChildSupportData](#getchildsupportdata) - Get child support garnishment data

## list

Garnishments, or employee deductions, are fixed amounts or percentages deducted from an employee’s pay. They can be deducted a specific number of times or on a recurring basis. Garnishments can also have maximum deductions on a yearly or per-pay-period bases. Common uses for garnishments are court-ordered payments for child support or back taxes. Some companies provide loans to their employees that are repaid via garnishments.

scope: `garnishments:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees-employee_id-garnishments" method="get" path="/v1/employees/{employee_id}/garnishments" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdGarnishmentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdGarnishmentsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesEmployeeIdGarnishmentsResponse res = sdk.garnishments().list()
                .xGustoAPIVersion(GetV1EmployeesEmployeeIdGarnishmentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .call();

        if (res.garnishments().isPresent()) {
            System.out.println(res.garnishments().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1EmployeesEmployeeIdGarnishmentsHeaderXGustoAPIVersion>](../../models/operations/GetV1EmployeesEmployeeIdGarnishmentsHeaderXGustoAPIVersion.md)                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `page`                                                                                                                                                                                                                       | *Optional\<Long>*                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                           | The page that is requested. When unspecified, will load all objects unless endpoint forces pagination.                                                                                                                       |
| `per`                                                                                                                                                                                                                        | *Optional\<Long>*                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                           | Number of objects per page. For majority of endpoints will default to 25                                                                                                                                                     |

### Response

**[GetV1EmployeesEmployeeIdGarnishmentsResponse](../../models/operations/GetV1EmployeesEmployeeIdGarnishmentsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## create

Garnishments, or employee deductions, are fixed amounts or percentages deducted from an employee’s pay. They can be deducted a specific number of times or on a recurring basis. Garnishments can also have maximum deductions on a yearly or per-pay-period bases. Common uses for garnishments are court-ordered payments for child support or back taxes. Some companies provide loans to their employees that are repaid via garnishments.

scope: `garnishments:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-garnishments" method="post" path="/v1/employees/{employee_id}/garnishments" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.GarnishmentRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdGarnishmentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdGarnishmentsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdGarnishmentsResponse res = sdk.garnishments().create()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdGarnishmentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .garnishmentRequest(GarnishmentRequest.builder()
                    .amount("<value>")
                    .courtOrdered(false)
                    .build())
                .call();

        if (res.garnishment().isPresent()) {
            System.out.println(res.garnishment().get());
        }
    }
}
```
### Example Usage: Child-Support-Example

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-garnishments" method="post" path="/v1/employees/{employee_id}/garnishments" example="Child-Support-Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.*;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdGarnishmentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdGarnishmentsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdGarnishmentsResponse res = sdk.garnishments().create()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdGarnishmentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .garnishmentRequest(GarnishmentRequest.builder()
                    .amount("40")
                    .courtOrdered(true)
                    .garnishmentType(GarnishmentRequestGarnishmentType.CHILD_SUPPORT)
                    .recurring(true)
                    .payPeriodMaximum("500.00")
                    .deductAsPercentage(true)
                    .childSupport(GarnishmentChildSupport.builder()
                        .state("FL")
                        .paymentPeriod(PaymentPeriod.MONTHLY)
                        .fipsCode("12011")
                        .caseNumber("CS1234")
                        .build())
                    .build())
                .call();

        if (res.garnishment().isPresent()) {
            System.out.println(res.garnishment().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-garnishments" method="post" path="/v1/employees/{employee_id}/garnishments" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.GarnishmentRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdGarnishmentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdGarnishmentsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdGarnishmentsResponse res = sdk.garnishments().create()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdGarnishmentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .garnishmentRequest(GarnishmentRequest.builder()
                    .amount("150.00")
                    .courtOrdered(true)
                    .description("Back taxes")
                    .recurring(true)
                    .build())
                .call();

        if (res.garnishment().isPresent()) {
            System.out.println(res.garnishment().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-garnishments" method="post" path="/v1/employees/{employee_id}/garnishments" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.GarnishmentRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdGarnishmentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdGarnishmentsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdGarnishmentsResponse res = sdk.garnishments().create()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdGarnishmentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .garnishmentRequest(GarnishmentRequest.builder()
                    .amount("<value>")
                    .courtOrdered(false)
                    .build())
                .call();

        if (res.garnishment().isPresent()) {
            System.out.println(res.garnishment().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-garnishments" method="post" path="/v1/employees/{employee_id}/garnishments" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.GarnishmentRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdGarnishmentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdGarnishmentsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdGarnishmentsResponse res = sdk.garnishments().create()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdGarnishmentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .garnishmentRequest(GarnishmentRequest.builder()
                    .amount("<value>")
                    .courtOrdered(false)
                    .build())
                .call();

        if (res.garnishment().isPresent()) {
            System.out.println(res.garnishment().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1EmployeesEmployeeIdGarnishmentsHeaderXGustoAPIVersion>](../../models/operations/PostV1EmployeesEmployeeIdGarnishmentsHeaderXGustoAPIVersion.md)                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `garnishmentRequest`                                                                                                                                                                                                         | [GarnishmentRequest](../../models/components/GarnishmentRequest.md)                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1EmployeesEmployeeIdGarnishmentsResponse](../../models/operations/PostV1EmployeesEmployeeIdGarnishmentsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## get

Garnishments, or employee deductions, are fixed amounts or percentages deducted from an employee’s pay. They can be deducted a specific number of times or on a recurring basis. Garnishments can also have maximum deductions on a yearly or per-pay-period bases. Common uses for garnishments are court-ordered payments for child support or back taxes. Some companies provide loans to their employees that are repaid via garnishments.

scope: `garnishments:read`

### Example Usage: Child-Support-Example

<!-- UsageSnippet language="java" operationID="get-v1-garnishments-garnishment_id" method="get" path="/v1/garnishments/{garnishment_id}" example="Child-Support-Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1GarnishmentsGarnishmentIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1GarnishmentsGarnishmentIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1GarnishmentsGarnishmentIdResponse res = sdk.garnishments().get()
                .xGustoAPIVersion(GetV1GarnishmentsGarnishmentIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .garnishmentId("<id>")
                .call();

        if (res.garnishment().isPresent()) {
            System.out.println(res.garnishment().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="get-v1-garnishments-garnishment_id" method="get" path="/v1/garnishments/{garnishment_id}" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1GarnishmentsGarnishmentIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1GarnishmentsGarnishmentIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1GarnishmentsGarnishmentIdResponse res = sdk.garnishments().get()
                .xGustoAPIVersion(GetV1GarnishmentsGarnishmentIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .garnishmentId("<id>")
                .call();

        if (res.garnishment().isPresent()) {
            System.out.println(res.garnishment().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1GarnishmentsGarnishmentIdHeaderXGustoAPIVersion>](../../models/operations/GetV1GarnishmentsGarnishmentIdHeaderXGustoAPIVersion.md)                                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `garnishmentId`                                                                                                                                                                                                              | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the garnishment                                                                                                                                                                                                  |

### Response

**[GetV1GarnishmentsGarnishmentIdResponse](../../models/operations/GetV1GarnishmentsGarnishmentIdResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## update

Garnishments, or employee deductions, are fixed amounts or percentages deducted from an employee’s pay. They can be deducted a specific number of times or on a recurring basis. Garnishments can also have maximum deductions on a yearly or per-pay-period bases. Common uses for garnishments are court-ordered payments for child support or back taxes. Some companies provide loans to their employees that are repaid via garnishments.

scope: `garnishments:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-garnishments-garnishment_id" method="put" path="/v1/garnishments/{garnishment_id}" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.UpdateGarnishmentRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1GarnishmentsGarnishmentIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1GarnishmentsGarnishmentIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1GarnishmentsGarnishmentIdResponse res = sdk.garnishments().update()
                .xGustoAPIVersion(PutV1GarnishmentsGarnishmentIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .garnishmentId("<id>")
                .updateGarnishmentRequest(UpdateGarnishmentRequest.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.garnishment().isPresent()) {
            System.out.println(res.garnishment().get());
        }
    }
}
```
### Example Usage: Child-Support-Example

<!-- UsageSnippet language="java" operationID="put-v1-garnishments-garnishment_id" method="put" path="/v1/garnishments/{garnishment_id}" example="Child-Support-Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.UpdateGarnishmentRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1GarnishmentsGarnishmentIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1GarnishmentsGarnishmentIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1GarnishmentsGarnishmentIdResponse res = sdk.garnishments().update()
                .xGustoAPIVersion(PutV1GarnishmentsGarnishmentIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .garnishmentId("<id>")
                .updateGarnishmentRequest(UpdateGarnishmentRequest.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.garnishment().isPresent()) {
            System.out.println(res.garnishment().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-garnishments-garnishment_id" method="put" path="/v1/garnishments/{garnishment_id}" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.UpdateGarnishmentRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1GarnishmentsGarnishmentIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1GarnishmentsGarnishmentIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1GarnishmentsGarnishmentIdResponse res = sdk.garnishments().update()
                .xGustoAPIVersion(PutV1GarnishmentsGarnishmentIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .garnishmentId("<id>")
                .updateGarnishmentRequest(UpdateGarnishmentRequest.builder()
                    .version("52b7c567242cb7452e89ba2bc02cb476")
                    .active(false)
                    .build())
                .call();

        if (res.garnishment().isPresent()) {
            System.out.println(res.garnishment().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-garnishments-garnishment_id" method="put" path="/v1/garnishments/{garnishment_id}" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.UpdateGarnishmentRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1GarnishmentsGarnishmentIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1GarnishmentsGarnishmentIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1GarnishmentsGarnishmentIdResponse res = sdk.garnishments().update()
                .xGustoAPIVersion(PutV1GarnishmentsGarnishmentIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .garnishmentId("<id>")
                .updateGarnishmentRequest(UpdateGarnishmentRequest.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.garnishment().isPresent()) {
            System.out.println(res.garnishment().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-garnishments-garnishment_id" method="put" path="/v1/garnishments/{garnishment_id}" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.UpdateGarnishmentRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1GarnishmentsGarnishmentIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1GarnishmentsGarnishmentIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1GarnishmentsGarnishmentIdResponse res = sdk.garnishments().update()
                .xGustoAPIVersion(PutV1GarnishmentsGarnishmentIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .garnishmentId("<id>")
                .updateGarnishmentRequest(UpdateGarnishmentRequest.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.garnishment().isPresent()) {
            System.out.println(res.garnishment().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1GarnishmentsGarnishmentIdHeaderXGustoAPIVersion>](../../models/operations/PutV1GarnishmentsGarnishmentIdHeaderXGustoAPIVersion.md)                                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `garnishmentId`                                                                                                                                                                                                              | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the garnishment                                                                                                                                                                                                  |
| `updateGarnishmentRequest`                                                                                                                                                                                                   | [UpdateGarnishmentRequest](../../models/components/UpdateGarnishmentRequest.md)                                                                                                                                              | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1GarnishmentsGarnishmentIdResponse](../../models/operations/PutV1GarnishmentsGarnishmentIdResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getChildSupportData

Agency data and requirements to be used for creating child support garnishments

scope: `garnishments:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-garnishments-child_support" method="get" path="/v1/garnishments/child_support" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.operations.GetV1GarnishmentsChildSupportHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1GarnishmentsChildSupportResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1GarnishmentsChildSupportResponse res = sdk.garnishments().getChildSupportData()
                .xGustoAPIVersion(GetV1GarnishmentsChildSupportHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.childSupportData().isPresent()) {
            System.out.println(res.childSupportData().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1GarnishmentsChildSupportHeaderXGustoAPIVersion>](../../models/operations/GetV1GarnishmentsChildSupportHeaderXGustoAPIVersion.md)                                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1GarnishmentsChildSupportResponse](../../models/operations/GetV1GarnishmentsChildSupportResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |