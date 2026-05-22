# Companies

## Overview

### Available Operations

* [createPartnerManaged](#createpartnermanaged) - Create a partner managed company
* [get](#get) - Get a company
* [update](#update) - Update a company
* [migrate](#migrate) - Migrate company to embedded payroll
* [getV1PartnerManagedCompaniesCompanyUuidMigrationReadiness](#getv1partnermanagedcompaniescompanyuuidmigrationreadiness) - Check company migration readiness
* [acceptTermsOfService](#accepttermsofservice) - Accept terms of service for a company user
* [retrieveTermsOfService](#retrievetermsofservice) - Retrieve terms of service status for a company user
* [listAdmins](#listadmins) - Get all the admins at a company
* [createAdmin](#createadmin) - Create an admin for the company
* [getOnboardingStatus](#getonboardingstatus) - Get company onboarding status
* [finishOnboarding](#finishonboarding) - Finish company onboarding
* [getCustomFields](#getcustomfields) - Get the custom fields of a company

## createPartnerManaged

Create a partner managed company. When you successfully call the API, it does the following:
* Creates a new company in Gusto
* Creates a new user using the provided email if the user does not already exist.
* Makes the user the primary payroll administrator of the new company.

In response, you will receive oauth access tokens for the created company.

IMPORTANT: the returned access and refresh tokens are reserved for this company only. They cannot be used to access other companies AND previously granted tokens cannot be used to access this company.

📘 System Access Authentication

This endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)

scope: `partner_managed_companies:manage`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-partner-managed-companies" method="post" path="/v1/partner_managed_companies" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.*;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        PostV1PartnerManagedCompaniesResponse res = sdk.companies().createPartnerManaged()
                .security(PostV1PartnerManagedCompaniesSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .xGustoAPIVersion(PostV1PartnerManagedCompaniesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .partnerManagedCompanyCreateRequest(PartnerManagedCompanyCreateRequest.builder()
                    .user(User.builder()
                        .firstName("Marco")
                        .lastName("Trantow")
                        .email("Jewell_Greenholt72@hotmail.com")
                        .build())
                    .company(PartnerManagedCompanyCreateRequestCompany.builder()
                        .name("<value>")
                        .build())
                    .build())
                .call();

        if (res.partnerManagedCompany().isPresent()) {
            System.out.println(res.partnerManagedCompany().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `security`                                                                                                                                                                                                                   | [com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1PartnerManagedCompaniesSecurity](../../models/operations/PostV1PartnerManagedCompaniesSecurity.md)                                                              | :heavy_check_mark:                                                                                                                                                                                                           | The security requirements to use for the request.                                                                                                                                                                            |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1PartnerManagedCompaniesHeaderXGustoAPIVersion>](../../models/operations/PostV1PartnerManagedCompaniesHeaderXGustoAPIVersion.md)                                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `partnerManagedCompanyCreateRequest`                                                                                                                                                                                         | [PartnerManagedCompanyCreateRequest](../../models/components/PartnerManagedCompanyCreateRequest.md)                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1PartnerManagedCompaniesResponse](../../models/operations/PostV1PartnerManagedCompaniesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## get

Get a company.

The employees:read scope is required to return home_address and non-work locations.
The company_admin:read scope is required to return primary_payroll_admin.
The signatories:read scope is required to return primary_signatory.

scope: `companies:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies" method="get" path="/v1/companies/{company_id}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesResponse res = sdk.companies().get()
                .companyId("<id>")
                .xGustoAPIVersion(GetV1CompaniesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .call();

        if (res.company().isPresent()) {
            System.out.println(res.company().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompaniesHeaderXGustoAPIVersion>](../../models/operations/GetV1CompaniesHeaderXGustoAPIVersion.md)                                                                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1CompaniesResponse](../../models/operations/GetV1CompaniesResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## update

Update a company.

scope: `companies:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-companies" method="put" path="/v1/companies/{company_id}" -->
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

        PutV1CompaniesResponse res = sdk.companies().update()
                .companyId("<id>")
                .xGustoAPIVersion(PutV1CompaniesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .requestBody(PutV1CompaniesRequestBody.builder()
                    .contractorOnly(true)
                    .build())
                .call();

        if (res.company().isPresent()) {
            System.out.println(res.company().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1CompaniesHeaderXGustoAPIVersion>](../../models/operations/PutV1CompaniesHeaderXGustoAPIVersion.md)                                                                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `requestBody`                                                                                                                                                                                                                | [PutV1CompaniesRequestBody](../../models/operations/PutV1CompaniesRequestBody.md)                                                                                                                                            | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1CompaniesResponse](../../models/operations/PutV1CompaniesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## migrate

Migrate an existing Gusto customer to your embedded payroll product.

### Prerequisites
Before calling this endpoint:
1. The customer must connect their Gusto account to your application using [OAuth2](doc:oauth2)
2. The customer must view and [accept the Embedded Payroll Terms of Service](ref:post-partner-managed-companies-company_uuid-accept_terms_of_service)

### Related guides
- [Migrate an existing company](doc:migrate-existing-company)

scope: `partner_managed_companies:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-partner-managed-companies-company-uuid-migrate" method="put" path="/v1/partner_managed_companies/{company_uuid}/migrate" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.PartnerManagedCompanyMigrateRequest;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1PartnerManagedCompaniesCompanyUuidMigrateHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1PartnerManagedCompaniesCompanyUuidMigrateResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1PartnerManagedCompaniesCompanyUuidMigrateResponse res = sdk.companies().migrate()
                .companyUuid("<id>")
                .xGustoAPIVersion(PutV1PartnerManagedCompaniesCompanyUuidMigrateHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .partnerManagedCompanyMigrateRequest(PartnerManagedCompanyMigrateRequest.builder()
                    .email("Janice18@gmail.com")
                    .build())
                .call();

        if (res.partnerManagedCompanyMigrateResponse().isPresent()) {
            System.out.println(res.partnerManagedCompanyMigrateResponse().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1PartnerManagedCompaniesCompanyUuidMigrateHeaderXGustoAPIVersion>](../../models/operations/PutV1PartnerManagedCompaniesCompanyUuidMigrateHeaderXGustoAPIVersion.md)                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `partnerManagedCompanyMigrateRequest`                                                                                                                                                                                        | [PartnerManagedCompanyMigrateRequest](../../models/components/PartnerManagedCompanyMigrateRequest.md)                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1PartnerManagedCompaniesCompanyUuidMigrateResponse](../../models/operations/PutV1PartnerManagedCompaniesCompanyUuidMigrateResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getV1PartnerManagedCompaniesCompanyUuidMigrationReadiness

Check if an existing Gusto customer is ready to be migrated to embedded payroll. This endpoint returns blockers and warnings associated with migrating the company and is recommended to be called before attempting to migrate a company.

scope: `partner_managed_companies:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-partner-managed-companies-company-uuid-migration_readiness" method="get" path="/v1/partner_managed_companies/{company_uuid}/migration_readiness" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1PartnerManagedCompaniesCompanyUuidMigrationReadinessHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1PartnerManagedCompaniesCompanyUuidMigrationReadinessResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1PartnerManagedCompaniesCompanyUuidMigrationReadinessResponse res = sdk.companies().getV1PartnerManagedCompaniesCompanyUuidMigrationReadiness()
                .companyUuid("<id>")
                .xGustoAPIVersion(GetV1PartnerManagedCompaniesCompanyUuidMigrationReadinessHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .call();

        if (res.partnerManagedCompanyMigrationReadinessResponse().isPresent()) {
            System.out.println(res.partnerManagedCompanyMigrationReadinessResponse().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1PartnerManagedCompaniesCompanyUuidMigrationReadinessHeaderXGustoAPIVersion>](../../models/operations/GetV1PartnerManagedCompaniesCompanyUuidMigrationReadinessHeaderXGustoAPIVersion.md)                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1PartnerManagedCompaniesCompanyUuidMigrationReadinessResponse](../../models/operations/GetV1PartnerManagedCompaniesCompanyUuidMigrationReadinessResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## acceptTermsOfService

Accept the Gusto Embedded Payroll's [Terms of Service](https://flows.gusto.com/terms).
The user must have a role in the company in order to accept the Terms of Service.

scope: `terms_of_services:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-partner-managed-companies-company_uuid-accept_terms_of_service" method="post" path="/v1/partner_managed_companies/{company_uuid}/accept_terms_of_service" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.PartnerManagedCompanyAcceptTermsOfServiceRequest;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostPartnerManagedCompaniesCompanyUuidAcceptTermsOfServiceHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostPartnerManagedCompaniesCompanyUuidAcceptTermsOfServiceResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostPartnerManagedCompaniesCompanyUuidAcceptTermsOfServiceResponse res = sdk.companies().acceptTermsOfService()
                .companyUuid("<id>")
                .xGustoAPIVersion(PostPartnerManagedCompaniesCompanyUuidAcceptTermsOfServiceHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .partnerManagedCompanyAcceptTermsOfServiceRequest(PartnerManagedCompanyAcceptTermsOfServiceRequest.builder()
                    .email("Tabitha59@hotmail.com")
                    .ipAddress("dad9:5ede:cdbf:8dae:abe7:3cac:a2bf:2c26")
                    .externalUserId("<id>")
                    .build())
                .call();

        if (res.partnerManagedCompanyTermsOfServiceResponse().isPresent()) {
            System.out.println(res.partnerManagedCompanyTermsOfServiceResponse().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostPartnerManagedCompaniesCompanyUuidAcceptTermsOfServiceHeaderXGustoAPIVersion>](../../models/operations/PostPartnerManagedCompaniesCompanyUuidAcceptTermsOfServiceHeaderXGustoAPIVersion.md)                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `partnerManagedCompanyAcceptTermsOfServiceRequest`                                                                                                                                                                           | [PartnerManagedCompanyAcceptTermsOfServiceRequest](../../models/components/PartnerManagedCompanyAcceptTermsOfServiceRequest.md)                                                                                              | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostPartnerManagedCompaniesCompanyUuidAcceptTermsOfServiceResponse](../../models/operations/PostPartnerManagedCompaniesCompanyUuidAcceptTermsOfServiceResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## retrieveTermsOfService

Retrieve the user acceptance status of the Gusto Embedded Payroll's [Terms of Service](https://flows.gusto.com/terms).

scope: `terms_of_services:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-partner-managed-companies-company_uuid-retrieve_terms_of_service" method="post" path="/v1/partner_managed_companies/{company_uuid}/retrieve_terms_of_service" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.PartnerManagedCompanyRetrieveTermsOfServiceRequest;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostPartnerManagedCompaniesCompanyUuidRetrieveTermsOfServiceHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostPartnerManagedCompaniesCompanyUuidRetrieveTermsOfServiceResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostPartnerManagedCompaniesCompanyUuidRetrieveTermsOfServiceResponse res = sdk.companies().retrieveTermsOfService()
                .companyUuid("<id>")
                .xGustoAPIVersion(PostPartnerManagedCompaniesCompanyUuidRetrieveTermsOfServiceHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .partnerManagedCompanyRetrieveTermsOfServiceRequest(PartnerManagedCompanyRetrieveTermsOfServiceRequest.builder()
                    .email("Laverne_Raynor-Ziemann@yahoo.com")
                    .build())
                .call();

        if (res.partnerManagedCompanyTermsOfServiceResponse().isPresent()) {
            System.out.println(res.partnerManagedCompanyTermsOfServiceResponse().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostPartnerManagedCompaniesCompanyUuidRetrieveTermsOfServiceHeaderXGustoAPIVersion>](../../models/operations/PostPartnerManagedCompaniesCompanyUuidRetrieveTermsOfServiceHeaderXGustoAPIVersion.md)               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `partnerManagedCompanyRetrieveTermsOfServiceRequest`                                                                                                                                                                         | [PartnerManagedCompanyRetrieveTermsOfServiceRequest](../../models/components/PartnerManagedCompanyRetrieveTermsOfServiceRequest.md)                                                                                          | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostPartnerManagedCompaniesCompanyUuidRetrieveTermsOfServiceResponse](../../models/operations/PostPartnerManagedCompaniesCompanyUuidRetrieveTermsOfServiceResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## listAdmins

Returns a list of all the admins at a company

scope: `company_admin:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_id-admins" method="get" path="/v1/companies/{company_id}/admins" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdAdminsHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdAdminsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyIdAdminsResponse res = sdk.companies().listAdmins()
                .xGustoAPIVersion(GetV1CompaniesCompanyIdAdminsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyId("<id>")
                .call();

        if (res.admins().isPresent()) {
            System.out.println(res.admins().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompaniesCompanyIdAdminsHeaderXGustoAPIVersion>](../../models/operations/GetV1CompaniesCompanyIdAdminsHeaderXGustoAPIVersion.md)                                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `page`                                                                                                                                                                                                                       | *Optional\<Long>*                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                           | The page that is requested. When unspecified, will load all objects unless endpoint forces pagination.                                                                                                                       |
| `per`                                                                                                                                                                                                                        | *Optional\<Long>*                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                           | Number of objects per page. For majority of endpoints will default to 25                                                                                                                                                     |

### Response

**[GetV1CompaniesCompanyIdAdminsResponse](../../models/operations/GetV1CompaniesCompanyIdAdminsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## createAdmin

Creates a new admin for a company.
If the email matches an existing user, this will create an admin account for the current user. Otherwise, this will create a new user.

scope: `company_admin:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-admins" method="post" path="/v1/companies/{company_id}/admins" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.AdminCreateRequest;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1CompaniesCompanyIdAdminsHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1CompaniesCompanyIdAdminsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyIdAdminsResponse res = sdk.companies().createAdmin()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdAdminsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyId("<id>")
                .adminCreateRequest(AdminCreateRequest.builder()
                    .firstName("John")
                    .lastName("Smith")
                    .email("jsmith99@gmail.com")
                    .build())
                .call();

        if (res.admin().isPresent()) {
            System.out.println(res.admin().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompaniesCompanyIdAdminsHeaderXGustoAPIVersion>](../../models/operations/PostV1CompaniesCompanyIdAdminsHeaderXGustoAPIVersion.md)                                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `adminCreateRequest`                                                                                                                                                                                                         | [AdminCreateRequest](../../models/components/AdminCreateRequest.md)                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompaniesCompanyIdAdminsResponse](../../models/operations/PostV1CompaniesCompanyIdAdminsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getOnboardingStatus

Retrieves a company's onboarding status, including whether onboarding is complete and the list of
required onboarding steps with their respective completion state.

scope: `company_onboarding_status:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-company-onboarding-status" method="get" path="/v1/companies/{company_uuid}/onboarding_status" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompanyOnboardingStatusHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompanyOnboardingStatusResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompanyOnboardingStatusResponse res = sdk.companies().getOnboardingStatus()
                .companyUuid("7b1d0df1-6403-4a06-8768-c1dd7d24d27a")
                .additionalSteps("external_payroll")
                .xGustoAPIVersion(GetV1CompanyOnboardingStatusHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .call();

        if (res.companyOnboardingStatus().isPresent()) {
            System.out.println(res.companyOnboardingStatus().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  | Example                                                                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      | 7b1d0df1-6403-4a06-8768-c1dd7d24d27a                                                                                                                                                                                         |
| `additionalSteps`                                                                                                                                                                                                            | *Optional\<String>*                                                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                                                           | Comma-delimited string of additional onboarding steps to include. Currently only supports the value "external_payroll".                                                                                                      | external_payroll                                                                                                                                                                                                             |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompanyOnboardingStatusHeaderXGustoAPIVersion>](../../models/operations/GetV1CompanyOnboardingStatusHeaderXGustoAPIVersion.md)                                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |                                                                                                                                                                                                                              |

### Response

**[GetV1CompanyOnboardingStatusResponse](../../models/operations/GetV1CompanyOnboardingStatusResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## finishOnboarding

Finalize a company's onboarding process.

### Approve a company in demo

After a company is finished onboarding, Gusto requires an additional step to review and approve that company.
The company onboarding status is "onboarding_completed": false, until the API call is made to finish company
onboarding. In production environments, this step is required for risk-analysis purposes.

We provide the endpoint `PUT '/v1/companies/{company_uuid}/approve'` to facilitate company approvals in the demo environment.

```shell
PUT '/v1/companies/89771af8-b964-472e-8064-554dfbcb56d9/approve'

# Response: Company object, with company_status: 'Approved'
```

scope: `companies:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-company-finish-onboarding" method="put" path="/v1/companies/{company_uuid}/finish_onboarding" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompanyFinishOnboardingHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompanyFinishOnboardingResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompanyFinishOnboardingResponse res = sdk.companies().finishOnboarding()
                .companyUuid("7b1d0df1-6403-4a06-8768-c1dd7d24d27a")
                .xGustoAPIVersion(GetV1CompanyFinishOnboardingHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .call();

        if (res.companyOnboardingStatus().isPresent()) {
            System.out.println(res.companyOnboardingStatus().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  | Example                                                                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      | 7b1d0df1-6403-4a06-8768-c1dd7d24d27a                                                                                                                                                                                         |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompanyFinishOnboardingHeaderXGustoAPIVersion>](../../models/operations/GetV1CompanyFinishOnboardingHeaderXGustoAPIVersion.md)                                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |                                                                                                                                                                                                                              |

### Response

**[GetV1CompanyFinishOnboardingResponse](../../models/operations/GetV1CompanyFinishOnboardingResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getCustomFields

Returns a list of the custom fields of the company. Useful when you need to know the schema of custom fields for an entire company.

scope: `companies:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_id-custom_fields" method="get" path="/v1/companies/{company_id}/custom_fields" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdCustomFieldsHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdCustomFieldsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyIdCustomFieldsResponse res = sdk.companies().getCustomFields()
                .xGustoAPIVersion(GetV1CompaniesCompanyIdCustomFieldsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyId("<id>")
                .call();

        if (res.companyCustomFieldList().isPresent()) {
            System.out.println(res.companyCustomFieldList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompaniesCompanyIdCustomFieldsHeaderXGustoAPIVersion>](../../models/operations/GetV1CompaniesCompanyIdCustomFieldsHeaderXGustoAPIVersion.md)                                                                 | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `page`                                                                                                                                                                                                                       | *Optional\<Long>*                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                           | The page that is requested. When unspecified, will load all objects unless endpoint forces pagination.                                                                                                                       |
| `per`                                                                                                                                                                                                                        | *Optional\<Long>*                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                           | Number of objects per page. For majority of endpoints will default to 25                                                                                                                                                     |

### Response

**[GetV1CompaniesCompanyIdCustomFieldsResponse](../../models/operations/GetV1CompaniesCompanyIdCustomFieldsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |