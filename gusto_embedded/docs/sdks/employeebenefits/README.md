# EmployeeBenefits

## Overview

### Available Operations

* [get](#get) - Get all benefits for an employee
* [create](#create) - Create an employee benefit
* [retrieve](#retrieve) - Get an employee benefit
* [update](#update) - Update an employee benefit
* [delete](#delete) - Delete an employee benefit
* [getYtdBenefitAmountsFromDifferentCompany](#getytdbenefitamountsfromdifferentcompany) - Get year-to-date benefit amounts from a different company
* [createYtdBenefitAmountsFromDifferentCompany](#createytdbenefitamountsfromdifferentcompany) - Create year-to-date benefit amounts from a different company
* [getV1EmployeesEmployeeUuidSection603HighEarnerStatuses](#getv1employeesemployeeuuidsection603highearnerstatuses) - Get all Section 603 high earner statuses for an employee
* [postV1EmployeesEmployeeUuidSection603HighEarnerStatuses](#postv1employeesemployeeuuidsection603highearnerstatuses) - Create a Section 603 high earner status
* [getV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYear](#getv1employeesemployeeuuidsection603highearnerstatuseseffectiveyear) - Get a Section 603 high earner status for a specific year
* [patchV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYear](#patchv1employeesemployeeuuidsection603highearnerstatuseseffectiveyear) - Update a Section 603 high earner status

## get

Employee benefits represent an employee enrolled in a particular company benefit. It includes information specific to that employee’s enrollment.

Returns an array of all employee benefits for this employee

Benefits containing PHI are only visible to applications with the `employee_benefits:read:phi` scope.

scope: `employee_benefits:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees-employee_id-employee_benefits" method="get" path="/v1/employees/{employee_id}/employee_benefits" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdEmployeeBenefitsRequest;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdEmployeeBenefitsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesEmployeeIdEmployeeBenefitsRequest req = GetV1EmployeesEmployeeIdEmployeeBenefitsRequest.builder()
                .employeeId("<id>")
                .build();

        GetV1EmployeesEmployeeIdEmployeeBenefitsResponse res = sdk.employeeBenefits().get()
                .request(req)
                .call();

        if (res.employeeBenefits().isPresent()) {
            System.out.println(res.employeeBenefits().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                     | Type                                                                                                                          | Required                                                                                                                      | Description                                                                                                                   |
| ----------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `request`                                                                                                                     | [GetV1EmployeesEmployeeIdEmployeeBenefitsRequest](../../models/operations/GetV1EmployeesEmployeeIdEmployeeBenefitsRequest.md) | :heavy_check_mark:                                                                                                            | The request object to use for the request.                                                                                    |

### Response

**[GetV1EmployeesEmployeeIdEmployeeBenefitsResponse](../../models/operations/GetV1EmployeesEmployeeIdEmployeeBenefitsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## create

Employee benefits represent an employee enrolled in a particular company benefit. It includes information specific to that employee's enrollment.

When the application has the `employee_benefits:write:benefit_type_limited` data scope, the application can only create employee benefits for benefit types that are permitted for the application.

scope: `employee_benefits:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-employee_benefits" method="post" path="/v1/employees/{employee_id}/employee_benefits" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBenefitCreateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdEmployeeBenefitsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdEmployeeBenefitsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdEmployeeBenefitsResponse res = sdk.employeeBenefits().create()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdEmployeeBenefitsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .employeeBenefitCreateRequest(EmployeeBenefitCreateRequest.builder()
                    .companyBenefitUuid("<id>")
                    .build())
                .call();

        if (res.employeeBenefit().isPresent()) {
            System.out.println(res.employeeBenefit().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-employee_benefits" method="post" path="/v1/employees/{employee_id}/employee_benefits" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.*;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdEmployeeBenefitsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdEmployeeBenefitsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdEmployeeBenefitsResponse res = sdk.employeeBenefits().create()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdEmployeeBenefitsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .employeeBenefitCreateRequest(EmployeeBenefitCreateRequest.builder()
                    .companyBenefitUuid("f68abb42-431e-4392-bc3f-2795627e00f3")
                    .employeeDeduction("100.00")
                    .contribution(EmployeeBenefitCreateRequestContribution.builder()
                        .type(EmployeeBenefitCreateRequestType.AMOUNT)
                        .value(EmployeeBenefitCreateRequestValue.of("100.00"))
                        .build())
                    .build())
                .call();

        if (res.employeeBenefit().isPresent()) {
            System.out.println(res.employeeBenefit().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-employee_benefits" method="post" path="/v1/employees/{employee_id}/employee_benefits" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBenefitCreateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdEmployeeBenefitsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdEmployeeBenefitsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdEmployeeBenefitsResponse res = sdk.employeeBenefits().create()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdEmployeeBenefitsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .employeeBenefitCreateRequest(EmployeeBenefitCreateRequest.builder()
                    .companyBenefitUuid("<id>")
                    .build())
                .call();

        if (res.employeeBenefit().isPresent()) {
            System.out.println(res.employeeBenefit().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-employee_benefits" method="post" path="/v1/employees/{employee_id}/employee_benefits" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBenefitCreateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdEmployeeBenefitsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdEmployeeBenefitsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdEmployeeBenefitsResponse res = sdk.employeeBenefits().create()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdEmployeeBenefitsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .employeeBenefitCreateRequest(EmployeeBenefitCreateRequest.builder()
                    .companyBenefitUuid("<id>")
                    .build())
                .call();

        if (res.employeeBenefit().isPresent()) {
            System.out.println(res.employeeBenefit().get());
        }
    }
}
```
### Example Usage: Tiered example

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-employee_benefits" method="post" path="/v1/employees/{employee_id}/employee_benefits" example="Tiered example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBenefitCreateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdEmployeeBenefitsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdEmployeeBenefitsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdEmployeeBenefitsResponse res = sdk.employeeBenefits().create()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdEmployeeBenefitsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .employeeBenefitCreateRequest(EmployeeBenefitCreateRequest.builder()
                    .companyBenefitUuid("<id>")
                    .build())
                .call();

        if (res.employeeBenefit().isPresent()) {
            System.out.println(res.employeeBenefit().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1EmployeesEmployeeIdEmployeeBenefitsHeaderXGustoAPIVersion>](../../models/operations/PostV1EmployeesEmployeeIdEmployeeBenefitsHeaderXGustoAPIVersion.md)                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `employeeBenefitCreateRequest`                                                                                                                                                                                               | [EmployeeBenefitCreateRequest](../../models/components/EmployeeBenefitCreateRequest.md)                                                                                                                                      | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1EmployeesEmployeeIdEmployeeBenefitsResponse](../../models/operations/PostV1EmployeesEmployeeIdEmployeeBenefitsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## retrieve

Employee benefits represent an employee enrolled in a particular company benefit. It includes information specific to that employee’s enrollment.

Benefits containing PHI are only visible to applications with the `employee_benefits:read:phi` scope.

scope: `employee_benefits:read`

### Example Usage: Example

<!-- UsageSnippet language="java" operationID="get-v1-employee_benefits-employee_benefit_id" method="get" path="/v1/employee_benefits/{employee_benefit_id}" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1EmployeeBenefitsEmployeeBenefitIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeeBenefitsEmployeeBenefitIdResponse res = sdk.employeeBenefits().retrieve()
                .xGustoAPIVersion(GetV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeBenefitId("<id>")
                .call();

        if (res.employeeBenefit().isPresent()) {
            System.out.println(res.employeeBenefit().get());
        }
    }
}
```
### Example Usage: Tiered example

<!-- UsageSnippet language="java" operationID="get-v1-employee_benefits-employee_benefit_id" method="get" path="/v1/employee_benefits/{employee_benefit_id}" example="Tiered example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1EmployeeBenefitsEmployeeBenefitIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeeBenefitsEmployeeBenefitIdResponse res = sdk.employeeBenefits().retrieve()
                .xGustoAPIVersion(GetV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeBenefitId("<id>")
                .call();

        if (res.employeeBenefit().isPresent()) {
            System.out.println(res.employeeBenefit().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion>](../../models/operations/GetV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion.md)                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeBenefitId`                                                                                                                                                                                                          | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee benefit.                                                                                                                                                                                            |

### Response

**[GetV1EmployeeBenefitsEmployeeBenefitIdResponse](../../models/operations/GetV1EmployeeBenefitsEmployeeBenefitIdResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## update

Employee benefits represent an employee enrolled in a particular company benefit. It includes information specific to that employee's enrollment.

When the application has the `employee_benefits:write:benefit_type_limited` data scope, the application can only update employee benefits for benefit types that are permitted for the application.

scope: `employee_benefits:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-employee_benefits-employee_benefit_id" method="put" path="/v1/employee_benefits/{employee_benefit_id}" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBenefitUpdateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1EmployeeBenefitsEmployeeBenefitIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeeBenefitsEmployeeBenefitIdResponse res = sdk.employeeBenefits().update()
                .xGustoAPIVersion(PutV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeBenefitId("<id>")
                .employeeBenefitUpdateRequest(EmployeeBenefitUpdateRequest.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.employeeBenefit().isPresent()) {
            System.out.println(res.employeeBenefit().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-employee_benefits-employee_benefit_id" method="put" path="/v1/employee_benefits/{employee_benefit_id}" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBenefitUpdateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1EmployeeBenefitsEmployeeBenefitIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeeBenefitsEmployeeBenefitIdResponse res = sdk.employeeBenefits().update()
                .xGustoAPIVersion(PutV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeBenefitId("<id>")
                .employeeBenefitUpdateRequest(EmployeeBenefitUpdateRequest.builder()
                    .version("09j3d29jqdpj92109j9j2d90dq")
                    .employeeDeduction("250.00")
                    .build())
                .call();

        if (res.employeeBenefit().isPresent()) {
            System.out.println(res.employeeBenefit().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-employee_benefits-employee_benefit_id" method="put" path="/v1/employee_benefits/{employee_benefit_id}" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBenefitUpdateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1EmployeeBenefitsEmployeeBenefitIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeeBenefitsEmployeeBenefitIdResponse res = sdk.employeeBenefits().update()
                .xGustoAPIVersion(PutV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeBenefitId("<id>")
                .employeeBenefitUpdateRequest(EmployeeBenefitUpdateRequest.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.employeeBenefit().isPresent()) {
            System.out.println(res.employeeBenefit().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-employee_benefits-employee_benefit_id" method="put" path="/v1/employee_benefits/{employee_benefit_id}" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBenefitUpdateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1EmployeeBenefitsEmployeeBenefitIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeeBenefitsEmployeeBenefitIdResponse res = sdk.employeeBenefits().update()
                .xGustoAPIVersion(PutV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeBenefitId("<id>")
                .employeeBenefitUpdateRequest(EmployeeBenefitUpdateRequest.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.employeeBenefit().isPresent()) {
            System.out.println(res.employeeBenefit().get());
        }
    }
}
```
### Example Usage: Tiered example

<!-- UsageSnippet language="java" operationID="put-v1-employee_benefits-employee_benefit_id" method="put" path="/v1/employee_benefits/{employee_benefit_id}" example="Tiered example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBenefitUpdateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1EmployeeBenefitsEmployeeBenefitIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeeBenefitsEmployeeBenefitIdResponse res = sdk.employeeBenefits().update()
                .xGustoAPIVersion(PutV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeBenefitId("<id>")
                .employeeBenefitUpdateRequest(EmployeeBenefitUpdateRequest.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.employeeBenefit().isPresent()) {
            System.out.println(res.employeeBenefit().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion>](../../models/operations/PutV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion.md)                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeBenefitId`                                                                                                                                                                                                          | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee benefit.                                                                                                                                                                                            |
| `employeeBenefitUpdateRequest`                                                                                                                                                                                               | [EmployeeBenefitUpdateRequest](../../models/components/EmployeeBenefitUpdateRequest.md)                                                                                                                                      | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1EmployeeBenefitsEmployeeBenefitIdResponse](../../models/operations/PutV1EmployeeBenefitsEmployeeBenefitIdResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## delete

Employee benefits represent an employee enrolled in a particular company benefit. It includes information specific to that employee's enrollment.

When the application has the `employee_benefits:write:benefit_type_limited` data scope, the application can only delete employee benefits for benefit types that are permitted for the application.

scope: `employee_benefits:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-employee_benefits-employee_benefit_id" method="delete" path="/v1/employee_benefits/{employee_benefit_id}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.operations.DeleteV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.DeleteV1EmployeeBenefitsEmployeeBenefitIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1EmployeeBenefitsEmployeeBenefitIdResponse res = sdk.employeeBenefits().delete()
                .xGustoAPIVersion(DeleteV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeBenefitId("<id>")
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion>](../../models/operations/DeleteV1EmployeeBenefitsEmployeeBenefitIdHeaderXGustoAPIVersion.md)                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeBenefitId`                                                                                                                                                                                                          | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee benefit.                                                                                                                                                                                            |

### Response

**[DeleteV1EmployeeBenefitsEmployeeBenefitIdResponse](../../models/operations/DeleteV1EmployeeBenefitsEmployeeBenefitIdResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |

## getYtdBenefitAmountsFromDifferentCompany

Retrieves year-to-date benefit amounts that were contributed at a different company for the specified employee.
Returns benefit amounts for the requested tax year (defaults to current year if not specified).

This endpoint only supports retrieving outside contributions for 401(k) benefits.

scope: `employee_benefits:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-employee-ytd-benefit-amounts-from-different-company" method="get" path="/v1/employees/{employee_id}/ytd_benefit_amounts_from_different_company" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetEmployeeYtdBenefitAmountsFromDifferentCompanyHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetEmployeeYtdBenefitAmountsFromDifferentCompanyResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetEmployeeYtdBenefitAmountsFromDifferentCompanyResponse res = sdk.employeeBenefits().getYtdBenefitAmountsFromDifferentCompany()
                .xGustoAPIVersion(GetEmployeeYtdBenefitAmountsFromDifferentCompanyHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .taxYear(2024L)
                .call();

        if (res.ytdBenefitAmountsFromDifferentCompanies().isPresent()) {
            System.out.println(res.ytdBenefitAmountsFromDifferentCompanies().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  | Example                                                                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetEmployeeYtdBenefitAmountsFromDifferentCompanyHeaderXGustoAPIVersion>](../../models/operations/GetEmployeeYtdBenefitAmountsFromDifferentCompanyHeaderXGustoAPIVersion.md)                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |                                                                                                                                                                                                                              |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |                                                                                                                                                                                                                              |
| `taxYear`                                                                                                                                                                                                                    | *Optional\<Long>*                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                           | The tax year for which to retrieve YTD benefit amounts. Defaults to current year if not specified.                                                                                                                           | 2024                                                                                                                                                                                                                         |

### Response

**[GetEmployeeYtdBenefitAmountsFromDifferentCompanyResponse](../../models/operations/GetEmployeeYtdBenefitAmountsFromDifferentCompanyResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## createYtdBenefitAmountsFromDifferentCompany

Year-to-date benefit amounts from a different company represents the amount of money added to an employee's plan during a current year, made outside of the current contribution when they were employed at a different company.

This endpoint only supports passing outside contributions for 401(k) benefits.

scope: `employee_benefits:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="post-employee-ytd-benefit-amounts-from-different-company" method="post" path="/v1/employees/{employee_id}/ytd_benefit_amounts_from_different_company" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.YtdBenefitAmountsFromDifferentCompanyBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostEmployeeYtdBenefitAmountsFromDifferentCompanyHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostEmployeeYtdBenefitAmountsFromDifferentCompanyResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostEmployeeYtdBenefitAmountsFromDifferentCompanyResponse res = sdk.employeeBenefits().createYtdBenefitAmountsFromDifferentCompany()
                .xGustoAPIVersion(PostEmployeeYtdBenefitAmountsFromDifferentCompanyHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .ytdBenefitAmountsFromDifferentCompanyBody(YtdBenefitAmountsFromDifferentCompanyBody.builder()
                    .benefitType(182856L)
                    .taxYear(1828.56)
                    .build())
                .call();

        // handle response
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="post-employee-ytd-benefit-amounts-from-different-company" method="post" path="/v1/employees/{employee_id}/ytd_benefit_amounts_from_different_company" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.YtdBenefitAmountsFromDifferentCompanyBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostEmployeeYtdBenefitAmountsFromDifferentCompanyHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostEmployeeYtdBenefitAmountsFromDifferentCompanyResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostEmployeeYtdBenefitAmountsFromDifferentCompanyResponse res = sdk.employeeBenefits().createYtdBenefitAmountsFromDifferentCompany()
                .xGustoAPIVersion(PostEmployeeYtdBenefitAmountsFromDifferentCompanyHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .ytdBenefitAmountsFromDifferentCompanyBody(YtdBenefitAmountsFromDifferentCompanyBody.builder()
                    .benefitType(600673L)
                    .taxYear(1828.56)
                    .build())
                .call();

        // handle response
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="post-employee-ytd-benefit-amounts-from-different-company" method="post" path="/v1/employees/{employee_id}/ytd_benefit_amounts_from_different_company" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.YtdBenefitAmountsFromDifferentCompanyBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostEmployeeYtdBenefitAmountsFromDifferentCompanyHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostEmployeeYtdBenefitAmountsFromDifferentCompanyResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostEmployeeYtdBenefitAmountsFromDifferentCompanyResponse res = sdk.employeeBenefits().createYtdBenefitAmountsFromDifferentCompany()
                .xGustoAPIVersion(PostEmployeeYtdBenefitAmountsFromDifferentCompanyHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .ytdBenefitAmountsFromDifferentCompanyBody(YtdBenefitAmountsFromDifferentCompanyBody.builder()
                    .benefitType(270638L)
                    .taxYear(1828.56)
                    .build())
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostEmployeeYtdBenefitAmountsFromDifferentCompanyHeaderXGustoAPIVersion>](../../models/operations/PostEmployeeYtdBenefitAmountsFromDifferentCompanyHeaderXGustoAPIVersion.md)                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `ytdBenefitAmountsFromDifferentCompanyBody`                                                                                                                                                                                  | [YtdBenefitAmountsFromDifferentCompanyBody](../../models/components/YtdBenefitAmountsFromDifferentCompanyBody.md)                                                                                                            | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostEmployeeYtdBenefitAmountsFromDifferentCompanyResponse](../../models/operations/PostEmployeeYtdBenefitAmountsFromDifferentCompanyResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getV1EmployeesEmployeeUuidSection603HighEarnerStatuses

Get all Section 603 high earner statuses for an employee across all years.

Section 603 of the SECURE 2.0 Act applies to employees aged 50 or older whose prior-year FICA wages exceed the IRS threshold.
These employees are classified as high earners, and their catch-up contributions to pre-tax retirement benefits must be designated as post-tax contributions.

scope: `employee_benefits:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees-employee_uuid-section603_high_earner_statuses" method="get" path="/v1/employees/{employee_uuid}/section603_high_earner_statuses" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeUuidSection603HighEarnerStatusesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeUuidSection603HighEarnerStatusesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesEmployeeUuidSection603HighEarnerStatusesResponse res = sdk.employeeBenefits().getV1EmployeesEmployeeUuidSection603HighEarnerStatuses()
                .employeeUuid("<id>")
                .xGustoAPIVersion(GetV1EmployeesEmployeeUuidSection603HighEarnerStatusesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.employeeSection603HighEarnerStatusList().isPresent()) {
            System.out.println(res.employeeSection603HighEarnerStatusList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `employeeUuid`                                                                                                                                                                                                               | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1EmployeesEmployeeUuidSection603HighEarnerStatusesHeaderXGustoAPIVersion>](../../models/operations/GetV1EmployeesEmployeeUuidSection603HighEarnerStatusesHeaderXGustoAPIVersion.md)                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1EmployeesEmployeeUuidSection603HighEarnerStatusesResponse](../../models/operations/GetV1EmployeesEmployeeUuidSection603HighEarnerStatusesResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## postV1EmployeesEmployeeUuidSection603HighEarnerStatuses

Create a Section 603 high earner status for an employee for a specific year.

Section 603 of the SECURE 2.0 Act applies to employees aged 50 or older whose prior-year FICA wages exceed the IRS threshold.
These employees are classified as high earners, and their catch-up contributions to pre-tax retirement benefits must be designated as post-tax contributions.

scope: `employee_benefits:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_uuid-section603_high_earner_statuses" method="post" path="/v1/employees/{employee_uuid}/section603_high_earner_statuses" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeSection603HighEarnerStatusCreateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeUuidSection603HighEarnerStatusesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeUuidSection603HighEarnerStatusesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeUuidSection603HighEarnerStatusesResponse res = sdk.employeeBenefits().postV1EmployeesEmployeeUuidSection603HighEarnerStatuses()
                .employeeUuid("<id>")
                .xGustoAPIVersion(PostV1EmployeesEmployeeUuidSection603HighEarnerStatusesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeSection603HighEarnerStatusCreateRequest(EmployeeSection603HighEarnerStatusCreateRequest.builder()
                    .effectiveYear(2026L)
                    .isHighEarner(true)
                    .build())
                .call();

        if (res.employeeSection603HighEarnerStatus().isPresent()) {
            System.out.println(res.employeeSection603HighEarnerStatus().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `employeeUuid`                                                                                                                                                                                                               | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1EmployeesEmployeeUuidSection603HighEarnerStatusesHeaderXGustoAPIVersion>](../../models/operations/PostV1EmployeesEmployeeUuidSection603HighEarnerStatusesHeaderXGustoAPIVersion.md)                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeSection603HighEarnerStatusCreateRequest`                                                                                                                                                                            | [EmployeeSection603HighEarnerStatusCreateRequest](../../models/components/EmployeeSection603HighEarnerStatusCreateRequest.md)                                                                                                | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1EmployeesEmployeeUuidSection603HighEarnerStatusesResponse](../../models/operations/PostV1EmployeesEmployeeUuidSection603HighEarnerStatusesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 409, 422                               | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYear

Get a Section 603 high earner status for an employee for a specific year.

Section 603 of the SECURE 2.0 Act applies to employees aged 50 or older whose prior-year FICA wages exceed the IRS threshold.
These employees are classified as high earners, and their catch-up contributions to pre-tax retirement benefits must be designated as post-tax contributions.

scope: `employee_benefits:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees-employee_uuid-section603_high_earner_statuses-effective_year" method="get" path="/v1/employees/{employee_uuid}/section603_high_earner_statuses/{effective_year}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYearHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYearResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYearResponse res = sdk.employeeBenefits().getV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYear()
                .employeeUuid("<id>")
                .effectiveYear(857230L)
                .xGustoAPIVersion(GetV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYearHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.employeeSection603HighEarnerStatus().isPresent()) {
            System.out.println(res.employeeSection603HighEarnerStatus().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `employeeUuid`                                                                                                                                                                                                               | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `effectiveYear`                                                                                                                                                                                                              | *long*                                                                                                                                                                                                                       | :heavy_check_mark:                                                                                                                                                                                                           | The effective year for the Section 603 status                                                                                                                                                                                |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYearHeaderXGustoAPIVersion>](../../models/operations/GetV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYearHeaderXGustoAPIVersion.md) | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYearResponse](../../models/operations/GetV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYearResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## patchV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYear

Update a Section 603 high earner status for an employee for a specific year.

Section 603 of the SECURE 2.0 Act applies to employees aged 50 or older whose prior-year FICA wages exceed the IRS threshold.
These employees are classified as high earners, and their catch-up contributions to pre-tax retirement benefits must be designated as post-tax contributions.

scope: `employee_benefits:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="patch-v1-employees-employee_uuid-section603_high_earner_statuses-effective_year" method="patch" path="/v1/employees/{employee_uuid}/section603_high_earner_statuses/{effective_year}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeSection603HighEarnerStatusUpdateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PatchV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYearHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PatchV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYearResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PatchV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYearResponse res = sdk.employeeBenefits().patchV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYear()
                .employeeUuid("<id>")
                .effectiveYear(152322L)
                .xGustoAPIVersion(PatchV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYearHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeSection603HighEarnerStatusUpdateRequest(EmployeeSection603HighEarnerStatusUpdateRequest.builder()
                    .isHighEarner(true)
                    .build())
                .call();

        if (res.employeeSection603HighEarnerStatus().isPresent()) {
            System.out.println(res.employeeSection603HighEarnerStatus().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                        | Type                                                                                                                                                                                                                             | Required                                                                                                                                                                                                                         | Description                                                                                                                                                                                                                      |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `employeeUuid`                                                                                                                                                                                                                   | *String*                                                                                                                                                                                                                         | :heavy_check_mark:                                                                                                                                                                                                               | The UUID of the employee                                                                                                                                                                                                         |
| `effectiveYear`                                                                                                                                                                                                                  | *long*                                                                                                                                                                                                                           | :heavy_check_mark:                                                                                                                                                                                                               | The effective year for the Section 603 status                                                                                                                                                                                    |
| `xGustoAPIVersion`                                                                                                                                                                                                               | [Optional\<PatchV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYearHeaderXGustoAPIVersion>](../../models/operations/PatchV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYearHeaderXGustoAPIVersion.md) | :heavy_minus_sign:                                                                                                                                                                                                               | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used.     |
| `employeeSection603HighEarnerStatusUpdateRequest`                                                                                                                                                                                | [EmployeeSection603HighEarnerStatusUpdateRequest](../../models/components/EmployeeSection603HighEarnerStatusUpdateRequest.md)                                                                                                    | :heavy_check_mark:                                                                                                                                                                                                               | N/A                                                                                                                                                                                                                              |

### Response

**[PatchV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYearResponse](../../models/operations/PatchV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYearResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |