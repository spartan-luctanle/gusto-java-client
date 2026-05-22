# PaySchedules

## Overview

### Available Operations

* [getAll](#getall) - Get the pay schedules for a company
* [create](#create) - Create a new pay schedule
* [getPreview](#getpreview) - Preview pay schedule dates
* [get](#get) - Get a pay schedule
* [update](#update) - Update a pay schedule
* [getPayPeriods](#getpayperiods) - Get pay periods for a company
* [getUnprocessedTerminationPeriods](#getunprocessedterminationperiods) - Get termination pay periods for a company
* [getAssignments](#getassignments) - Get pay schedule assignments for a company
* [previewAssignment](#previewassignment) - Preview pay schedule assignments for a company
* [assign](#assign) - Assign pay schedules for a company

## getAll

Returns all pay schedules for a company. The pay schedule object captures the details of when employees work and when they should be paid. A company can have multiple pay schedules.

scope: `pay_schedules:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_id-pay_schedules" method="get" path="/v1/companies/{company_id}/pay_schedules" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdPaySchedulesHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdPaySchedulesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyIdPaySchedulesResponse res = sdk.paySchedules().getAll()
                .xGustoAPIVersion(GetV1CompaniesCompanyIdPaySchedulesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyId("<id>")
                .call();

        if (res.payScheduleShowResponse().isPresent()) {
            System.out.println(res.payScheduleShowResponse().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompaniesCompanyIdPaySchedulesHeaderXGustoAPIVersion>](../../models/operations/GetV1CompaniesCompanyIdPaySchedulesHeaderXGustoAPIVersion.md)                                                                 | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `page`                                                                                                                                                                                                                       | *Optional\<Long>*                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                           | The page that is requested. When unspecified, will load all objects unless endpoint forces pagination.                                                                                                                       |
| `per`                                                                                                                                                                                                                        | *Optional\<Long>*                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                           | Number of objects per page. For majority of endpoints will default to 25                                                                                                                                                     |

### Response

**[GetV1CompaniesCompanyIdPaySchedulesResponse](../../models/operations/GetV1CompaniesCompanyIdPaySchedulesResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## create

If a company does not have any pay schedules, this endpoint will create a single pay schedule and assign it to all employees. This is a common use case during company onboarding.

If a company has an existing active pay schedule and want to support multiple pay schedules, this endpoint will create a pay schedule that is not assigned to any employee.

Be sure to **[check state laws](https://www.dol.gov/agencies/whd/state/payday)** to know what schedule is right for your customers.

> If an onboarded company misses their first pay date, Gusto will automatically adjust the pay schedule to the next available pay date.

### Webhooks
- `pay_schedule.created`: Fires when a pay schedule is successfully created.

### Related guides
- [Create a pay schedule](doc:create-a-pay-schedule)
- [Pay Schedules](doc:pay-schedule-info)
- [Manage Pay Schedules via API](doc:manage-pay-schedules-api)

scope: `pay_schedules:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-pay_schedules" method="post" path="/v1/companies/{company_id}/pay_schedules" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.Frequency;
import com.gusto.embedded_api_v_2025_11_15.models.components.PayScheduleCreateRequest;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1CompaniesCompanyIdPaySchedulesHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1CompaniesCompanyIdPaySchedulesResponse;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyIdPaySchedulesResponse res = sdk.paySchedules().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdPaySchedulesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyId("<id>")
                .payScheduleCreateRequest(PayScheduleCreateRequest.builder()
                    .frequency(Frequency.TWICE_PER_MONTH)
                    .anchorPayDate(LocalDate.parse("2020-05-15"))
                    .anchorEndOfPayPeriod(LocalDate.parse("2020-05-08"))
                    .day1(15L)
                    .day2(31L)
                    .customName("demo pay schedule")
                    .build())
                .call();

        if (res.payScheduleShow().isPresent()) {
            System.out.println(res.payScheduleShow().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  | Example                                                                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompaniesCompanyIdPaySchedulesHeaderXGustoAPIVersion>](../../models/operations/PostV1CompaniesCompanyIdPaySchedulesHeaderXGustoAPIVersion.md)                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |                                                                                                                                                                                                                              |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |                                                                                                                                                                                                                              |
| `payScheduleCreateRequest`                                                                                                                                                                                                   | [PayScheduleCreateRequest](../../models/components/PayScheduleCreateRequest.md)                                                                                                                                              | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          | {<br/>"frequency": "Twice per month",<br/>"anchor_pay_date": "2020-05-15",<br/>"anchor_end_of_pay_period": "2020-05-08",<br/>"day_1": 15,<br/>"day_2": 31,<br/>"custom_name": "demo pay schedule"<br/>}                      |

### Response

**[PostV1CompaniesCompanyIdPaySchedulesResponse](../../models/operations/PostV1CompaniesCompanyIdPaySchedulesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getPreview

Provides a preview of a pay schedule with the specified parameters for the next 18 months. Use this before creating or updating a pay schedule to show expected check dates, pay period boundaries, and payroll deadlines.

### Related guides
- [Create a pay schedule](doc:create-a-pay-schedule)
- [Manage Pay Schedules via API](doc:manage-pay-schedules-api)

scope: `pay_schedules:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_id-pay_schedules-preview" method="get" path="/v1/companies/{company_id}/pay_schedules/preview" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyIdPaySchedulesPreviewRequest req = GetV1CompaniesCompanyIdPaySchedulesPreviewRequest.builder()
                .companyId("<id>")
                .frequency(Frequency.TWICE_PER_MONTH)
                .anchorPayDate(LocalDate.parse("2020-05-15"))
                .anchorEndOfPayPeriod(LocalDate.parse("2020-05-08"))
                .day1(15L)
                .day2(31L)
                .build();

        GetV1CompaniesCompanyIdPaySchedulesPreviewResponse res = sdk.paySchedules().getPreview()
                .request(req)
                .call();

        if (res.paySchedulePreview().isPresent()) {
            System.out.println(res.paySchedulePreview().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                         | Type                                                                                                                              | Required                                                                                                                          | Description                                                                                                                       |
| --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `request`                                                                                                                         | [GetV1CompaniesCompanyIdPaySchedulesPreviewRequest](../../models/operations/GetV1CompaniesCompanyIdPaySchedulesPreviewRequest.md) | :heavy_check_mark:                                                                                                                | The request object to use for the request.                                                                                        |

### Response

**[GetV1CompaniesCompanyIdPaySchedulesPreviewResponse](../../models/operations/GetV1CompaniesCompanyIdPaySchedulesPreviewResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## get

Returns a single pay schedule by UUID. The pay schedule object in Gusto captures the details of when employees work and when they should be paid. A company can have multiple pay schedules.

scope: `pay_schedules:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_id-pay_schedules-pay_schedule_id" method="get" path="/v1/companies/{company_id}/pay_schedules/{pay_schedule_id}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdPaySchedulesPayScheduleIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdPaySchedulesPayScheduleIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyIdPaySchedulesPayScheduleIdResponse res = sdk.paySchedules().get()
                .xGustoAPIVersion(GetV1CompaniesCompanyIdPaySchedulesPayScheduleIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyId("<id>")
                .payScheduleId("<id>")
                .call();

        if (res.payScheduleShow().isPresent()) {
            System.out.println(res.payScheduleShow().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompaniesCompanyIdPaySchedulesPayScheduleIdHeaderXGustoAPIVersion>](../../models/operations/GetV1CompaniesCompanyIdPaySchedulesPayScheduleIdHeaderXGustoAPIVersion.md)                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `payScheduleId`                                                                                                                                                                                                              | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the pay schedule                                                                                                                                                                                                 |

### Response

**[GetV1CompaniesCompanyIdPaySchedulesPayScheduleIdResponse](../../models/operations/GetV1CompaniesCompanyIdPaySchedulesPayScheduleIdResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## update

Updates a pay schedule. The `version` parameter from the GET response is required for [optimistic concurrency](doc:api-fundamentals); a mismatch returns 409 Conflict.

### Effect on payrolls
Updating a pay schedule will delete any unprocessed regular payrolls whose pay period end date is today or in the future. Already-processed payrolls are not affected.

### Pay schedules may be automatically adjusted
If an onboarded company misses their first pay date, Gusto will automatically adjust the pay schedule to the next available pay date.

### Webhooks
- `pay_schedule.updated`: Fires when a pay schedule is successfully updated.

### Related guides
- [Create a pay schedule](doc:create-a-pay-schedule)
- [Manage Pay Schedules via API](doc:manage-pay-schedules-api)

scope: `pay_schedules:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_id-pay_schedules-pay_schedule_id" method="put" path="/v1/companies/{company_id}/pay_schedules/{pay_schedule_id}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.PayScheduleUpdateRequest;
import com.gusto.embedded_api_v_2025_11_15.models.components.PayScheduleUpdateRequestFrequency;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1CompaniesCompanyIdPaySchedulesPayScheduleIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1CompaniesCompanyIdPaySchedulesPayScheduleIdResponse;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompaniesCompanyIdPaySchedulesPayScheduleIdResponse res = sdk.paySchedules().update()
                .xGustoAPIVersion(PutV1CompaniesCompanyIdPaySchedulesPayScheduleIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyId("<id>")
                .payScheduleId("<id>")
                .payScheduleUpdateRequest(PayScheduleUpdateRequest.builder()
                    .version("68934a3e9455fa72420237eb05902327")
                    .autoPayroll(true)
                    .frequency(PayScheduleUpdateRequestFrequency.TWICE_PER_MONTH)
                    .anchorPayDate(LocalDate.parse("2021-10-15"))
                    .anchorEndOfPayPeriod(LocalDate.parse("2021-10-15"))
                    .day1(15L)
                    .day2(31L)
                    .customName("demo pay schedule")
                    .build())
                .call();

        if (res.payScheduleShow().isPresent()) {
            System.out.println(res.payScheduleShow().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                                        | Type                                                                                                                                                                                                                                             | Required                                                                                                                                                                                                                                         | Description                                                                                                                                                                                                                                      | Example                                                                                                                                                                                                                                          |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `xGustoAPIVersion`                                                                                                                                                                                                                               | [Optional\<PutV1CompaniesCompanyIdPaySchedulesPayScheduleIdHeaderXGustoAPIVersion>](../../models/operations/PutV1CompaniesCompanyIdPaySchedulesPayScheduleIdHeaderXGustoAPIVersion.md)                                                           | :heavy_minus_sign:                                                                                                                                                                                                                               | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used.                     |                                                                                                                                                                                                                                                  |
| `companyId`                                                                                                                                                                                                                                      | *String*                                                                                                                                                                                                                                         | :heavy_check_mark:                                                                                                                                                                                                                               | The UUID of the company                                                                                                                                                                                                                          |                                                                                                                                                                                                                                                  |
| `payScheduleId`                                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                                         | :heavy_check_mark:                                                                                                                                                                                                                               | The UUID of the pay schedule                                                                                                                                                                                                                     |                                                                                                                                                                                                                                                  |
| `payScheduleUpdateRequest`                                                                                                                                                                                                                       | [PayScheduleUpdateRequest](../../models/components/PayScheduleUpdateRequest.md)                                                                                                                                                                  | :heavy_check_mark:                                                                                                                                                                                                                               | N/A                                                                                                                                                                                                                                              | {<br/>"version": "68934a3e9455fa72420237eb05902327",<br/>"auto_payroll": true,<br/>"frequency": "Twice per month",<br/>"anchor_pay_date": "2021-10-15",<br/>"anchor_end_of_pay_period": "2021-10-15",<br/>"day_1": 15,<br/>"day_2": 31,<br/>"custom_name": "demo pay schedule"<br/>} |

### Response

**[PutV1CompaniesCompanyIdPaySchedulesPayScheduleIdResponse](../../models/operations/PutV1CompaniesCompanyIdPaySchedulesPayScheduleIdResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 409, 422                               | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getPayPeriods

Pay periods are the foundation of payroll. Compensation, time & attendance, taxes, and expense reports all rely on when they happened.

To begin submitting information for a given payroll, we need to agree on the time period.

By default, this endpoint returns pay periods starting from 6 months ago to the date today. Use the `start_date` and `end_date` parameters to change the scope of the response. End dates can be up to 3 months in the future and there is no limit on start dates.

Starting in version 2023-04-01, the `eligible_employees` attribute was removed from the response. The eligible employees for a payroll are determined by the employee_compensations returned from the [PUT /v1/companies/{company_id}/payrolls/{payroll_id}/prepare](ref:put-v1-companies-company_id-payrolls-payroll_id-prepare) endpoint.

scope: `payrolls:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_id-pay_periods" method="get" path="/v1/companies/{company_id}/pay_periods" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdPayPeriodsRequest;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdPayPeriodsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyIdPayPeriodsRequest req = GetV1CompaniesCompanyIdPayPeriodsRequest.builder()
                .companyId("<id>")
                .build();

        GetV1CompaniesCompanyIdPayPeriodsResponse res = sdk.paySchedules().getPayPeriods()
                .request(req)
                .call();

        if (res.payPeriods().isPresent()) {
            System.out.println(res.payPeriods().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                       | Type                                                                                                            | Required                                                                                                        | Description                                                                                                     |
| --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| `request`                                                                                                       | [GetV1CompaniesCompanyIdPayPeriodsRequest](../../models/operations/GetV1CompaniesCompanyIdPayPeriodsRequest.md) | :heavy_check_mark:                                                                                              | The request object to use for the request.                                                                      |

### Response

**[GetV1CompaniesCompanyIdPayPeriodsResponse](../../models/operations/GetV1CompaniesCompanyIdPayPeriodsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getUnprocessedTerminationPeriods

When a payroll admin terminates an employee and selects "Dismissal Payroll" as the employee's final payroll, their last pay period will appear on the list.

This endpoint returns the unprocessed pay periods for past and future terminated employees in a given company.

scope: `payrolls:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_id-unprocessed_termination_pay_periods" method="get" path="/v1/companies/{company_id}/pay_periods/unprocessed_termination_pay_periods" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdUnprocessedTerminationPayPeriodsHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdUnprocessedTerminationPayPeriodsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyIdUnprocessedTerminationPayPeriodsResponse res = sdk.paySchedules().getUnprocessedTerminationPeriods()
                .xGustoAPIVersion(GetV1CompaniesCompanyIdUnprocessedTerminationPayPeriodsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyId("<id>")
                .call();

        if (res.unprocessedTerminationPayPeriods().isPresent()) {
            System.out.println(res.unprocessedTerminationPayPeriods().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompaniesCompanyIdUnprocessedTerminationPayPeriodsHeaderXGustoAPIVersion>](../../models/operations/GetV1CompaniesCompanyIdUnprocessedTerminationPayPeriodsHeaderXGustoAPIVersion.md)                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |

### Response

**[GetV1CompaniesCompanyIdUnprocessedTerminationPayPeriodsResponse](../../models/operations/GetV1CompaniesCompanyIdUnprocessedTerminationPayPeriodsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## getAssignments

This endpoint returns the current pay schedule assignment for a company, with pay schedule and employee/department mappings depending on the pay schedule type.

scope: `pay_schedules:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_id-pay_schedules-assignments" method="get" path="/v1/companies/{company_id}/pay_schedules/assignments" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdPaySchedulesAssignmentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdPaySchedulesAssignmentsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyIdPaySchedulesAssignmentsResponse res = sdk.paySchedules().getAssignments()
                .xGustoAPIVersion(GetV1CompaniesCompanyIdPaySchedulesAssignmentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyId("<id>")
                .call();

        if (res.payScheduleAssignment().isPresent()) {
            System.out.println(res.payScheduleAssignment().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompaniesCompanyIdPaySchedulesAssignmentsHeaderXGustoAPIVersion>](../../models/operations/GetV1CompaniesCompanyIdPaySchedulesAssignmentsHeaderXGustoAPIVersion.md)                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |

### Response

**[GetV1CompaniesCompanyIdPaySchedulesAssignmentsResponse](../../models/operations/GetV1CompaniesCompanyIdPaySchedulesAssignmentsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## previewAssignment

This endpoint returns the employee changes, including pay period and transition pay periods, for changing the pay schedule.

scope: `pay_schedules:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-pay_schedules-assignment_preview" method="post" path="/v1/companies/{company_id}/pay_schedules/assignment_preview" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.PayScheduleAssignmentBody;
import com.gusto.embedded_api_v_2025_11_15.models.components.PayScheduleAssignmentBodyType;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1CompaniesCompanyIdPaySchedulesAssignmentPreviewHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1CompaniesCompanyIdPaySchedulesAssignmentPreviewResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyIdPaySchedulesAssignmentPreviewResponse res = sdk.paySchedules().previewAssignment()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdPaySchedulesAssignmentPreviewHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyId("<id>")
                .payScheduleAssignmentBody(PayScheduleAssignmentBody.builder()
                    .type(PayScheduleAssignmentBodyType.BY_EMPLOYEE)
                    .build())
                .call();

        if (res.payScheduleAssignmentPreview().isPresent()) {
            System.out.println(res.payScheduleAssignmentPreview().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompaniesCompanyIdPaySchedulesAssignmentPreviewHeaderXGustoAPIVersion>](../../models/operations/PostV1CompaniesCompanyIdPaySchedulesAssignmentPreviewHeaderXGustoAPIVersion.md)                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `payScheduleAssignmentBody`                                                                                                                                                                                                  | [PayScheduleAssignmentBody](../../models/components/PayScheduleAssignmentBody.md)                                                                                                                                            | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompaniesCompanyIdPaySchedulesAssignmentPreviewResponse](../../models/operations/PostV1CompaniesCompanyIdPaySchedulesAssignmentPreviewResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## assign

This endpoint assigns employees to pay schedules based on the schedule type.
For `by_employee` and `by_department` schedules, use the `partial_assignment` parameter to control the assignment scope. Set it to `true` for partial assignments (only some employees or departments at a time) and `false` for full assignments (all employees or departments at once).

scope: `pay_schedules:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-pay_schedules-assign" method="post" path="/v1/companies/{company_id}/pay_schedules/assign" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.PayScheduleAssignmentBody;
import com.gusto.embedded_api_v_2025_11_15.models.components.PayScheduleAssignmentBodyType;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1CompaniesCompanyIdPaySchedulesAssignHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1CompaniesCompanyIdPaySchedulesAssignResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyIdPaySchedulesAssignResponse res = sdk.paySchedules().assign()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdPaySchedulesAssignHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyId("<id>")
                .payScheduleAssignmentBody(PayScheduleAssignmentBody.builder()
                    .type(PayScheduleAssignmentBodyType.BY_EMPLOYEE)
                    .build())
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompaniesCompanyIdPaySchedulesAssignHeaderXGustoAPIVersion>](../../models/operations/PostV1CompaniesCompanyIdPaySchedulesAssignHeaderXGustoAPIVersion.md)                                                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `payScheduleAssignmentBody`                                                                                                                                                                                                  | [PayScheduleAssignmentBody](../../models/components/PayScheduleAssignmentBody.md)                                                                                                                                            | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompaniesCompanyIdPaySchedulesAssignResponse](../../models/operations/PostV1CompaniesCompanyIdPaySchedulesAssignResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |