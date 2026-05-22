# JobsAndCompensations

## Overview

### Available Operations

* [getJobs](#getjobs) - Get jobs for an employee
* [createJob](#createjob) - Create a job
* [getJob](#getjob) - Get a job
* [update](#update) - Update a job
* [delete](#delete) - Delete an individual job
* [getCompensations](#getcompensations) - Get compensations for a job
* [createCompensation](#createcompensation) - Create a compensation
* [getCompensation](#getcompensation) - Get a compensation
* [updateCompensation](#updatecompensation) - Update a compensation
* [deleteCompensation](#deletecompensation) - Delete a compensation

## getJobs

Get all of the jobs that an employee holds.
Note: Compensation data (pay rate, payment unit, and related fields) represents sensitive employee pay information. When retrieving employee job data, these fields (`rate`, `payment_unit`, `current_compensation_uuid`, `compensations`) are only returned when the `compensations:read` scope is included. This allows you to access employee and job metadata without exposing pay rates.

Compensation data in the response requires the `compensations:read` scope.

scope: `jobs:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees-employee_id-jobs" method="get" path="/v1/employees/{employee_id}/jobs" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdJobsRequest;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdJobsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesEmployeeIdJobsRequest req = GetV1EmployeesEmployeeIdJobsRequest.builder()
                .employeeId("<id>")
                .build();

        GetV1EmployeesEmployeeIdJobsResponse res = sdk.jobsAndCompensations().getJobs()
                .request(req)
                .call();

        if (res.jobs().isPresent()) {
            System.out.println(res.jobs().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                             | Type                                                                                                  | Required                                                                                              | Description                                                                                           |
| ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| `request`                                                                                             | [GetV1EmployeesEmployeeIdJobsRequest](../../models/operations/GetV1EmployeesEmployeeIdJobsRequest.md) | :heavy_check_mark:                                                                                    | The request object to use for the request.                                                            |

### Response

**[GetV1EmployeesEmployeeIdJobsResponse](../../models/operations/GetV1EmployeesEmployeeIdJobsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## createJob

Create a job.

scope: `jobs:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-jobs" method="post" path="/v1/employees/{employee_id}/jobs" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.JobsCreateRequestBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdJobsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdJobsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdJobsResponse res = sdk.jobsAndCompensations().createJob()
                .employeeId("<id>")
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdJobsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .jobsCreateRequestBody(JobsCreateRequestBody.builder()
                    .title("Regional Manager")
                    .hireDate("2020-12-21")
                    .build())
                .call();

        if (res.job().isPresent()) {
            System.out.println(res.job().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1EmployeesEmployeeIdJobsHeaderXGustoAPIVersion>](../../models/operations/PostV1EmployeesEmployeeIdJobsHeaderXGustoAPIVersion.md)                                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `jobsCreateRequestBody`                                                                                                                                                                                                      | [JobsCreateRequestBody](../../models/components/JobsCreateRequestBody.md)                                                                                                                                                    | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1EmployeesEmployeeIdJobsResponse](../../models/operations/PostV1EmployeesEmployeeIdJobsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getJob

Get a job.

Note: Compensation data (pay rate, payment unit, and related fields) represents sensitive employee pay information. When retrieving employee job data, these fields (`rate`, `payment_unit`, `current_compensation_uuid`, `compensations`) are only returned when the `compensations:read` scope is included. This allows you to access employee and job metadata without exposing pay rates.

Compensation data in the response requires the `compensations:read` scope.

scope: `jobs:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-jobs-job_id" method="get" path="/v1/jobs/{job_id}" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1JobsJobIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1JobsJobIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1JobsJobIdResponse res = sdk.jobsAndCompensations().getJob()
                .jobId("<id>")
                .xGustoAPIVersion(GetV1JobsJobIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.job().isPresent()) {
            System.out.println(res.job().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `jobId`                                                                                                                                                                                                                      | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the job                                                                                                                                                                                                          |
| `include`                                                                                                                                                                                                                    | [Optional\<GetV1JobsJobIdQueryParamInclude>](../../models/operations/GetV1JobsJobIdQueryParamInclude.md)                                                                                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Available options:<br/>- all_compensations: Include all effective dated compensations for each job instead of only the current compensation<br/>                                                                             |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1JobsJobIdHeaderXGustoAPIVersion>](../../models/operations/GetV1JobsJobIdHeaderXGustoAPIVersion.md)                                                                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1JobsJobIdResponse](../../models/operations/GetV1JobsJobIdResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## update

Update a job.

scope: `jobs:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-jobs-job_id" method="put" path="/v1/jobs/{job_id}" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.JobsUpdateRequestBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1JobsJobIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1JobsJobIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1JobsJobIdResponse res = sdk.jobsAndCompensations().update()
                .jobId("<id>")
                .xGustoAPIVersion(PutV1JobsJobIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .jobsUpdateRequestBody(JobsUpdateRequestBody.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.job().isPresent()) {
            System.out.println(res.job().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-jobs-job_id" method="put" path="/v1/jobs/{job_id}" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.JobsUpdateRequestBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1JobsJobIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1JobsJobIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1JobsJobIdResponse res = sdk.jobsAndCompensations().update()
                .jobId("<id>")
                .xGustoAPIVersion(PutV1JobsJobIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .jobsUpdateRequestBody(JobsUpdateRequestBody.builder()
                    .version("gr78930htutrz444kuytr3s5hgxykuveb523fwl8sir")
                    .title("Regional Manager")
                    .hireDate("2020-12-21")
                    .build())
                .call();

        if (res.job().isPresent()) {
            System.out.println(res.job().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-jobs-job_id" method="put" path="/v1/jobs/{job_id}" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.JobsUpdateRequestBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1JobsJobIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1JobsJobIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1JobsJobIdResponse res = sdk.jobsAndCompensations().update()
                .jobId("<id>")
                .xGustoAPIVersion(PutV1JobsJobIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .jobsUpdateRequestBody(JobsUpdateRequestBody.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.job().isPresent()) {
            System.out.println(res.job().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-jobs-job_id" method="put" path="/v1/jobs/{job_id}" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.JobsUpdateRequestBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1JobsJobIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1JobsJobIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1JobsJobIdResponse res = sdk.jobsAndCompensations().update()
                .jobId("<id>")
                .xGustoAPIVersion(PutV1JobsJobIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .jobsUpdateRequestBody(JobsUpdateRequestBody.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.job().isPresent()) {
            System.out.println(res.job().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `jobId`                                                                                                                                                                                                                      | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the job                                                                                                                                                                                                          |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1JobsJobIdHeaderXGustoAPIVersion>](../../models/operations/PutV1JobsJobIdHeaderXGustoAPIVersion.md)                                                                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `jobsUpdateRequestBody`                                                                                                                                                                                                      | [JobsUpdateRequestBody](../../models/components/JobsUpdateRequestBody.md)                                                                                                                                                    | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1JobsJobIdResponse](../../models/operations/PutV1JobsJobIdResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## delete

Deletes a specific job that an employee holds.

scope: `jobs:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-jobs-job_id" method="delete" path="/v1/jobs/{job_id}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.DeleteV1JobsJobIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.DeleteV1JobsJobIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1JobsJobIdResponse res = sdk.jobsAndCompensations().delete()
                .jobId("<id>")
                .xGustoAPIVersion(DeleteV1JobsJobIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `jobId`                                                                                                                                                                                                                      | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the job                                                                                                                                                                                                          |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1JobsJobIdHeaderXGustoAPIVersion>](../../models/operations/DeleteV1JobsJobIdHeaderXGustoAPIVersion.md)                                                                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[DeleteV1JobsJobIdResponse](../../models/operations/DeleteV1JobsJobIdResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getCompensations

Compensations contain information on how much is paid out for a job. Jobs may have many compensations, but only one that is active. The current compensation is the one with the most recent `effective_date`.

*Note: Currently the API does not support creating multiple compensations per job - creating a compensation with the same job_uuid as another will fail with a relevant error.*

Use `flsa_status` to determine if an employee is eligible for overtime
By default the API returns only the current compensation - use the `include` parameter to return all compensations.

scope: `compensations:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-jobs-job_id-compensations" method="get" path="/v1/jobs/{job_id}/compensations" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1JobsJobIdCompensationsRequest;
import com.gusto.embedded_api.models.operations.GetV1JobsJobIdCompensationsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1JobsJobIdCompensationsRequest req = GetV1JobsJobIdCompensationsRequest.builder()
                .jobId("<id>")
                .build();

        GetV1JobsJobIdCompensationsResponse res = sdk.jobsAndCompensations().getCompensations()
                .request(req)
                .call();

        if (res.compensations().isPresent()) {
            System.out.println(res.compensations().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                           | Type                                                                                                | Required                                                                                            | Description                                                                                         |
| --------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| `request`                                                                                           | [GetV1JobsJobIdCompensationsRequest](../../models/operations/GetV1JobsJobIdCompensationsRequest.md) | :heavy_check_mark:                                                                                  | The request object to use for the request.                                                          |

### Response

**[GetV1JobsJobIdCompensationsResponse](../../models/operations/GetV1JobsJobIdCompensationsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## createCompensation

Compensations contain information on how much is paid out for a job. Jobs may have many compensations, but only one that is active. The current compensation is the one with the most recent `effective_date`.

### Prerequisites
Before calling this endpoint:
1. A [job](ref:post-v1-jobs-job_id) must exist for the employee

### Webhooks
- `employee_job_compensation.created`: Fires when a compensation is successfully created

scope: `compensations:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="post-v1-compensations-compensation_id" method="post" path="/v1/jobs/{job_id}/compensations" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.*;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompensationsCompensationIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompensationsCompensationIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompensationsCompensationIdResponse res = sdk.jobsAndCompensations().createCompensation()
                .xGustoAPIVersion(PostV1CompensationsCompensationIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .jobId("<id>")
                .compensationsRequestBody(CompensationsRequestBody.builder()
                    .rate("70000.00")
                    .paymentUnit(CompensationsRequestBodyPaymentUnit.WEEK)
                    .flsaStatus(FlsaStatusType.SALARIED_NONEXEMPT)
                    .build())
                .call();

        if (res.compensation().isPresent()) {
            System.out.println(res.compensation().get());
        }
    }
}
```
### Example Usage: Exempt

<!-- UsageSnippet language="java" operationID="post-v1-compensations-compensation_id" method="post" path="/v1/jobs/{job_id}/compensations" example="Exempt" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.*;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompensationsCompensationIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompensationsCompensationIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompensationsCompensationIdResponse res = sdk.jobsAndCompensations().createCompensation()
                .xGustoAPIVersion(PostV1CompensationsCompensationIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .jobId("<id>")
                .compensationsRequestBody(CompensationsRequestBody.builder()
                    .rate("60000.00")
                    .paymentUnit(CompensationsRequestBodyPaymentUnit.YEAR)
                    .flsaStatus(FlsaStatusType.EXEMPT)
                    .build())
                .call();

        if (res.compensation().isPresent()) {
            System.out.println(res.compensation().get());
        }
    }
}
```
### Example Usage: Minimum Wage Adjusted

<!-- UsageSnippet language="java" operationID="post-v1-compensations-compensation_id" method="post" path="/v1/jobs/{job_id}/compensations" example="Minimum Wage Adjusted" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.*;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompensationsCompensationIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompensationsCompensationIdResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompensationsCompensationIdResponse res = sdk.jobsAndCompensations().createCompensation()
                .xGustoAPIVersion(PostV1CompensationsCompensationIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .jobId("<id>")
                .compensationsRequestBody(CompensationsRequestBody.builder()
                    .rate("7.00")
                    .paymentUnit(CompensationsRequestBodyPaymentUnit.HOUR)
                    .flsaStatus(FlsaStatusType.NONEXEMPT)
                    .effectiveDate("2023-01-01")
                    .adjustForMinimumWage(true)
                    .minimumWages(List.of(
                        CompensationsRequestBodyMinimumWages.builder()
                            .uuid("340832db-ab28-4112-9e10-28dd1711835f")
                            .build()))
                    .build())
                .call();

        if (res.compensation().isPresent()) {
            System.out.println(res.compensation().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="post-v1-compensations-compensation_id" method="post" path="/v1/jobs/{job_id}/compensations" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.*;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompensationsCompensationIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompensationsCompensationIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompensationsCompensationIdResponse res = sdk.jobsAndCompensations().createCompensation()
                .xGustoAPIVersion(PostV1CompensationsCompensationIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .jobId("<id>")
                .compensationsRequestBody(CompensationsRequestBody.builder()
                    .rate("70000.00")
                    .paymentUnit(CompensationsRequestBodyPaymentUnit.WEEK)
                    .flsaStatus(FlsaStatusType.SALARIED_NONEXEMPT)
                    .build())
                .call();

        if (res.compensation().isPresent()) {
            System.out.println(res.compensation().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="post-v1-compensations-compensation_id" method="post" path="/v1/jobs/{job_id}/compensations" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.*;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompensationsCompensationIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompensationsCompensationIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompensationsCompensationIdResponse res = sdk.jobsAndCompensations().createCompensation()
                .xGustoAPIVersion(PostV1CompensationsCompensationIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .jobId("<id>")
                .compensationsRequestBody(CompensationsRequestBody.builder()
                    .rate("70000.00")
                    .paymentUnit(CompensationsRequestBodyPaymentUnit.WEEK)
                    .flsaStatus(FlsaStatusType.SALARIED_NONEXEMPT)
                    .build())
                .call();

        if (res.compensation().isPresent()) {
            System.out.println(res.compensation().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompensationsCompensationIdHeaderXGustoAPIVersion>](../../models/operations/PostV1CompensationsCompensationIdHeaderXGustoAPIVersion.md)                                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `jobId`                                                                                                                                                                                                                      | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the job                                                                                                                                                                                                          |
| `compensationsRequestBody`                                                                                                                                                                                                   | [CompensationsRequestBody](../../models/components/CompensationsRequestBody.md)                                                                                                                                              | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompensationsCompensationIdResponse](../../models/operations/PostV1CompensationsCompensationIdResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getCompensation

Compensations contain information on how much is paid out for a job. Jobs may have many compensations, but only one that is active. The current compensation is the one with the most recent `effective_date`.

scope: `compensations:read`

### Example Usage: Exempt

<!-- UsageSnippet language="java" operationID="get-v1-compensations-compensation_id" method="get" path="/v1/compensations/{compensation_id}" example="Exempt" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1CompensationsCompensationIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1CompensationsCompensationIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompensationsCompensationIdResponse res = sdk.jobsAndCompensations().getCompensation()
                .xGustoAPIVersion(GetV1CompensationsCompensationIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .compensationId("<id>")
                .call();

        if (res.compensation().isPresent()) {
            System.out.println(res.compensation().get());
        }
    }
}
```
### Example Usage: Minimum Wage Adjusted

<!-- UsageSnippet language="java" operationID="get-v1-compensations-compensation_id" method="get" path="/v1/compensations/{compensation_id}" example="Minimum Wage Adjusted" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1CompensationsCompensationIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1CompensationsCompensationIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompensationsCompensationIdResponse res = sdk.jobsAndCompensations().getCompensation()
                .xGustoAPIVersion(GetV1CompensationsCompensationIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .compensationId("<id>")
                .call();

        if (res.compensation().isPresent()) {
            System.out.println(res.compensation().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompensationsCompensationIdHeaderXGustoAPIVersion>](../../models/operations/GetV1CompensationsCompensationIdHeaderXGustoAPIVersion.md)                                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `compensationId`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the compensation                                                                                                                                                                                                 |

### Response

**[GetV1CompensationsCompensationIdResponse](../../models/operations/GetV1CompensationsCompensationIdResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## updateCompensation

Compensations contain information on how much is paid out for a job. Jobs may have many compensations, but only one that is active. The current compensation is the one with the most recent `effective_date`.

### Webhooks
- `employee_job_compensation.updated`: Fires when a compensation is successfully updated

scope: `compensations:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-compensations-compensation_id" method="put" path="/v1/compensations/{compensation_id}" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompensationsUpdateRequestBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompensationsCompensationIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompensationsCompensationIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompensationsCompensationIdResponse res = sdk.jobsAndCompensations().updateCompensation()
                .xGustoAPIVersion(PutV1CompensationsCompensationIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .compensationId("<id>")
                .compensationsUpdateRequestBody(CompensationsUpdateRequestBody.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.compensation().isPresent()) {
            System.out.println(res.compensation().get());
        }
    }
}
```
### Example Usage: Exempt

<!-- UsageSnippet language="java" operationID="put-v1-compensations-compensation_id" method="put" path="/v1/compensations/{compensation_id}" example="Exempt" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.*;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompensationsCompensationIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompensationsCompensationIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompensationsCompensationIdResponse res = sdk.jobsAndCompensations().updateCompensation()
                .xGustoAPIVersion(PutV1CompensationsCompensationIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .compensationId("<id>")
                .compensationsUpdateRequestBody(CompensationsUpdateRequestBody.builder()
                    .version("98jr3289h3298hr9329gf9egskt3kagri32qqgiqe3872")
                    .rate("60000.00")
                    .paymentUnit(CompensationsUpdateRequestBodyPaymentUnit.YEAR)
                    .flsaStatus(FlsaStatusType.EXEMPT)
                    .build())
                .call();

        if (res.compensation().isPresent()) {
            System.out.println(res.compensation().get());
        }
    }
}
```
### Example Usage: Minimum Wage Adjusted

<!-- UsageSnippet language="java" operationID="put-v1-compensations-compensation_id" method="put" path="/v1/compensations/{compensation_id}" example="Minimum Wage Adjusted" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.*;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompensationsCompensationIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompensationsCompensationIdResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompensationsCompensationIdResponse res = sdk.jobsAndCompensations().updateCompensation()
                .xGustoAPIVersion(PutV1CompensationsCompensationIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .compensationId("<id>")
                .compensationsUpdateRequestBody(CompensationsUpdateRequestBody.builder()
                    .version("98jr3289h3298hr9329gf9egskt3kagri32qqgiqe3872")
                    .rate("7.00")
                    .paymentUnit(CompensationsUpdateRequestBodyPaymentUnit.HOUR)
                    .flsaStatus(FlsaStatusType.NONEXEMPT)
                    .adjustForMinimumWage(true)
                    .minimumWages(List.of(
                        CompensationsUpdateRequestBodyMinimumWages.builder()
                            .uuid("340832db-ab28-4112-9e10-28dd1711835f")
                            .build()))
                    .build())
                .call();

        if (res.compensation().isPresent()) {
            System.out.println(res.compensation().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-compensations-compensation_id" method="put" path="/v1/compensations/{compensation_id}" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompensationsUpdateRequestBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompensationsCompensationIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompensationsCompensationIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompensationsCompensationIdResponse res = sdk.jobsAndCompensations().updateCompensation()
                .xGustoAPIVersion(PutV1CompensationsCompensationIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .compensationId("<id>")
                .compensationsUpdateRequestBody(CompensationsUpdateRequestBody.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.compensation().isPresent()) {
            System.out.println(res.compensation().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-compensations-compensation_id" method="put" path="/v1/compensations/{compensation_id}" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompensationsUpdateRequestBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompensationsCompensationIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompensationsCompensationIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompensationsCompensationIdResponse res = sdk.jobsAndCompensations().updateCompensation()
                .xGustoAPIVersion(PutV1CompensationsCompensationIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .compensationId("<id>")
                .compensationsUpdateRequestBody(CompensationsUpdateRequestBody.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.compensation().isPresent()) {
            System.out.println(res.compensation().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1CompensationsCompensationIdHeaderXGustoAPIVersion>](../../models/operations/PutV1CompensationsCompensationIdHeaderXGustoAPIVersion.md)                                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `compensationId`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the compensation                                                                                                                                                                                                 |
| `compensationsUpdateRequestBody`                                                                                                                                                                                             | [CompensationsUpdateRequestBody](../../models/components/CompensationsUpdateRequestBody.md)                                                                                                                                  | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1CompensationsCompensationIdResponse](../../models/operations/PutV1CompensationsCompensationIdResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## deleteCompensation

Compensations contain information on how much is paid out for a job. Jobs may have many compensations, but only one that is active. The current compensation is the one with the most recent `effective_date`. This endpoint deletes a compensation for a job that hasn't been processed on payroll.

### Webhooks
- `employee_job_compensation.destroyed`: Fires when a compensation is successfully deleted

scope: `compensations:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-compensations-compensation_id" method="delete" path="/v1/compensations/{compensation_id}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.DeleteV1CompensationsCompensationIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.DeleteV1CompensationsCompensationIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1CompensationsCompensationIdResponse res = sdk.jobsAndCompensations().deleteCompensation()
                .xGustoAPIVersion(DeleteV1CompensationsCompensationIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .compensationId("<id>")
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1CompensationsCompensationIdHeaderXGustoAPIVersion>](../../models/operations/DeleteV1CompensationsCompensationIdHeaderXGustoAPIVersion.md)                                                                 | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `compensationId`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the compensation                                                                                                                                                                                                 |

### Response

**[DeleteV1CompensationsCompensationIdResponse](../../models/operations/DeleteV1CompensationsCompensationIdResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |