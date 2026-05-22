# TimeOffRequests

## Overview

### Available Operations

* [postV1CompaniesCompanyUuidTimeOffAdminApprovedRequests](#postv1companiescompanyuuidtimeoffadminapprovedrequests) - Create an admin-approved time off request
* [getV1CompaniesCompanyUuidTimeOffBalances](#getv1companiescompanyuuidtimeoffbalances) - Get time off balances for a company
* [getV1CompaniesCompanyUuidTimeOffRequests](#getv1companiescompanyuuidtimeoffrequests) - List time off requests for a company
* [postV1CompaniesCompanyUuidTimeOffRequests](#postv1companiescompanyuuidtimeoffrequests) - Create a time off request
* [postV1CompaniesCompanyUuidTimeOffRequestsPreview](#postv1companiescompanyuuidtimeoffrequestspreview) - Preview a time off request
* [getV1TimeOffRequestsTimeOffRequestUuid](#getv1timeoffrequeststimeoffrequestuuid) - Get a time off request
* [deleteV1TimeOffRequestsTimeOffRequestUuid](#deletev1timeoffrequeststimeoffrequestuuid) - Delete a time off request
* [putV1TimeOffRequestsTimeOffRequestUuidApprove](#putv1timeoffrequeststimeoffrequestuuidapprove) - Approve a time off request
* [putV1TimeOffRequestsTimeOffRequestUuidDecline](#putv1timeoffrequeststimeoffrequestuuiddecline) - Decline a time off request

## postV1CompaniesCompanyUuidTimeOffAdminApprovedRequests

Create a pre-approved time off request on behalf of an employee (admin or system initiated).
The request is always created with approved status.

scope: `time_off_requests:manage`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_uuid-time_off-admin_approved_requests" method="post" path="/v1/companies/{company_uuid}/time_off/admin_approved_requests" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;
import java.util.Map;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyUuidTimeOffAdminApprovedRequestsResponse res = sdk.timeOffRequests().postV1CompaniesCompanyUuidTimeOffAdminApprovedRequests()
                .xGustoAPIVersion(PostV1CompaniesCompanyUuidTimeOffAdminApprovedRequestsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyUuid("<id>")
                .requestBody(PostV1CompaniesCompanyUuidTimeOffAdminApprovedRequestsRequestBody.builder()
                    .employeeUuid("<id>")
                    .policyUuid("<id>")
                    .startDate("<value>")
                    .endDate("<value>")
                    .days(Map.ofEntries(
                        Map.entry("key", "<value>"),
                        Map.entry("key1", "<value>"),
                        Map.entry("key2", "<value>")))
                    .build())
                .call();

        if (res.embeddedTimeOffRequest().isPresent()) {
            System.out.println(res.embeddedTimeOffRequest().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompaniesCompanyUuidTimeOffAdminApprovedRequestsHeaderXGustoAPIVersion>](../../models/operations/PostV1CompaniesCompanyUuidTimeOffAdminApprovedRequestsHeaderXGustoAPIVersion.md)                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `requestBody`                                                                                                                                                                                                                | [PostV1CompaniesCompanyUuidTimeOffAdminApprovedRequestsRequestBody](../../models/operations/PostV1CompaniesCompanyUuidTimeOffAdminApprovedRequestsRequestBody.md)                                                            | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompaniesCompanyUuidTimeOffAdminApprovedRequestsResponse](../../models/operations/PostV1CompaniesCompanyUuidTimeOffAdminApprovedRequestsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## getV1CompaniesCompanyUuidTimeOffBalances

Get time off balances for all employees in a company

scope: `time_off_requests:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_uuid-time_off-balances" method="get" path="/v1/companies/{company_uuid}/time_off/balances" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyUuidTimeOffBalancesRequest;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyUuidTimeOffBalancesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyUuidTimeOffBalancesRequest req = GetV1CompaniesCompanyUuidTimeOffBalancesRequest.builder()
                .companyUuid("<id>")
                .build();

        GetV1CompaniesCompanyUuidTimeOffBalancesResponse res = sdk.timeOffRequests().getV1CompaniesCompanyUuidTimeOffBalances()
                .request(req)
                .call();

        if (res.embeddedTimeOffBalances().isPresent()) {
            System.out.println(res.embeddedTimeOffBalances().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                     | Type                                                                                                                          | Required                                                                                                                      | Description                                                                                                                   |
| ----------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `request`                                                                                                                     | [GetV1CompaniesCompanyUuidTimeOffBalancesRequest](../../models/operations/GetV1CompaniesCompanyUuidTimeOffBalancesRequest.md) | :heavy_check_mark:                                                                                                            | The request object to use for the request.                                                                                    |

### Response

**[GetV1CompaniesCompanyUuidTimeOffBalancesResponse](../../models/operations/GetV1CompaniesCompanyUuidTimeOffBalancesResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## getV1CompaniesCompanyUuidTimeOffRequests

Get all time off requests for a company. Supports filtering by status, employee, and date ranges.

Possible statuses:
- `pending` — awaiting approval
- `approved` — approved by an admin but not yet processed in a payroll
- `declined` — declined by an admin
- `consumed` — processed in a completed payroll

Allowed values for `status`: pending, approved, declined, consumed.

scope: `time_off_requests:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_uuid-time_off-requests" method="get" path="/v1/companies/{company_uuid}/time_off/requests" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyUuidTimeOffRequestsRequest;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyUuidTimeOffRequestsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyUuidTimeOffRequestsRequest req = GetV1CompaniesCompanyUuidTimeOffRequestsRequest.builder()
                .companyUuid("<id>")
                .build();

        GetV1CompaniesCompanyUuidTimeOffRequestsResponse res = sdk.timeOffRequests().getV1CompaniesCompanyUuidTimeOffRequests()
                .request(req)
                .call();

        if (res.embeddedTimeOffRequests().isPresent()) {
            System.out.println(res.embeddedTimeOffRequests().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                     | Type                                                                                                                          | Required                                                                                                                      | Description                                                                                                                   |
| ----------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `request`                                                                                                                     | [GetV1CompaniesCompanyUuidTimeOffRequestsRequest](../../models/operations/GetV1CompaniesCompanyUuidTimeOffRequestsRequest.md) | :heavy_check_mark:                                                                                                            | The request object to use for the request.                                                                                    |

### Response

**[GetV1CompaniesCompanyUuidTimeOffRequestsResponse](../../models/operations/GetV1CompaniesCompanyUuidTimeOffRequestsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## postV1CompaniesCompanyUuidTimeOffRequests

Create a time off request for an employee

scope: `time_off_requests:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_uuid-time_off-requests" method="post" path="/v1/companies/{company_uuid}/time_off/requests" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;
import java.util.Map;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyUuidTimeOffRequestsResponse res = sdk.timeOffRequests().postV1CompaniesCompanyUuidTimeOffRequests()
                .xGustoAPIVersion(PostV1CompaniesCompanyUuidTimeOffRequestsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyUuid("<id>")
                .requestBody(PostV1CompaniesCompanyUuidTimeOffRequestsRequestBody.builder()
                    .employeeUuid("<id>")
                    .policyUuid("<id>")
                    .startDate("<value>")
                    .endDate("<value>")
                    .days(Map.ofEntries(
                        Map.entry("key", "<value>"),
                        Map.entry("key1", "<value>"),
                        Map.entry("key2", "<value>")))
                    .build())
                .call();

        if (res.embeddedTimeOffRequest().isPresent()) {
            System.out.println(res.embeddedTimeOffRequest().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompaniesCompanyUuidTimeOffRequestsHeaderXGustoAPIVersion>](../../models/operations/PostV1CompaniesCompanyUuidTimeOffRequestsHeaderXGustoAPIVersion.md)                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `requestBody`                                                                                                                                                                                                                | [PostV1CompaniesCompanyUuidTimeOffRequestsRequestBody](../../models/operations/PostV1CompaniesCompanyUuidTimeOffRequestsRequestBody.md)                                                                                      | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompaniesCompanyUuidTimeOffRequestsResponse](../../models/operations/PostV1CompaniesCompanyUuidTimeOffRequestsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## postV1CompaniesCompanyUuidTimeOffRequestsPreview

Preview a time off request to see balance impact before creating

scope: `time_off_requests:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_uuid-time_off-requests-preview" method="post" path="/v1/companies/{company_uuid}/time_off/requests/preview" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;
import java.util.Map;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyUuidTimeOffRequestsPreviewResponse res = sdk.timeOffRequests().postV1CompaniesCompanyUuidTimeOffRequestsPreview()
                .xGustoAPIVersion(PostV1CompaniesCompanyUuidTimeOffRequestsPreviewHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyUuid("<id>")
                .requestBody(PostV1CompaniesCompanyUuidTimeOffRequestsPreviewRequestBody.builder()
                    .employeeUuid("<id>")
                    .policyUuid("<id>")
                    .startDate("<value>")
                    .endDate("<value>")
                    .days(Map.ofEntries(
                        Map.entry("key", "<value>"),
                        Map.entry("key1", "<value>"),
                        Map.entry("key2", "<value>")))
                    .build())
                .call();

        if (res.embeddedTimeOffRequestPreview().isPresent()) {
            System.out.println(res.embeddedTimeOffRequestPreview().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompaniesCompanyUuidTimeOffRequestsPreviewHeaderXGustoAPIVersion>](../../models/operations/PostV1CompaniesCompanyUuidTimeOffRequestsPreviewHeaderXGustoAPIVersion.md)                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `requestBody`                                                                                                                                                                                                                | [PostV1CompaniesCompanyUuidTimeOffRequestsPreviewRequestBody](../../models/operations/PostV1CompaniesCompanyUuidTimeOffRequestsPreviewRequestBody.md)                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompaniesCompanyUuidTimeOffRequestsPreviewResponse](../../models/operations/PostV1CompaniesCompanyUuidTimeOffRequestsPreviewResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## getV1TimeOffRequestsTimeOffRequestUuid

Get a single time off request by UUID

scope: `time_off_requests:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-time_off-requests-time_off_request_uuid" method="get" path="/v1/time_off/requests/{time_off_request_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1TimeOffRequestsTimeOffRequestUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1TimeOffRequestsTimeOffRequestUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1TimeOffRequestsTimeOffRequestUuidResponse res = sdk.timeOffRequests().getV1TimeOffRequestsTimeOffRequestUuid()
                .xGustoAPIVersion(GetV1TimeOffRequestsTimeOffRequestUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .timeOffRequestUuid("<id>")
                .call();

        if (res.embeddedTimeOffRequest().isPresent()) {
            System.out.println(res.embeddedTimeOffRequest().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1TimeOffRequestsTimeOffRequestUuidHeaderXGustoAPIVersion>](../../models/operations/GetV1TimeOffRequestsTimeOffRequestUuidHeaderXGustoAPIVersion.md)                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `timeOffRequestUuid`                                                                                                                                                                                                         | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the time off request                                                                                                                                                                                             |

### Response

**[GetV1TimeOffRequestsTimeOffRequestUuidResponse](../../models/operations/GetV1TimeOffRequestsTimeOffRequestUuidResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## deleteV1TimeOffRequestsTimeOffRequestUuid

Delete a time off request

scope: `time_off_requests:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-time_off-requests-time_off_request_uuid" method="delete" path="/v1/time_off/requests/{time_off_request_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.operations.DeleteV1TimeOffRequestsTimeOffRequestUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.DeleteV1TimeOffRequestsTimeOffRequestUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1TimeOffRequestsTimeOffRequestUuidResponse res = sdk.timeOffRequests().deleteV1TimeOffRequestsTimeOffRequestUuid()
                .xGustoAPIVersion(DeleteV1TimeOffRequestsTimeOffRequestUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .timeOffRequestUuid("<id>")
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1TimeOffRequestsTimeOffRequestUuidHeaderXGustoAPIVersion>](../../models/operations/DeleteV1TimeOffRequestsTimeOffRequestUuidHeaderXGustoAPIVersion.md)                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `timeOffRequestUuid`                                                                                                                                                                                                         | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the time off request                                                                                                                                                                                             |

### Response

**[DeleteV1TimeOffRequestsTimeOffRequestUuidResponse](../../models/operations/DeleteV1TimeOffRequestsTimeOffRequestUuidResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |

## putV1TimeOffRequestsTimeOffRequestUuidApprove

Approve a pending time off request. Optionally override the dates and hours.

Only requests with a `pending` status can be approved. Attempting to approve a request that has already been `declined` or `consumed` will fail with a 422 error.

scope: `time_off_requests:manage`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-time_off-requests-time_off_request_uuid-approve" method="put" path="/v1/time_off/requests/{time_off_request_uuid}/approve" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1TimeOffRequestsTimeOffRequestUuidApproveHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1TimeOffRequestsTimeOffRequestUuidApproveResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1TimeOffRequestsTimeOffRequestUuidApproveResponse res = sdk.timeOffRequests().putV1TimeOffRequestsTimeOffRequestUuidApprove()
                .xGustoAPIVersion(PutV1TimeOffRequestsTimeOffRequestUuidApproveHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .timeOffRequestUuid("<id>")
                .call();

        if (res.embeddedTimeOffRequest().isPresent()) {
            System.out.println(res.embeddedTimeOffRequest().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1TimeOffRequestsTimeOffRequestUuidApproveHeaderXGustoAPIVersion>](../../models/operations/PutV1TimeOffRequestsTimeOffRequestUuidApproveHeaderXGustoAPIVersion.md)                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `timeOffRequestUuid`                                                                                                                                                                                                         | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the time off request                                                                                                                                                                                             |
| `requestBody`                                                                                                                                                                                                                | [Optional\<PutV1TimeOffRequestsTimeOffRequestUuidApproveRequestBody>](../../models/operations/PutV1TimeOffRequestsTimeOffRequestUuidApproveRequestBody.md)                                                                   | :heavy_minus_sign:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1TimeOffRequestsTimeOffRequestUuidApproveResponse](../../models/operations/PutV1TimeOffRequestsTimeOffRequestUuidApproveResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## putV1TimeOffRequestsTimeOffRequestUuidDecline

Decline a pending or approved time off request. Requires an employer_note.

scope: `time_off_requests:manage`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-time_off-requests-time_off_request_uuid-decline" method="put" path="/v1/time_off/requests/{time_off_request_uuid}/decline" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1TimeOffRequestsTimeOffRequestUuidDeclineResponse res = sdk.timeOffRequests().putV1TimeOffRequestsTimeOffRequestUuidDecline()
                .xGustoAPIVersion(PutV1TimeOffRequestsTimeOffRequestUuidDeclineHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .timeOffRequestUuid("<id>")
                .requestBody(PutV1TimeOffRequestsTimeOffRequestUuidDeclineRequestBody.builder()
                    .employerNote("<value>")
                    .build())
                .call();

        if (res.embeddedTimeOffRequest().isPresent()) {
            System.out.println(res.embeddedTimeOffRequest().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1TimeOffRequestsTimeOffRequestUuidDeclineHeaderXGustoAPIVersion>](../../models/operations/PutV1TimeOffRequestsTimeOffRequestUuidDeclineHeaderXGustoAPIVersion.md)                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `timeOffRequestUuid`                                                                                                                                                                                                         | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the time off request                                                                                                                                                                                             |
| `requestBody`                                                                                                                                                                                                                | [PutV1TimeOffRequestsTimeOffRequestUuidDeclineRequestBody](../../models/operations/PutV1TimeOffRequestsTimeOffRequestUuidDeclineRequestBody.md)                                                                              | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1TimeOffRequestsTimeOffRequestUuidDeclineResponse](../../models/operations/PutV1TimeOffRequestsTimeOffRequestUuidDeclineResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |