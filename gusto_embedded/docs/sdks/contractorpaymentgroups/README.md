# ContractorPaymentGroups

## Overview

### Available Operations

* [getList](#getlist) - Get contractor payment groups for a company
* [create](#create) - Create a contractor payment group
* [preview](#preview) - Preview a contractor payment group
* [get](#get) - Get a contractor payment group
* [delete](#delete) - Cancel a contractor payment group
* [fund](#fund) - Fund a contractor payment group [DEMO]
* [getV1ContractorPaymentGroupsIdPartnerDisbursements](#getv1contractorpaymentgroupsidpartnerdisbursements) - Get partner disbursements for a contractor payment group
* [patchV1ContractorPaymentGroupsIdPartnerDisbursements](#patchv1contractorpaymentgroupsidpartnerdisbursements) - Update partner disbursements for a contractor payment group

## getList

Returns a list of minimal contractor payment groups within a given time period, including totals but not associated contractor payments.

scope: `payrolls:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_id-contractor_payment_groups" method="get" path="/v1/companies/{company_id}/contractor_payment_groups" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyIdContractorPaymentGroupsRequest;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyIdContractorPaymentGroupsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyIdContractorPaymentGroupsRequest req = GetV1CompaniesCompanyIdContractorPaymentGroupsRequest.builder()
                .companyId("<id>")
                .startDate("2020-01-01")
                .endDate("2020-12-31")
                .build();

        GetV1CompaniesCompanyIdContractorPaymentGroupsResponse res = sdk.contractorPaymentGroups().getList()
                .request(req)
                .call();

        if (res.contractorPaymentGroupWithBlockers().isPresent()) {
            System.out.println(res.contractorPaymentGroupWithBlockers().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                 | Type                                                                                                                                      | Required                                                                                                                                  | Description                                                                                                                               |
| ----------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `request`                                                                                                                                 | [GetV1CompaniesCompanyIdContractorPaymentGroupsRequest](../../models/operations/GetV1CompaniesCompanyIdContractorPaymentGroupsRequest.md) | :heavy_check_mark:                                                                                                                        | The request object to use for the request.                                                                                                |

### Response

**[GetV1CompaniesCompanyIdContractorPaymentGroupsResponse](../../models/operations/GetV1CompaniesCompanyIdContractorPaymentGroupsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## create

Pay a group of contractors. Information needed depends on the contractor's wage type (hourly vs fixed)

scope: `payrolls:run`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-contractor_payment_groups" method="post" path="/v1/companies/{company_id}/contractor_payment_groups" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;
import java.time.LocalDate;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyIdContractorPaymentGroupsResponse res = sdk.contractorPaymentGroups().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdContractorPaymentGroupsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .requestBody(PostV1CompaniesCompanyIdContractorPaymentGroupsRequestBody.builder()
                    .checkDate(LocalDate.parse("2020-01-01"))
                    .creationToken("1d532d13-8f61-4a57-ad3c-b5fac1c6e05e")
                    .contractorPayments(List.of())
                    .build())
                .call();

        if (res.contractorPaymentGroup().isPresent()) {
            System.out.println(res.contractorPaymentGroup().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompaniesCompanyIdContractorPaymentGroupsHeaderXGustoAPIVersion>](../../models/operations/PostV1CompaniesCompanyIdContractorPaymentGroupsHeaderXGustoAPIVersion.md)                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `requestBody`                                                                                                                                                                                                                | [PostV1CompaniesCompanyIdContractorPaymentGroupsRequestBody](../../models/operations/PostV1CompaniesCompanyIdContractorPaymentGroupsRequestBody.md)                                                                          | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompaniesCompanyIdContractorPaymentGroupsResponse](../../models/operations/PostV1CompaniesCompanyIdContractorPaymentGroupsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## preview

Preview a group of contractor payments. Request will validate inputs and return preview of the contractor payment group including the expected `debit_date`. The `uuid` field will be null in the response.

The returned `creation_token` is a required parameter in order to create the contractor payment group.

scope: `payrolls:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-contractor_payment_groups-preview" method="post" path="/v1/companies/{company_id}/contractor_payment_groups/preview" -->
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

        PostV1CompaniesCompanyIdContractorPaymentGroupsPreviewResponse res = sdk.contractorPaymentGroups().preview()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdContractorPaymentGroupsPreviewHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .requestBody(PostV1CompaniesCompanyIdContractorPaymentGroupsPreviewRequestBody.builder()
                    .contractorPayments(List.of())
                    .build())
                .call();

        if (res.contractorPaymentGroupPreview().isPresent()) {
            System.out.println(res.contractorPaymentGroupPreview().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompaniesCompanyIdContractorPaymentGroupsPreviewHeaderXGustoAPIVersion>](../../models/operations/PostV1CompaniesCompanyIdContractorPaymentGroupsPreviewHeaderXGustoAPIVersion.md)                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `requestBody`                                                                                                                                                                                                                | [PostV1CompaniesCompanyIdContractorPaymentGroupsPreviewRequestBody](../../models/operations/PostV1CompaniesCompanyIdContractorPaymentGroupsPreviewRequestBody.md)                                                            | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompaniesCompanyIdContractorPaymentGroupsPreviewResponse](../../models/operations/PostV1CompaniesCompanyIdContractorPaymentGroupsPreviewResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## get

Returns a contractor payment group with all associated contractor payments.

scope: `payrolls:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-contractor_payment_groups-contractor_payment_group_id" method="get" path="/v1/contractor_payment_groups/{contractor_payment_group_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1ContractorPaymentGroupsContractorPaymentGroupIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1ContractorPaymentGroupsContractorPaymentGroupIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1ContractorPaymentGroupsContractorPaymentGroupIdResponse res = sdk.contractorPaymentGroups().get()
                .contractorPaymentGroupUuid("<id>")
                .xGustoAPIVersion(GetV1ContractorPaymentGroupsContractorPaymentGroupIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.contractorPaymentGroup().isPresent()) {
            System.out.println(res.contractorPaymentGroup().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `contractorPaymentGroupUuid`                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor payment group                                                                                                                                                                                     |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1ContractorPaymentGroupsContractorPaymentGroupIdHeaderXGustoAPIVersion>](../../models/operations/GetV1ContractorPaymentGroupsContractorPaymentGroupIdHeaderXGustoAPIVersion.md)                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1ContractorPaymentGroupsContractorPaymentGroupIdResponse](../../models/operations/GetV1ContractorPaymentGroupsContractorPaymentGroupIdResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## delete

Cancels a contractor payment group and all associated contractor payments. All contractor payments must be cancellable, unfunded.

scope: `payrolls:run`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-contractor_payment_groups-contractor_payment_group_id" method="delete" path="/v1/contractor_payment_groups/{contractor_payment_group_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.DeleteV1ContractorPaymentGroupsContractorPaymentGroupIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.DeleteV1ContractorPaymentGroupsContractorPaymentGroupIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1ContractorPaymentGroupsContractorPaymentGroupIdResponse res = sdk.contractorPaymentGroups().delete()
                .contractorPaymentGroupUuid("<id>")
                .xGustoAPIVersion(DeleteV1ContractorPaymentGroupsContractorPaymentGroupIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `contractorPaymentGroupUuid`                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor payment group                                                                                                                                                                                     |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1ContractorPaymentGroupsContractorPaymentGroupIdHeaderXGustoAPIVersion>](../../models/operations/DeleteV1ContractorPaymentGroupsContractorPaymentGroupIdHeaderXGustoAPIVersion.md)                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[DeleteV1ContractorPaymentGroupsContractorPaymentGroupIdResponse](../../models/operations/DeleteV1ContractorPaymentGroupsContractorPaymentGroupIdResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## fund

> 🚧 Demo action
> This action is only available in the Demo environment

Simulate funding a contractor payment group. Funding only occurs automatically in the production environment when bank transactions are generated. Use this action in the demo environment to transition a contractor payment group's `status` from `Unfunded` to `Funded`. A `Funded` status is required for generating a contractor payment receipt.

scope: `payrolls:run`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-contractor_payment_groups-contractor_payment_group_id-fund" method="put" path="/v1/contractor_payment_groups/{contractor_payment_group_uuid}/fund" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1ContractorPaymentGroupsContractorPaymentGroupIdFundHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1ContractorPaymentGroupsContractorPaymentGroupIdFundResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1ContractorPaymentGroupsContractorPaymentGroupIdFundResponse res = sdk.contractorPaymentGroups().fund()
                .contractorPaymentGroupUuid("<id>")
                .xGustoAPIVersion(PutV1ContractorPaymentGroupsContractorPaymentGroupIdFundHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.contractorPaymentGroup().isPresent()) {
            System.out.println(res.contractorPaymentGroup().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `contractorPaymentGroupUuid`                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor payment group                                                                                                                                                                                     |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1ContractorPaymentGroupsContractorPaymentGroupIdFundHeaderXGustoAPIVersion>](../../models/operations/PutV1ContractorPaymentGroupsContractorPaymentGroupIdFundHeaderXGustoAPIVersion.md)                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[PutV1ContractorPaymentGroupsContractorPaymentGroupIdFundResponse](../../models/operations/PutV1ContractorPaymentGroupsContractorPaymentGroupIdFundResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getV1ContractorPaymentGroupsIdPartnerDisbursements

Get partner disbursements for a specific contractor payment group.

scope: `partner_disbursements:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-contractor_payment_groups-id-partner_disbursements" method="get" path="/v1/contractor_payment_groups/{id}/partner_disbursements" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1ContractorPaymentGroupsIdPartnerDisbursementsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1ContractorPaymentGroupsIdPartnerDisbursementsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1ContractorPaymentGroupsIdPartnerDisbursementsResponse res = sdk.contractorPaymentGroups().getV1ContractorPaymentGroupsIdPartnerDisbursements()
                .id("<id>")
                .xGustoAPIVersion(GetV1ContractorPaymentGroupsIdPartnerDisbursementsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.contractorPaymentGroupPartnerDisbursements().isPresent()) {
            System.out.println(res.contractorPaymentGroupPartnerDisbursements().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                                                                                         | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor payment group                                                                                                                                                                                     |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1ContractorPaymentGroupsIdPartnerDisbursementsHeaderXGustoAPIVersion>](../../models/operations/GetV1ContractorPaymentGroupsIdPartnerDisbursementsHeaderXGustoAPIVersion.md)                                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1ContractorPaymentGroupsIdPartnerDisbursementsResponse](../../models/operations/GetV1ContractorPaymentGroupsIdPartnerDisbursementsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## patchV1ContractorPaymentGroupsIdPartnerDisbursements

Update partner disbursements for a specific contractor payment group.

scope: `partner_disbursements:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="patch-v1-contractor_payment_groups-id-partner_disbursements" method="patch" path="/v1/contractor_payment_groups/{id}/partner_disbursements" -->
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

        PatchV1ContractorPaymentGroupsIdPartnerDisbursementsResponse res = sdk.contractorPaymentGroups().patchV1ContractorPaymentGroupsIdPartnerDisbursements()
                .id("<id>")
                .xGustoAPIVersion(PatchV1ContractorPaymentGroupsIdPartnerDisbursementsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PatchV1ContractorPaymentGroupsIdPartnerDisbursementsRequestBody.builder()
                    .disbursements(List.of(
                        Disbursements.builder()
                            .contractorPaymentUuid("9f8e7d6c-5b4a-3928-1c2d-3e4f5a6b7c8d")
                            .build()))
                    .build())
                .call();

        if (res.contractorPaymentGroupPartnerDisbursements().isPresent()) {
            System.out.println(res.contractorPaymentGroupPartnerDisbursements().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                                                                                         | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor payment group                                                                                                                                                                                     |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PatchV1ContractorPaymentGroupsIdPartnerDisbursementsHeaderXGustoAPIVersion>](../../models/operations/PatchV1ContractorPaymentGroupsIdPartnerDisbursementsHeaderXGustoAPIVersion.md)                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `requestBody`                                                                                                                                                                                                                | [Optional\<PatchV1ContractorPaymentGroupsIdPartnerDisbursementsRequestBody>](../../models/operations/PatchV1ContractorPaymentGroupsIdPartnerDisbursementsRequestBody.md)                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PatchV1ContractorPaymentGroupsIdPartnerDisbursementsResponse](../../models/operations/PatchV1ContractorPaymentGroupsIdPartnerDisbursementsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |