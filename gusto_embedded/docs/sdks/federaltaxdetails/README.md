# FederalTaxDetails

## Overview

### Available Operations

* [get](#get) - Get a company's federal tax details
* [update](#update) - Update a company's federal tax details

## get

Retrieves a company's federal tax details including EIN verification status, tax payer type, filing form, and other federal tax configuration.

scope: `company_federal_taxes:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_id-federal_tax_details" method="get" path="/v1/companies/{company_id}/federal_tax_details" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyIdFederalTaxDetailsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyIdFederalTaxDetailsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyIdFederalTaxDetailsResponse res = sdk.federalTaxDetails().get()
                .companyId("<id>")
                .xGustoAPIVersion(GetV1CompaniesCompanyIdFederalTaxDetailsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.federalTaxDetails().isPresent()) {
            System.out.println(res.federalTaxDetails().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  | Example                                                                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      | 7b1d0df1-6403-4a06-8768-c1dd7d24d27a                                                                                                                                                                                         |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompaniesCompanyIdFederalTaxDetailsHeaderXGustoAPIVersion>](../../models/operations/GetV1CompaniesCompanyIdFederalTaxDetailsHeaderXGustoAPIVersion.md)                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |                                                                                                                                                                                                                              |

### Response

**[GetV1CompaniesCompanyIdFederalTaxDetailsResponse](../../models/operations/GetV1CompaniesCompanyIdFederalTaxDetailsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## update

Updates a company's federal tax details including EIN, legal name, tax payer type, filing form, and S-Corp
taxation status. This information is required to onboard a company for use with Gusto Embedded Payroll.

### Prerequisites
Before calling this endpoint, retrieve the current federal tax details and `version` via [GET /v1/companies/{company_id}/federal_tax_details](ref:get-v1-companies-company_id-federal_tax_details)

### Webhooks
- `company.updated`: Fires when federal tax details for a company are successfully updated

**Setup:** [POST /v1/webhook_subscriptions](ref:post-v1-webhook-subscription) with `subscription_types`: `["Company"]`

scope: `company_federal_taxes:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_id-federal_tax_details" method="put" path="/v1/companies/{company_id}/federal_tax_details" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.FederalTaxDetailsUpdate;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyIdFederalTaxDetailsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyIdFederalTaxDetailsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompaniesCompanyIdFederalTaxDetailsResponse res = sdk.federalTaxDetails().update()
                .companyId("<id>")
                .xGustoAPIVersion(PutV1CompaniesCompanyIdFederalTaxDetailsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .federalTaxDetailsUpdate(FederalTaxDetailsUpdate.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.federalTaxDetails().isPresent()) {
            System.out.println(res.federalTaxDetails().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_id-federal_tax_details" method="put" path="/v1/companies/{company_id}/federal_tax_details" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.*;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyIdFederalTaxDetailsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyIdFederalTaxDetailsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompaniesCompanyIdFederalTaxDetailsResponse res = sdk.federalTaxDetails().update()
                .companyId("<id>")
                .xGustoAPIVersion(PutV1CompaniesCompanyIdFederalTaxDetailsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .federalTaxDetailsUpdate(FederalTaxDetailsUpdate.builder()
                    .version("6cb95e00540706ca48d4577b3c839fbe")
                    .legalName("Acme Corp.")
                    .taxPayerType(FederalTaxDetailsUpdateTaxPayerType.LLP)
                    .filingForm(FederalTaxDetailsUpdateFilingForm.NINE_HUNDRED_AND_FORTY_FOUR)
                    .taxableAsScorp(false)
                    .build())
                .call();

        if (res.federalTaxDetails().isPresent()) {
            System.out.println(res.federalTaxDetails().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_id-federal_tax_details" method="put" path="/v1/companies/{company_id}/federal_tax_details" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.FederalTaxDetailsUpdate;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyIdFederalTaxDetailsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyIdFederalTaxDetailsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompaniesCompanyIdFederalTaxDetailsResponse res = sdk.federalTaxDetails().update()
                .companyId("<id>")
                .xGustoAPIVersion(PutV1CompaniesCompanyIdFederalTaxDetailsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .federalTaxDetailsUpdate(FederalTaxDetailsUpdate.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.federalTaxDetails().isPresent()) {
            System.out.println(res.federalTaxDetails().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_id-federal_tax_details" method="put" path="/v1/companies/{company_id}/federal_tax_details" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.FederalTaxDetailsUpdate;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyIdFederalTaxDetailsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyIdFederalTaxDetailsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompaniesCompanyIdFederalTaxDetailsResponse res = sdk.federalTaxDetails().update()
                .companyId("<id>")
                .xGustoAPIVersion(PutV1CompaniesCompanyIdFederalTaxDetailsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .federalTaxDetailsUpdate(FederalTaxDetailsUpdate.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.federalTaxDetails().isPresent()) {
            System.out.println(res.federalTaxDetails().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  | Example                                                                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      | 7b1d0df1-6403-4a06-8768-c1dd7d24d27a                                                                                                                                                                                         |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1CompaniesCompanyIdFederalTaxDetailsHeaderXGustoAPIVersion>](../../models/operations/PutV1CompaniesCompanyIdFederalTaxDetailsHeaderXGustoAPIVersion.md)                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |                                                                                                                                                                                                                              |
| `federalTaxDetailsUpdate`                                                                                                                                                                                                    | [FederalTaxDetailsUpdate](../../models/components/FederalTaxDetailsUpdate.md)                                                                                                                                                | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |                                                                                                                                                                                                                              |

### Response

**[PutV1CompaniesCompanyIdFederalTaxDetailsResponse](../../models/operations/PutV1CompaniesCompanyIdFederalTaxDetailsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 409, 422                               | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |