# SalaryEstimates

## Overview

### Available Operations

* [postV1EmployeesEmployeeIdSalaryEstimates](#postv1employeesemployeeidsalaryestimates) - Create a salary estimate for an employee
* [getV1SalaryEstimatesId](#getv1salaryestimatesid) - Get a salary estimate
* [putV1SalaryEstimatesId](#putv1salaryestimatesid) - Update a salary estimate
* [postV1SalaryEstimatesUuidAccept](#postv1salaryestimatesuuidaccept) - Accept a salary estimate
* [getV1SalaryEstimatesOccupations](#getv1salaryestimatesoccupations) - Search for BLS occupations

## postV1EmployeesEmployeeIdSalaryEstimates

Create a salary estimate for an employee. This endpoint helps calculate a reasonable salary for S Corp owners based on their occupation, experience level, location, and business revenue.

A salary estimate must include:
- Annual net revenue of the business
- ZIP code for location-based salary data
- One or more occupations with experience levels and time percentages (must sum to 100%)

Only one in-progress salary estimate can exist per employee at a time. If an in-progress estimate already exists, you must either accept it or use the update endpoint.

scope: `salary_estimates:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-salary_estimates" method="post" path="/v1/employees/{employee_id}/salary_estimates" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdSalaryEstimatesResponse res = sdk.salaryEstimates().postV1EmployeesEmployeeIdSalaryEstimates()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdSalaryEstimatesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .requestBody(PostV1EmployeesEmployeeIdSalaryEstimatesRequestBody.builder()
                    .zipCode("94107")
                    .occupations(List.of())
                    .annualNetRevenue(500000d)
                    .build())
                .call();

        if (res.salaryEstimate().isPresent()) {
            System.out.println(res.salaryEstimate().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1EmployeesEmployeeIdSalaryEstimatesHeaderXGustoAPIVersion>](../../models/operations/PostV1EmployeesEmployeeIdSalaryEstimatesHeaderXGustoAPIVersion.md)                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `requestBody`                                                                                                                                                                                                                | [PostV1EmployeesEmployeeIdSalaryEstimatesRequestBody](../../models/operations/PostV1EmployeesEmployeeIdSalaryEstimatesRequestBody.md)                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1EmployeesEmployeeIdSalaryEstimatesResponse](../../models/operations/PostV1EmployeesEmployeeIdSalaryEstimatesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getV1SalaryEstimatesId

Retrieve a salary estimate by its UUID. Returns the estimated salary calculation along with all occupation details, revenue, and location information.

scope: `salary_estimates:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-salary_estimates-id" method="get" path="/v1/salary_estimates/{uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1SalaryEstimatesIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1SalaryEstimatesIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1SalaryEstimatesIdResponse res = sdk.salaryEstimates().getV1SalaryEstimatesId()
                .xGustoAPIVersion(GetV1SalaryEstimatesIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .uuid("3c9d1f7e-adda-44fb-ba0e-7e5843661514")
                .call();

        if (res.salaryEstimate().isPresent()) {
            System.out.println(res.salaryEstimate().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1SalaryEstimatesIdHeaderXGustoAPIVersion>](../../models/operations/GetV1SalaryEstimatesIdHeaderXGustoAPIVersion.md)                                                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `uuid`                                                                                                                                                                                                                       | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the salary estimate                                                                                                                                                                                              |

### Response

**[GetV1SalaryEstimatesIdResponse](../../models/operations/GetV1SalaryEstimatesIdResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## putV1SalaryEstimatesId

Update an existing salary estimate. You can modify the annual net revenue, ZIP code, and occupations.

The salary estimate must not be finalized (accepted). Once accepted, salary estimates become read-only for record-keeping purposes.

scope: `salary_estimates:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-salary_estimates-id" method="put" path="/v1/salary_estimates/{uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1SalaryEstimatesIdResponse res = sdk.salaryEstimates().putV1SalaryEstimatesId()
                .xGustoAPIVersion(PutV1SalaryEstimatesIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .uuid("969f5dac-57dd-4091-b195-2546171d3a76")
                .requestBody(PutV1SalaryEstimatesIdRequestBody.builder()
                    .zipCode("94107")
                    .occupations(List.of(
                        PutV1SalaryEstimatesIdOccupations.builder()
                            .code("151252")
                            .experienceLevel(PutV1SalaryEstimatesIdExperienceLevel.EXPERT)
                            .timePercentage("0.6")
                            .primary(true)
                            .build()))
                    .annualNetRevenue(600000d)
                    .build())
                .call();

        if (res.salaryEstimate().isPresent()) {
            System.out.println(res.salaryEstimate().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1SalaryEstimatesIdHeaderXGustoAPIVersion>](../../models/operations/PutV1SalaryEstimatesIdHeaderXGustoAPIVersion.md)                                                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `uuid`                                                                                                                                                                                                                       | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the salary estimate                                                                                                                                                                                              |
| `requestBody`                                                                                                                                                                                                                | [PutV1SalaryEstimatesIdRequestBody](../../models/operations/PutV1SalaryEstimatesIdRequestBody.md)                                                                                                                            | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1SalaryEstimatesIdResponse](../../models/operations/PutV1SalaryEstimatesIdResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## postV1SalaryEstimatesUuidAccept

Accept and finalize a salary estimate. This associates the estimate with an employee job and marks it as accepted.

Once accepted, the salary estimate becomes read-only for record-keeping purposes. The accepted salary can then be used to set up compensation for the employee.

scope: `salary_estimates:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-salary_estimates-uuid-accept" method="post" path="/v1/salary_estimates/{uuid}/accept" -->
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

        PostV1SalaryEstimatesUuidAcceptResponse res = sdk.salaryEstimates().postV1SalaryEstimatesUuidAccept()
                .xGustoAPIVersion(PostV1SalaryEstimatesUuidAcceptHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .uuid("22c00075-fa4c-4bdc-91e3-f72ab8ec7a1d")
                .requestBody(PostV1SalaryEstimatesUuidAcceptRequestBody.builder()
                    .employeeJobUuid("7f5d3d93-6d6f-48c0-9f4e-cd12c2d3e4b2")
                    .build())
                .call();

        if (res.salaryEstimate().isPresent()) {
            System.out.println(res.salaryEstimate().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1SalaryEstimatesUuidAcceptHeaderXGustoAPIVersion>](../../models/operations/PostV1SalaryEstimatesUuidAcceptHeaderXGustoAPIVersion.md)                                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `uuid`                                                                                                                                                                                                                       | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the salary estimate                                                                                                                                                                                              |
| `requestBody`                                                                                                                                                                                                                | [PostV1SalaryEstimatesUuidAcceptRequestBody](../../models/operations/PostV1SalaryEstimatesUuidAcceptRequestBody.md)                                                                                                          | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1SalaryEstimatesUuidAcceptResponse](../../models/operations/PostV1SalaryEstimatesUuidAcceptResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getV1SalaryEstimatesOccupations

Search for Bureau of Labor Statistics (BLS) occupations by name or keyword. This endpoint helps users find the appropriate occupation codes to use when creating or updating salary estimates.

Returns a list of matching occupations with their codes, titles, and descriptions.

📘 System Access Authentication

This endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)

scope: `salary_estimates:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-salary_estimates-occupations" method="get" path="/v1/salary_estimates/occupations" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        GetV1SalaryEstimatesOccupationsResponse res = sdk.salaryEstimates().getV1SalaryEstimatesOccupations()
                .security(GetV1SalaryEstimatesOccupationsSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .xGustoAPIVersion(GetV1SalaryEstimatesOccupationsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .search("software")
                .call();

        if (res.blsOccupations().isPresent()) {
            System.out.println(res.blsOccupations().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  | Example                                                                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `security`                                                                                                                                                                                                                   | [com.gusto.embedded_api.models.operations.GetV1SalaryEstimatesOccupationsSecurity](../../models/operations/GetV1SalaryEstimatesOccupationsSecurity.md)                                                                       | :heavy_check_mark:                                                                                                                                                                                                           | The security requirements to use for the request.                                                                                                                                                                            |                                                                                                                                                                                                                              |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1SalaryEstimatesOccupationsHeaderXGustoAPIVersion>](../../models/operations/GetV1SalaryEstimatesOccupationsHeaderXGustoAPIVersion.md)                                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |                                                                                                                                                                                                                              |
| `search`                                                                                                                                                                                                                     | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | Search term for occupation (minimum 3 characters)                                                                                                                                                                            | software                                                                                                                                                                                                                     |

### Response

**[GetV1SalaryEstimatesOccupationsResponse](../../models/operations/GetV1SalaryEstimatesOccupationsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |