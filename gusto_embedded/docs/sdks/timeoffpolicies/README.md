# TimeOffPolicies

## Overview

### Available Operations

* [calculateAccruingTimeOffHours](#calculateaccruingtimeoffhours) - Calculate accruing time off hours
* [get](#get) - Get a time off policy
* [update](#update) - Update a time off policy
* [getAll](#getall) - Get all time off policies for a company
* [create](#create) - Create a time off policy
* [addEmployees](#addemployees) - Add employees to a time off policy
* [removeEmployees](#removeemployees) - Remove employees from a time off policy
* [updateBalance](#updatebalance) - Update employee time off balances
* [deactivate](#deactivate) - Deactivate a time off policy

## calculateAccruingTimeOffHours

Returns a list of accruing time off for each time off policy associated with the employee.

Factors affecting the accrued hours:

- the time off policy accrual method (whether they get pay per hour worked, per hour paid, with / without overtime, accumulate time off based on pay period / calendar year / anniversary)
- how many hours of work during this pay period
- how many hours of PTO / sick hours taken during this pay period (for per hour paid policies only)
- company pay schedule frequency (for per pay period)

If none of the parameters is passed in, the accrued time off hour will be 0.

scope: `payrolls:read`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="post-v1-payrolls-payroll_id-calculate_accruing_time_off_hours" method="post" path="/v1/payrolls/{payroll_id}/employees/{employee_id}/calculate_accruing_time_off_hours" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.PayrollCalculateAccruingTimeOffHoursRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursResponse res = sdk.timeOffPolicies().calculateAccruingTimeOffHours()
                .xGustoAPIVersion(PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .payrollId("<id>")
                .employeeId("<id>")
                .payrollCalculateAccruingTimeOffHoursRequest(PayrollCalculateAccruingTimeOffHoursRequest.builder()
                    .build())
                .call();

        if (res.payrollCalculateAccruingTimeOffHoursResponse().isPresent()) {
            System.out.println(res.payrollCalculateAccruingTimeOffHoursResponse().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="post-v1-payrolls-payroll_id-calculate_accruing_time_off_hours" method="post" path="/v1/payrolls/{payroll_id}/employees/{employee_id}/calculate_accruing_time_off_hours" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.PayrollCalculateAccruingTimeOffHoursRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursResponse res = sdk.timeOffPolicies().calculateAccruingTimeOffHours()
                .xGustoAPIVersion(PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .payrollId("<id>")
                .employeeId("<id>")
                .payrollCalculateAccruingTimeOffHoursRequest(PayrollCalculateAccruingTimeOffHoursRequest.builder()
                    .regularHoursWorked("30.25")
                    .overtimeHoursWorked("10")
                    .doubleOvertimeHoursWorked("0")
                    .ptoHoursUsed("5.5")
                    .sickHoursUsed("0")
                    .build())
                .call();

        if (res.payrollCalculateAccruingTimeOffHoursResponse().isPresent()) {
            System.out.println(res.payrollCalculateAccruingTimeOffHoursResponse().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="post-v1-payrolls-payroll_id-calculate_accruing_time_off_hours" method="post" path="/v1/payrolls/{payroll_id}/employees/{employee_id}/calculate_accruing_time_off_hours" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.PayrollCalculateAccruingTimeOffHoursRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursResponse res = sdk.timeOffPolicies().calculateAccruingTimeOffHours()
                .xGustoAPIVersion(PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .payrollId("<id>")
                .employeeId("<id>")
                .payrollCalculateAccruingTimeOffHoursRequest(PayrollCalculateAccruingTimeOffHoursRequest.builder()
                    .build())
                .call();

        if (res.payrollCalculateAccruingTimeOffHoursResponse().isPresent()) {
            System.out.println(res.payrollCalculateAccruingTimeOffHoursResponse().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="post-v1-payrolls-payroll_id-calculate_accruing_time_off_hours" method="post" path="/v1/payrolls/{payroll_id}/employees/{employee_id}/calculate_accruing_time_off_hours" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.PayrollCalculateAccruingTimeOffHoursRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursResponse res = sdk.timeOffPolicies().calculateAccruingTimeOffHours()
                .xGustoAPIVersion(PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .payrollId("<id>")
                .employeeId("<id>")
                .payrollCalculateAccruingTimeOffHoursRequest(PayrollCalculateAccruingTimeOffHoursRequest.builder()
                    .build())
                .call();

        if (res.payrollCalculateAccruingTimeOffHoursResponse().isPresent()) {
            System.out.println(res.payrollCalculateAccruingTimeOffHoursResponse().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursHeaderXGustoAPIVersion>](../../models/operations/PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursHeaderXGustoAPIVersion.md)                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `payrollId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the payroll                                                                                                                                                                                                      |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `payrollCalculateAccruingTimeOffHoursRequest`                                                                                                                                                                                | [Optional\<PayrollCalculateAccruingTimeOffHoursRequest>](../../models/components/PayrollCalculateAccruingTimeOffHoursRequest.md)                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursResponse](../../models/operations/PostV1PayrollsPayrollIdCalculateAccruingTimeOffHoursResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## get

Get a time off policy

scope: `time_off_policies:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-time_off_policies-time_off_policy_uuid" method="get" path="/v1/time_off_policies/{time_off_policy_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1TimeOffPoliciesTimeOffPolicyUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1TimeOffPoliciesTimeOffPolicyUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1TimeOffPoliciesTimeOffPolicyUuidResponse res = sdk.timeOffPolicies().get()
                .xGustoAPIVersion(GetV1TimeOffPoliciesTimeOffPolicyUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .timeOffPolicyUuid("<id>")
                .call();

        if (res.timeOffPolicy().isPresent()) {
            System.out.println(res.timeOffPolicy().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1TimeOffPoliciesTimeOffPolicyUuidHeaderXGustoAPIVersion>](../../models/operations/GetV1TimeOffPoliciesTimeOffPolicyUuidHeaderXGustoAPIVersion.md)                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `timeOffPolicyUuid`                                                                                                                                                                                                          | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the time off policy                                                                                                                                                                                              |

### Response

**[GetV1TimeOffPoliciesTimeOffPolicyUuidResponse](../../models/operations/GetV1TimeOffPoliciesTimeOffPolicyUuidResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## update

Update a time off policy

scope: `time_off_policies:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-time_off_policies-time_off_policy_uuid" method="put" path="/v1/time_off_policies/{time_off_policy_uuid}" -->
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

        PutV1TimeOffPoliciesTimeOffPolicyUuidResponse res = sdk.timeOffPolicies().update()
                .xGustoAPIVersion(PutV1TimeOffPoliciesTimeOffPolicyUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .timeOffPolicyUuid("<id>")
                .requestBody(PutV1TimeOffPoliciesTimeOffPolicyUuidRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .name("Vacation Policy")
                    .build())
                .call();

        if (res.timeOffPolicy().isPresent()) {
            System.out.println(res.timeOffPolicy().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1TimeOffPoliciesTimeOffPolicyUuidHeaderXGustoAPIVersion>](../../models/operations/PutV1TimeOffPoliciesTimeOffPolicyUuidHeaderXGustoAPIVersion.md)                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `timeOffPolicyUuid`                                                                                                                                                                                                          | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the time off policy                                                                                                                                                                                              |
| `requestBody`                                                                                                                                                                                                                | [PutV1TimeOffPoliciesTimeOffPolicyUuidRequestBody](../../models/operations/PutV1TimeOffPoliciesTimeOffPolicyUuidRequestBody.md)                                                                                              | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1TimeOffPoliciesTimeOffPolicyUuidResponse](../../models/operations/PutV1TimeOffPoliciesTimeOffPolicyUuidResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getAll

Get all time off policies for a company

scope: `time_off_policies:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_uuid-time_off_policies" method="get" path="/v1/companies/{company_uuid}/time_off_policies" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyUuidTimeOffPoliciesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyUuidTimeOffPoliciesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyUuidTimeOffPoliciesResponse res = sdk.timeOffPolicies().getAll()
                .xGustoAPIVersion(GetV1CompaniesCompanyUuidTimeOffPoliciesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .call();

        if (res.timeOffPolicies().isPresent()) {
            System.out.println(res.timeOffPolicies().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompaniesCompanyUuidTimeOffPoliciesHeaderXGustoAPIVersion>](../../models/operations/GetV1CompaniesCompanyUuidTimeOffPoliciesHeaderXGustoAPIVersion.md)                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |

### Response

**[GetV1CompaniesCompanyUuidTimeOffPoliciesResponse](../../models/operations/GetV1CompaniesCompanyUuidTimeOffPoliciesResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## create

Create a time off policy

scope: `time_off_policies:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_uuid-time_off_policies" method="post" path="/v1/companies/{company_uuid}/time_off_policies" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.*;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyUuidTimeOffPoliciesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyUuidTimeOffPoliciesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyUuidTimeOffPoliciesResponse res = sdk.timeOffPolicies().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyUuidTimeOffPoliciesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .timeOffPolicyRequest(TimeOffPolicyRequest.builder()
                    .name("Vacation Policy")
                    .policyType(TimeOffPolicyRequestPolicyType.VACATION)
                    .accrualMethod(AccrualMethod.PER_PAY_PERIOD)
                    .build())
                .call();

        if (res.timeOffPolicy().isPresent()) {
            System.out.println(res.timeOffPolicy().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompaniesCompanyUuidTimeOffPoliciesHeaderXGustoAPIVersion>](../../models/operations/PostV1CompaniesCompanyUuidTimeOffPoliciesHeaderXGustoAPIVersion.md)                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `timeOffPolicyRequest`                                                                                                                                                                                                       | [TimeOffPolicyRequest](../../models/components/TimeOffPolicyRequest.md)                                                                                                                                                      | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompaniesCompanyUuidTimeOffPoliciesResponse](../../models/operations/PostV1CompaniesCompanyUuidTimeOffPoliciesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## addEmployees

Add employees to a time off policy. Employees are required to have at least one job to be added to a time off policy. Accepts starting balances for non-unlimited policies

scope: `time_off_policies:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-time_off_policies-time_off_policy_uuid-add_employees" method="put" path="/v1/time_off_policies/{time_off_policy_uuid}/add_employees" -->
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

        PutV1TimeOffPoliciesTimeOffPolicyUuidAddEmployeesResponse res = sdk.timeOffPolicies().addEmployees()
                .xGustoAPIVersion(PutV1TimeOffPoliciesTimeOffPolicyUuidAddEmployeesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .timeOffPolicyUuid("<id>")
                .requestBody(PutV1TimeOffPoliciesTimeOffPolicyUuidAddEmployeesRequestBody.builder()
                    .employees(List.of())
                    .build())
                .call();

        if (res.timeOffPolicy().isPresent()) {
            System.out.println(res.timeOffPolicy().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1TimeOffPoliciesTimeOffPolicyUuidAddEmployeesHeaderXGustoAPIVersion>](../../models/operations/PutV1TimeOffPoliciesTimeOffPolicyUuidAddEmployeesHeaderXGustoAPIVersion.md)                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `timeOffPolicyUuid`                                                                                                                                                                                                          | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the time off policy                                                                                                                                                                                              |
| `requestBody`                                                                                                                                                                                                                | [PutV1TimeOffPoliciesTimeOffPolicyUuidAddEmployeesRequestBody](../../models/operations/PutV1TimeOffPoliciesTimeOffPolicyUuidAddEmployeesRequestBody.md)                                                                      | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1TimeOffPoliciesTimeOffPolicyUuidAddEmployeesResponse](../../models/operations/PutV1TimeOffPoliciesTimeOffPolicyUuidAddEmployeesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## removeEmployees

Remove employees from a time off policy

scope: `time_off_policies:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-time_off_policies-time_off_policy_uuid-remove_employees" method="put" path="/v1/time_off_policies/{time_off_policy_uuid}/remove_employees" -->
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

        PutV1TimeOffPoliciesTimeOffPolicyUuidRemoveEmployeesResponse res = sdk.timeOffPolicies().removeEmployees()
                .xGustoAPIVersion(PutV1TimeOffPoliciesTimeOffPolicyUuidRemoveEmployeesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .timeOffPolicyUuid("<id>")
                .requestBody(PutV1TimeOffPoliciesTimeOffPolicyUuidRemoveEmployeesRequestBody.builder()
                    .employees(List.of())
                    .build())
                .call();

        if (res.timeOffPolicy().isPresent()) {
            System.out.println(res.timeOffPolicy().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1TimeOffPoliciesTimeOffPolicyUuidRemoveEmployeesHeaderXGustoAPIVersion>](../../models/operations/PutV1TimeOffPoliciesTimeOffPolicyUuidRemoveEmployeesHeaderXGustoAPIVersion.md)                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `timeOffPolicyUuid`                                                                                                                                                                                                          | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the time off policy                                                                                                                                                                                              |
| `requestBody`                                                                                                                                                                                                                | [PutV1TimeOffPoliciesTimeOffPolicyUuidRemoveEmployeesRequestBody](../../models/operations/PutV1TimeOffPoliciesTimeOffPolicyUuidRemoveEmployeesRequestBody.md)                                                                | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1TimeOffPoliciesTimeOffPolicyUuidRemoveEmployeesResponse](../../models/operations/PutV1TimeOffPoliciesTimeOffPolicyUuidRemoveEmployeesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## updateBalance

Updates time off hours balances for employees for a time off policy.

scope: `time_off_policies:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-time_off_policies-time_off_policy_uuid-balance" method="put" path="/v1/time_off_policies/{time_off_policy_uuid}/balance" -->
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

        PutV1TimeOffPoliciesTimeOffPolicyUuidBalanceResponse res = sdk.timeOffPolicies().updateBalance()
                .xGustoAPIVersion(PutV1TimeOffPoliciesTimeOffPolicyUuidBalanceHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .timeOffPolicyUuid("<id>")
                .requestBody(PutV1TimeOffPoliciesTimeOffPolicyUuidBalanceRequestBody.builder()
                    .employees(List.of())
                    .build())
                .call();

        if (res.timeOffPolicy().isPresent()) {
            System.out.println(res.timeOffPolicy().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1TimeOffPoliciesTimeOffPolicyUuidBalanceHeaderXGustoAPIVersion>](../../models/operations/PutV1TimeOffPoliciesTimeOffPolicyUuidBalanceHeaderXGustoAPIVersion.md)                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `timeOffPolicyUuid`                                                                                                                                                                                                          | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the time off policy                                                                                                                                                                                              |
| `requestBody`                                                                                                                                                                                                                | [PutV1TimeOffPoliciesTimeOffPolicyUuidBalanceRequestBody](../../models/operations/PutV1TimeOffPoliciesTimeOffPolicyUuidBalanceRequestBody.md)                                                                                | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1TimeOffPoliciesTimeOffPolicyUuidBalanceResponse](../../models/operations/PutV1TimeOffPoliciesTimeOffPolicyUuidBalanceResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## deactivate

Deactivate a time off policy

scope: `time_off_policies:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-time_off_policies-time_off_policy_uuid-deactivate" method="put" path="/v1/time_off_policies/{time_off_policy_uuid}/deactivate" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1TimeOffPoliciesTimeOffPolicyUuidDeactivateHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1TimeOffPoliciesTimeOffPolicyUuidDeactivateResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1TimeOffPoliciesTimeOffPolicyUuidDeactivateResponse res = sdk.timeOffPolicies().deactivate()
                .xGustoAPIVersion(PutV1TimeOffPoliciesTimeOffPolicyUuidDeactivateHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .timeOffPolicyUuid("<id>")
                .call();

        if (res.timeOffPolicy().isPresent()) {
            System.out.println(res.timeOffPolicy().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1TimeOffPoliciesTimeOffPolicyUuidDeactivateHeaderXGustoAPIVersion>](../../models/operations/PutV1TimeOffPoliciesTimeOffPolicyUuidDeactivateHeaderXGustoAPIVersion.md)                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `timeOffPolicyUuid`                                                                                                                                                                                                          | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the time off policy                                                                                                                                                                                              |

### Response

**[PutV1TimeOffPoliciesTimeOffPolicyUuidDeactivateResponse](../../models/operations/PutV1TimeOffPoliciesTimeOffPolicyUuidDeactivateResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |