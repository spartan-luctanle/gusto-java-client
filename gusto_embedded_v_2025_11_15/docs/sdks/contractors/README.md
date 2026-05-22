# Contractors

## Overview

### Available Operations

* [list](#list) - Get contractors of a company
* [create](#create) - Create a contractor
* [get](#get) - Get a contractor
* [update](#update) - Update a contractor
* [delete](#delete) - Delete a contractor
* [getOnboardingStatus](#getonboardingstatus) - Get the contractor's onboarding status
* [updateOnboardingStatus](#updateonboardingstatus) - Change the contractor's onboarding status
* [getAddress](#getaddress) - Get a contractor address
* [updateAddress](#updateaddress) - Create or update a contractor's address
* [getV1CompaniesCompanyIdContractorsPaymentDetails](#getv1companiescompanyidcontractorspaymentdetails) - List contractor payment details
* [postV1ContractorsContractorUuidRehire](#postv1contractorscontractoruuidrehire) - Schedule a contractor rehire
* [deleteV1ContractorsContractorUuidRehire](#deletev1contractorscontractoruuidrehire) - Cancel a pending contractor rehire
* [postV1ContractorsContractorUuidTermination](#postv1contractorscontractoruuidtermination) - Schedule a contractor termination
* [deleteV1ContractorsContractorUuidTermination](#deletev1contractorscontractoruuidtermination) - Cancel a pending contractor termination

## list

Get all contractors, active and inactive, individual and business, for a company.

scope: `contractors:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_uuid-contractors" method="get" path="/v1/companies/{company_uuid}/contractors" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyUuidContractorsRequest;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyUuidContractorsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyUuidContractorsRequest req = GetV1CompaniesCompanyUuidContractorsRequest.builder()
                .companyUuid("<id>")
                .build();

        GetV1CompaniesCompanyUuidContractorsResponse res = sdk.contractors().list()
                .request(req)
                .call();

        if (res.contractors().isPresent()) {
            System.out.println(res.contractors().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                             | Type                                                                                                                  | Required                                                                                                              | Description                                                                                                           |
| --------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| `request`                                                                                                             | [GetV1CompaniesCompanyUuidContractorsRequest](../../models/operations/GetV1CompaniesCompanyUuidContractorsRequest.md) | :heavy_check_mark:                                                                                                    | The request object to use for the request.                                                                            |

### Response

**[GetV1CompaniesCompanyUuidContractorsResponse](../../models/operations/GetV1CompaniesCompanyUuidContractorsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## create

Create an individual or business contractor.

scope: `contractors:manage`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_uuid-contractors" method="post" path="/v1/companies/{company_uuid}/contractors" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.ContractorCreateRequestBody;
import com.gusto.embedded_api_v_2025_11_15.models.components.ContractorCreateRequestBodyWageType;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1CompaniesCompanyUuidContractorsHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1CompaniesCompanyUuidContractorsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyUuidContractorsResponse res = sdk.contractors().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyUuidContractorsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyUuid("<id>")
                .contractorCreateRequestBody(ContractorCreateRequestBody.builder()
                    .wageType(ContractorCreateRequestBodyWageType.HOURLY)
                    .startDate("2020-01-11")
                    .hourlyRate("40.0")
                    .build())
                .call();

        if (res.contractor().isPresent()) {
            System.out.println(res.contractor().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompaniesCompanyUuidContractorsHeaderXGustoAPIVersion>](../../models/operations/PostV1CompaniesCompanyUuidContractorsHeaderXGustoAPIVersion.md)                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `contractorCreateRequestBody`                                                                                                                                                                                                | [ContractorCreateRequestBody](../../models/components/ContractorCreateRequestBody.md)                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompaniesCompanyUuidContractorsResponse](../../models/operations/PostV1CompaniesCompanyUuidContractorsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## get

Get a contractor.

scope: `contractors:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-contractors-contractor_uuid" method="get" path="/v1/contractors/{contractor_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1ContractorsContractorUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1ContractorsContractorUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1ContractorsContractorUuidResponse res = sdk.contractors().get()
                .xGustoAPIVersion(GetV1ContractorsContractorUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .contractorUuid("<id>")
                .call();

        if (res.contractor().isPresent()) {
            System.out.println(res.contractor().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1ContractorsContractorUuidHeaderXGustoAPIVersion>](../../models/operations/GetV1ContractorsContractorUuidHeaderXGustoAPIVersion.md)                                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `contractorUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor                                                                                                                                                                                                   |
| `include`                                                                                                                                                                                                                    | List\<[GetV1ContractorsContractorUuidQueryParamInclude](../../models/operations/GetV1ContractorsContractorUuidQueryParamInclude.md)>                                                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Include the requested attribute(s) in each contractor response. Multiple options are comma separated.                                                                                                                        |

### Response

**[GetV1ContractorsContractorUuidResponse](../../models/operations/GetV1ContractorsContractorUuidResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## update

Update a contractor.

> 🚧 Warning
>
> Watch out when changing a contractor's type (when the contractor is finished onboarding). Specifically, changing contractor type can be dangerous since Gusto won't recognize and file two separate 1099s if they simply change from business to individual

scope: `contractors:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-contractors-contractor_uuid" method="put" path="/v1/contractors/{contractor_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.ContractorUpdateRequestBody;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1ContractorsContractorUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1ContractorsContractorUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1ContractorsContractorUuidResponse res = sdk.contractors().update()
                .xGustoAPIVersion(PutV1ContractorsContractorUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .contractorUuid("<id>")
                .contractorUpdateRequestBody(ContractorUpdateRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .startDate("2020-01-11")
                    .hourlyRate("40.0")
                    .build())
                .call();

        if (res.contractor().isPresent()) {
            System.out.println(res.contractor().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1ContractorsContractorUuidHeaderXGustoAPIVersion>](../../models/operations/PutV1ContractorsContractorUuidHeaderXGustoAPIVersion.md)                                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `contractorUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor                                                                                                                                                                                                   |
| `contractorUpdateRequestBody`                                                                                                                                                                                                | [ContractorUpdateRequestBody](../../models/components/ContractorUpdateRequestBody.md)                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1ContractorsContractorUuidResponse](../../models/operations/PutV1ContractorsContractorUuidResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 409, 422                               | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## delete

A contractor can only be deleted when there are no contractor payments.

scope: `contractors:manage`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-contractors-contractor_uuid" method="delete" path="/v1/contractors/{contractor_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.DeleteV1ContractorsContractorUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.DeleteV1ContractorsContractorUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1ContractorsContractorUuidResponse res = sdk.contractors().delete()
                .xGustoAPIVersion(DeleteV1ContractorsContractorUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .contractorUuid("<id>")
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1ContractorsContractorUuidHeaderXGustoAPIVersion>](../../models/operations/DeleteV1ContractorsContractorUuidHeaderXGustoAPIVersion.md)                                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `contractorUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor                                                                                                                                                                                                   |

### Response

**[DeleteV1ContractorsContractorUuidResponse](../../models/operations/DeleteV1ContractorsContractorUuidResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getOnboardingStatus

Retrieves a contractor's onboarding status. The data returned helps inform the required onboarding steps and respective completion status.

## onboarding_status

### Admin-facilitated onboarding
| onboarding_status | Description |
|:------------------|------------:|
| `admin_onboarding_incomplete` | Admin needs to enter basic information about the contractor. |
| `admin_onboarding_review` | All information has been completed and admin needs to confirm onboarding. |
| `onboarding_completed` | Contractor has been fully onboarded and verified. |

### Contractor self-onboarding

| onboarding_status | Description |
| --- | ----------- |
| `admin_onboarding_incomplete` | Admin needs to enter basic information about the contractor. |
| `self_onboarding_not_invited` | Admin has the intention to invite the contractor to self-onboard (e.g., marking a checkbox), but the system has not yet sent the invitation. |
| `self_onboarding_invited` | Contractor has been sent an invitation to self-onboard. |
| `self_onboarding_started` | Contractor has started the self-onboarding process. |
| `self_onboarding_review` | Admin needs to review contractors's entered information and confirm onboarding. |
| `onboarding_completed` | Contractor has been fully onboarded and verified. |

## onboarding_steps

| onboarding_steps | Requirement(s) to be completed |
|:-----------------|-------------------------------:|
| `basic_details` | Add individual contractor's first name, last name, social security number or Business name and EIN depending on the contractor type |
| `add_address` | Add contractor address. |
| `compensation_details` | Add contractor compensation. |
| `payment_details` | (optional) Set up contractor's direct deposit or set to check. |
| `sign_documents` | Contractor forms (e.g., W9) are generated & signed. |
| `file_new_hire_report` | Contractor new hire report is generated. |

scope: `contractors:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-contractors-contractor_uuid-onboarding_status" method="get" path="/v1/contractors/{contractor_uuid}/onboarding_status" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1ContractorsContractorUuidOnboardingStatusHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1ContractorsContractorUuidOnboardingStatusResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1ContractorsContractorUuidOnboardingStatusResponse res = sdk.contractors().getOnboardingStatus()
                .xGustoAPIVersion(GetV1ContractorsContractorUuidOnboardingStatusHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .contractorUuid("<id>")
                .call();

        if (res.contractorOnboardingStatus().isPresent()) {
            System.out.println(res.contractorOnboardingStatus().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1ContractorsContractorUuidOnboardingStatusHeaderXGustoAPIVersion>](../../models/operations/GetV1ContractorsContractorUuidOnboardingStatusHeaderXGustoAPIVersion.md)                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `contractorUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor                                                                                                                                                                                                   |

### Response

**[GetV1ContractorsContractorUuidOnboardingStatusResponse](../../models/operations/GetV1ContractorsContractorUuidOnboardingStatusResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## updateOnboardingStatus

Updates a contractor's onboarding status.

Below is a list of valid onboarding status changes depending on the intended action to be performed on behalf of the contractor.

| Action | current onboarding_status | new onboarding_status |
|:------------------|:------------:|----------:|
| Mark a contractor as self-onboarding | `admin_onboarding_incomplete` | `self_onboarding_not_invited` |
| Invite a contractor to self-onboard | `admin_onboarding_incomplete` or `self_onboarding_not_invited` | `self_onboarding_invited` |
| Cancel a contractor's self-onboarding | `self_onboarding_invited` or `self_onboarding_not_invited` | `admin_onboarding_incomplete` |
| Review a contractor's self-onboarded info | `self_onboarding_started` | `self_onboarding_review` |
| Finish a contractor's onboarding | `admin_onboarding_review` or `self_onboarding_review` | `onboarding_completed` |

scope: `contractors:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-contractors-contractor_uuid-onboarding_status" method="put" path="/v1/contractors/{contractor_uuid}/onboarding_status" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.ContractorOnboardingStatusUpdateRequestBody;
import com.gusto.embedded_api_v_2025_11_15.models.components.ContractorOnboardingStatusUpdateRequestBodyOnboardingStatus;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1ContractorsContractorUuidOnboardingStatusHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1ContractorsContractorUuidOnboardingStatusResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1ContractorsContractorUuidOnboardingStatusResponse res = sdk.contractors().updateOnboardingStatus()
                .xGustoAPIVersion(PutV1ContractorsContractorUuidOnboardingStatusHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .contractorUuid("<id>")
                .contractorOnboardingStatusUpdateRequestBody(ContractorOnboardingStatusUpdateRequestBody.builder()
                    .onboardingStatus(ContractorOnboardingStatusUpdateRequestBodyOnboardingStatus.SELF_ONBOARDING_STARTED)
                    .build())
                .call();

        if (res.contractorOnboardingStatus().isPresent()) {
            System.out.println(res.contractorOnboardingStatus().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1ContractorsContractorUuidOnboardingStatusHeaderXGustoAPIVersion>](../../models/operations/PutV1ContractorsContractorUuidOnboardingStatusHeaderXGustoAPIVersion.md)                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `contractorUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor                                                                                                                                                                                                   |
| `contractorOnboardingStatusUpdateRequestBody`                                                                                                                                                                                | [ContractorOnboardingStatusUpdateRequestBody](../../models/components/ContractorOnboardingStatusUpdateRequestBody.md)                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1ContractorsContractorUuidOnboardingStatusResponse](../../models/operations/PutV1ContractorsContractorUuidOnboardingStatusResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getAddress

The address of a contractor is used to determine certain tax information about them. Addresses are geocoded on create and update to ensure validity.

scope: `contractors:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-contractors-contractor_uuid-address" method="get" path="/v1/contractors/{contractor_uuid}/address" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1ContractorsContractorUuidAddressHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1ContractorsContractorUuidAddressResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1ContractorsContractorUuidAddressResponse res = sdk.contractors().getAddress()
                .xGustoAPIVersion(GetV1ContractorsContractorUuidAddressHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .contractorUuid("<id>")
                .call();

        if (res.contractorAddress().isPresent()) {
            System.out.println(res.contractorAddress().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1ContractorsContractorUuidAddressHeaderXGustoAPIVersion>](../../models/operations/GetV1ContractorsContractorUuidAddressHeaderXGustoAPIVersion.md)                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `contractorUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor                                                                                                                                                                                                   |

### Response

**[GetV1ContractorsContractorUuidAddressResponse](../../models/operations/GetV1ContractorsContractorUuidAddressResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## updateAddress

The address of a contractor is used to determine certain tax information about them. Addresses are geocoded on create and update to ensure validity.

> 🚧 Contractors can only have one address.
>
> When a contractor is created, an address is created for them by default. Updating the address will replace the existing address.

scope: `contractors:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-contractors-contractor_uuid-address" method="put" path="/v1/contractors/{contractor_uuid}/address" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.ContractorAddressUpdateBody;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1ContractorsContractorUuidAddressHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1ContractorsContractorUuidAddressResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1ContractorsContractorUuidAddressResponse res = sdk.contractors().updateAddress()
                .xGustoAPIVersion(PutV1ContractorsContractorUuidAddressHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .contractorUuid("<id>")
                .contractorAddressUpdateBody(ContractorAddressUpdateBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .build())
                .call();

        if (res.contractorAddress().isPresent()) {
            System.out.println(res.contractorAddress().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1ContractorsContractorUuidAddressHeaderXGustoAPIVersion>](../../models/operations/PutV1ContractorsContractorUuidAddressHeaderXGustoAPIVersion.md)                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `contractorUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor                                                                                                                                                                                                   |
| `contractorAddressUpdateBody`                                                                                                                                                                                                | [ContractorAddressUpdateBody](../../models/components/ContractorAddressUpdateBody.md)                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1ContractorsContractorUuidAddressResponse](../../models/operations/PutV1ContractorsContractorUuidAddressResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getV1CompaniesCompanyIdContractorsPaymentDetails

Get payment details for contractors in a company. This endpoint returns a list of all contractors
associated with the specified company, including their payment methods and bank account details
if they are paid via direct deposit.

For contractors paid by direct deposit, the response includes their bank account information
with sensitive data masked for security. The payment details also include information about
how their payments are split if they have multiple bank accounts configured.

For contractors paid by check, only the basic payment method information is returned.

### Response Details
- For direct deposit contractors:
  - Bank account details (masked)
  - Payment splits configuration
  - Routing numbers
  - Account types
- For check payments:
  - Basic payment method designation

### Common Use Cases
- Fetching contractor payment information for payroll processing
- Verifying contractor payment methods
- Reviewing payment split configurations

`encrypted_account_number` is available only with the additional scope `contractor_payment_methods:read:account_numbers`.

scope: `contractor_payment_methods:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_id-contractors-payment_details" method="get" path="/v1/companies/{company_id}/contractors/payment_details" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdContractorsPaymentDetailsHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdContractorsPaymentDetailsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyIdContractorsPaymentDetailsResponse res = sdk.contractors().getV1CompaniesCompanyIdContractorsPaymentDetails()
                .companyId("<id>")
                .xGustoAPIVersion(GetV1CompaniesCompanyIdContractorsPaymentDetailsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .call();

        if (res.contractorPaymentDetailsList().isPresent()) {
            System.out.println(res.contractorPaymentDetailsList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company. This identifies the company whose contractor payment details you want to retrieve.                                                                                                                  |
| `contractorUuid`                                                                                                                                                                                                             | *Optional\<String>*                                                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                                                           | Optional filter to get payment details for a specific contractor. When provided, the response will only include payment details for this contractor.                                                                         |
| `contractorPaymentGroupUuid`                                                                                                                                                                                                 | *Optional\<String>*                                                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                                                           | Optional filter to get payment details for contractors in a specific payment group. When provided, the response will only include payment details for contractors in this group.                                             |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompaniesCompanyIdContractorsPaymentDetailsHeaderXGustoAPIVersion>](../../models/operations/GetV1CompaniesCompanyIdContractorsPaymentDetailsHeaderXGustoAPIVersion.md)                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1CompaniesCompanyIdContractorsPaymentDetailsResponse](../../models/operations/GetV1CompaniesCompanyIdContractorsPaymentDetailsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## postV1ContractorsContractorUuidRehire

## Purpose
Schedules a contractor rehire for a given date. Creates a new employment record for the contractor.

## Prerequisites
Before calling this endpoint:
1. The contractor must be inactive (previously dismissed)
2. The contractor must not already have an upcoming employment

## Related webhooks
- `contractor.reactivated`: Fires when the contractor becomes active again (on or after start_date)

scope: `contractors:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-contractors-contractor_uuid-rehire" method="post" path="/v1/contractors/{contractor_uuid}/rehire" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1ContractorsContractorUuidRehireResponse res = sdk.contractors().postV1ContractorsContractorUuidRehire()
                .contractorUuid("<id>")
                .xGustoAPIVersion(PostV1ContractorsContractorUuidRehireHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .requestBody(PostV1ContractorsContractorUuidRehireRequestBody.builder()
                    .startDate(LocalDate.parse("2025-07-01"))
                    .build())
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `contractorUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor                                                                                                                                                                                                   |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1ContractorsContractorUuidRehireHeaderXGustoAPIVersion>](../../models/operations/PostV1ContractorsContractorUuidRehireHeaderXGustoAPIVersion.md)                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `requestBody`                                                                                                                                                                                                                | [Optional\<PostV1ContractorsContractorUuidRehireRequestBody>](../../models/operations/PostV1ContractorsContractorUuidRehireRequestBody.md)                                                                                   | :heavy_minus_sign:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1ContractorsContractorUuidRehireResponse](../../models/operations/PostV1ContractorsContractorUuidRehireResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |

## deleteV1ContractorsContractorUuidRehire

## Purpose
Cancels a pending contractor rehire. For future-dated rehires, cancellation is available anytime before the date.
For past-dated rehires, cancellation is only available within the 2-day grace period.

## Prerequisites
Before calling this endpoint:
- The contractor must have a pending rehire (upcoming employment)

## Related webhooks
- `contractor.deactivated`: Fires when the contractor returns to inactive state after cancellation

scope: `contractors:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-contractors-contractor_uuid-rehire" method="delete" path="/v1/contractors/{contractor_uuid}/rehire" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.operations.DeleteV1ContractorsContractorUuidRehireHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.DeleteV1ContractorsContractorUuidRehireResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1ContractorsContractorUuidRehireResponse res = sdk.contractors().deleteV1ContractorsContractorUuidRehire()
                .contractorUuid("<id>")
                .xGustoAPIVersion(DeleteV1ContractorsContractorUuidRehireHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `contractorUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor                                                                                                                                                                                                   |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1ContractorsContractorUuidRehireHeaderXGustoAPIVersion>](../../models/operations/DeleteV1ContractorsContractorUuidRehireHeaderXGustoAPIVersion.md)                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[DeleteV1ContractorsContractorUuidRehireResponse](../../models/operations/DeleteV1ContractorsContractorUuidRehireResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |

## postV1ContractorsContractorUuidTermination

## Purpose
Schedules a contractor dismissal for a given date. Supports both immediate (past dates) and future-dated dismissals.

## Prerequisites
Before calling this endpoint:
1. The contractor must be active (no existing pending dismissal)
2. The contractor must have a current employment

## Related webhooks
- `contractor.deactivated`: Fires when the contractor becomes inactive (on or after end_date)

scope: `contractors:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-contractors-contractor_uuid-termination" method="post" path="/v1/contractors/{contractor_uuid}/termination" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1ContractorsContractorUuidTerminationResponse res = sdk.contractors().postV1ContractorsContractorUuidTermination()
                .contractorUuid("<id>")
                .xGustoAPIVersion(PostV1ContractorsContractorUuidTerminationHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .requestBody(PostV1ContractorsContractorUuidTerminationRequestBody.builder()
                    .endDate(LocalDate.parse("2025-06-15"))
                    .build())
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `contractorUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor                                                                                                                                                                                                   |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1ContractorsContractorUuidTerminationHeaderXGustoAPIVersion>](../../models/operations/PostV1ContractorsContractorUuidTerminationHeaderXGustoAPIVersion.md)                                                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `requestBody`                                                                                                                                                                                                                | [Optional\<PostV1ContractorsContractorUuidTerminationRequestBody>](../../models/operations/PostV1ContractorsContractorUuidTerminationRequestBody.md)                                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1ContractorsContractorUuidTerminationResponse](../../models/operations/PostV1ContractorsContractorUuidTerminationResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |

## deleteV1ContractorsContractorUuidTermination

## Purpose
Cancels a pending contractor dismissal. For future-dated dismissals, cancellation is available anytime before the date.
For past-dated dismissals, cancellation is only available within the 2-day grace period.

## Prerequisites
Before calling this endpoint:
- The contractor must have a pending dismissal (scheduled or within the grace period)

## Related webhooks
- `contractor.reactivated`: Fires when the contractor becomes active again after cancellation

scope: `contractors:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-contractors-contractor_uuid-termination" method="delete" path="/v1/contractors/{contractor_uuid}/termination" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.operations.DeleteV1ContractorsContractorUuidTerminationHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.DeleteV1ContractorsContractorUuidTerminationResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1ContractorsContractorUuidTerminationResponse res = sdk.contractors().deleteV1ContractorsContractorUuidTermination()
                .contractorUuid("<id>")
                .xGustoAPIVersion(DeleteV1ContractorsContractorUuidTerminationHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `contractorUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor                                                                                                                                                                                                   |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1ContractorsContractorUuidTerminationHeaderXGustoAPIVersion>](../../models/operations/DeleteV1ContractorsContractorUuidTerminationHeaderXGustoAPIVersion.md)                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[DeleteV1ContractorsContractorUuidTerminationResponse](../../models/operations/DeleteV1ContractorsContractorUuidTerminationResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |