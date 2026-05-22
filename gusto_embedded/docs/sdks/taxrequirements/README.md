# TaxRequirements

## Overview

### Available Operations

* [get](#get) - Get tax requirements for a state
* [updateState](#updatestate) - Update tax requirements for a state
* [getAll](#getall) - Get all tax requirements for a company

## get

Retrieves the detailed tax requirements for a specific state. The response includes requirement sets grouped by
category (e.g., registrations, tax rates, deposit schedules), each containing individual requirements with their
current values, labels, and metadata describing the expected input format.

Use this to build dynamic UIs for tax setup or to read the current tax configuration for a state.

scope: `company_tax_requirements:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_uuid-tax_requirements-state" method="get" path="/v1/companies/{company_uuid}/tax_requirements/{state}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyUuidTaxRequirementsStateHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyUuidTaxRequirementsStateResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyUuidTaxRequirementsStateResponse res = sdk.taxRequirements().get()
                .companyUuid("<id>")
                .state("CA")
                .xGustoAPIVersion(GetV1CompaniesCompanyUuidTaxRequirementsStateHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.taxRequirementsState().isPresent()) {
            System.out.println(res.taxRequirementsState().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  | Example                                                                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |                                                                                                                                                                                                                              |
| `state`                                                                                                                                                                                                                      | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The two-letter state abbreviation                                                                                                                                                                                            | CA                                                                                                                                                                                                                           |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompaniesCompanyUuidTaxRequirementsStateHeaderXGustoAPIVersion>](../../models/operations/GetV1CompaniesCompanyUuidTaxRequirementsStateHeaderXGustoAPIVersion.md)                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |                                                                                                                                                                                                                              |
| `scheduling`                                                                                                                                                                                                                 | *Optional\<Boolean>*                                                                                                                                                                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | When true, return "new" requirement sets with valid `effective_from` dates that are available to save new effective-dated values.                                                                                            |                                                                                                                                                                                                                              |

### Response

**[GetV1CompaniesCompanyUuidTaxRequirementsStateResponse](../../models/operations/GetV1CompaniesCompanyUuidTaxRequirementsStateResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## updateState

Updates the tax requirement answers for a specific state. Submit answers to the requirement questions returned
by [GET /v1/companies/{company_uuid}/tax_requirements/{state}](ref:get-v1-companies-company_uuid-tax_requirements-state).

### Prerequisites

1. Retrieve current requirements via [GET /v1/companies/{company_uuid}/tax_requirements/{state}](ref:get-v1-companies-company_uuid-tax_requirements-state)
2. Ensure that each requirement set that you're updating includes the correct `key`, `state`, and `effective_from` values from the GET response

scope: `company_tax_requirements:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_uuid-tax_requirements-state" method="put" path="/v1/companies/{company_uuid}/tax_requirements/{state}" example="Basic" -->
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

        PutV1CompaniesCompanyUuidTaxRequirementsStateResponse res = sdk.taxRequirements().updateState()
                .companyUuid("<id>")
                .state("West Virginia")
                .xGustoAPIVersion(PutV1CompaniesCompanyUuidTaxRequirementsStateHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PutV1CompaniesCompanyUuidTaxRequirementsStateRequestBody.builder()
                    .build())
                .call();

        // handle response
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_uuid-tax_requirements-state" method="put" path="/v1/companies/{company_uuid}/tax_requirements/{state}" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.*;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;
import java.util.List;
import org.openapitools.jackson.nullable.JsonNullable;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompaniesCompanyUuidTaxRequirementsStateResponse res = sdk.taxRequirements().updateState()
                .companyUuid("<id>")
                .state("Tennessee")
                .xGustoAPIVersion(PutV1CompaniesCompanyUuidTaxRequirementsStateHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PutV1CompaniesCompanyUuidTaxRequirementsStateRequestBody.builder()
                    .requirementSets(List.of(
                        TaxRequirementSetUpdate.builder()
                            .key("registrations")
                            .state("GA")
                            .effectiveFrom(JsonNullable.of(null))
                            .requirements(List.of(
                                Requirements.builder()
                                    .key("71653ec0-00b5-4c66-a58b-22ecf21704c5")
                                    .value(TaxRequirementsValue.of("1233214-AB"))
                                    .build(),
                                Requirements.builder()
                                    .key("6c0911ab-5860-412e-bdef-6437cd881df5")
                                    .value(TaxRequirementsValue.of("474747-22"))
                                    .build()))
                            .build(),
                        TaxRequirementSetUpdate.builder()
                            .key("taxrates")
                            .state("GA")
                            .effectiveFrom("2022-01-01")
                            .requirements(List.of(
                                Requirements.builder()
                                    .key("e0ac2284-8d30-4100-ae23-f85f9574868b")
                                    .value(TaxRequirementsValue.of("0.05"))
                                    .build()))
                            .build(),
                        TaxRequirementSetUpdate.builder()
                            .key("depositschedules")
                            .state("GA")
                            .effectiveFrom("2022-01-01")
                            .requirements(List.of(
                                Requirements.builder()
                                    .key("6ddfcbeb-94d3-4003-bfc2-8c6e1ca9f70c")
                                    .value(TaxRequirementsValue.of("Semi-weekly"))
                                    .build()))
                            .build()))
                    .build())
                .call();

        // handle response
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_uuid-tax_requirements-state" method="put" path="/v1/companies/{company_uuid}/tax_requirements/{state}" example="Nested" -->
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

        PutV1CompaniesCompanyUuidTaxRequirementsStateResponse res = sdk.taxRequirements().updateState()
                .companyUuid("<id>")
                .state("Maryland")
                .xGustoAPIVersion(PutV1CompaniesCompanyUuidTaxRequirementsStateHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PutV1CompaniesCompanyUuidTaxRequirementsStateRequestBody.builder()
                    .build())
                .call();

        // handle response
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_uuid-tax_requirements-state" method="put" path="/v1/companies/{company_uuid}/tax_requirements/{state}" example="Resource" -->
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

        PutV1CompaniesCompanyUuidTaxRequirementsStateResponse res = sdk.taxRequirements().updateState()
                .companyUuid("<id>")
                .state("Vermont")
                .xGustoAPIVersion(PutV1CompaniesCompanyUuidTaxRequirementsStateHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PutV1CompaniesCompanyUuidTaxRequirementsStateRequestBody.builder()
                    .build())
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  | Example                                                                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |                                                                                                                                                                                                                              |
| `state`                                                                                                                                                                                                                      | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The two-letter state abbreviation                                                                                                                                                                                            | CA                                                                                                                                                                                                                           |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1CompaniesCompanyUuidTaxRequirementsStateHeaderXGustoAPIVersion>](../../models/operations/PutV1CompaniesCompanyUuidTaxRequirementsStateHeaderXGustoAPIVersion.md)                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |                                                                                                                                                                                                                              |
| `requestBody`                                                                                                                                                                                                                | [PutV1CompaniesCompanyUuidTaxRequirementsStateRequestBody](../../models/operations/PutV1CompaniesCompanyUuidTaxRequirementsStateRequestBody.md)                                                                              | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |                                                                                                                                                                                                                              |

### Response

**[PutV1CompaniesCompanyUuidTaxRequirementsStateResponse](../../models/operations/PutV1CompaniesCompanyUuidTaxRequirementsStateResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getAll

Retrieves all states for which a company has tax requirements, along with a boolean indicating whether tax setup
is complete for each state. Use this to determine which states still need tax setup during company onboarding.

scope: `company_tax_requirements:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_uuid-tax_requirements" method="get" path="/v1/companies/{company_uuid}/tax_requirements" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyUuidTaxRequirementsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyUuidTaxRequirementsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyUuidTaxRequirementsResponse res = sdk.taxRequirements().getAll()
                .companyUuid("<id>")
                .xGustoAPIVersion(GetV1CompaniesCompanyUuidTaxRequirementsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.taxRequirementStatesList().isPresent()) {
            System.out.println(res.taxRequirementStatesList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompaniesCompanyUuidTaxRequirementsHeaderXGustoAPIVersion>](../../models/operations/GetV1CompaniesCompanyUuidTaxRequirementsHeaderXGustoAPIVersion.md)                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1CompaniesCompanyUuidTaxRequirementsResponse](../../models/operations/GetV1CompaniesCompanyUuidTaxRequirementsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |