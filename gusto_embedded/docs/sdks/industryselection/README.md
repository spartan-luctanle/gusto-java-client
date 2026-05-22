# IndustrySelection

## Overview

### Available Operations

* [get](#get) - Get a company industry selection
* [update](#update) - Update a company industry selection

## get

Returns the industry classification for a company, including NAICS code, SIC codes, and industry title.

scope: `companies:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-company-industry" method="get" path="/v1/companies/{company_id}/industry_selection" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1CompanyIndustryHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1CompanyIndustryResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompanyIndustryResponse res = sdk.industrySelection().get()
                .companyId("<id>")
                .xGustoAPIVersion(GetV1CompanyIndustryHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.industry().isPresent()) {
            System.out.println(res.industry().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompanyIndustryHeaderXGustoAPIVersion>](../../models/operations/GetV1CompanyIndustryHeaderXGustoAPIVersion.md)                                                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1CompanyIndustryResponse](../../models/operations/GetV1CompanyIndustryResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## update

Update the industry classification for a company by passing in a [NAICS code](https://www.naics.com).

Optionally provide an industry title and [SIC codes](https://siccode.com/). If you do not provide SIC codes,
we will use the NAICS code to perform an internal lookup.

Our UI leverages [Middesk API](https://docs.middesk.com/reference/introduction) to determine industry
classification codes.

scope: `companies:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-company-industry" method="put" path="/v1/companies/{company_id}/industry_selection" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyIndustrySelectionRequiredBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompanyIndustryHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompanyIndustryResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompanyIndustryResponse res = sdk.industrySelection().update()
                .companyId("<id>")
                .xGustoAPIVersion(PutV1CompanyIndustryHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyIndustrySelectionRequiredBody(CompanyIndustrySelectionRequiredBody.builder()
                    .naicsCode("<value>")
                    .build())
                .call();

        if (res.industry().isPresent()) {
            System.out.println(res.industry().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-company-industry" method="put" path="/v1/companies/{company_id}/industry_selection" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyIndustrySelectionRequiredBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompanyIndustryHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompanyIndustryResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompanyIndustryResponse res = sdk.industrySelection().update()
                .companyId("<id>")
                .xGustoAPIVersion(PutV1CompanyIndustryHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyIndustrySelectionRequiredBody(CompanyIndustrySelectionRequiredBody.builder()
                    .naicsCode("611420")
                    .title("Computer Training")
                    .sicCodes(List.of(
                        "8243"))
                    .build())
                .call();

        if (res.industry().isPresent()) {
            System.out.println(res.industry().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-company-industry" method="put" path="/v1/companies/{company_id}/industry_selection" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyIndustrySelectionRequiredBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompanyIndustryHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompanyIndustryResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompanyIndustryResponse res = sdk.industrySelection().update()
                .companyId("<id>")
                .xGustoAPIVersion(PutV1CompanyIndustryHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyIndustrySelectionRequiredBody(CompanyIndustrySelectionRequiredBody.builder()
                    .naicsCode("<value>")
                    .build())
                .call();

        if (res.industry().isPresent()) {
            System.out.println(res.industry().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-company-industry" method="put" path="/v1/companies/{company_id}/industry_selection" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyIndustrySelectionRequiredBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompanyIndustryHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompanyIndustryResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompanyIndustryResponse res = sdk.industrySelection().update()
                .companyId("<id>")
                .xGustoAPIVersion(PutV1CompanyIndustryHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyIndustrySelectionRequiredBody(CompanyIndustrySelectionRequiredBody.builder()
                    .naicsCode("<value>")
                    .build())
                .call();

        if (res.industry().isPresent()) {
            System.out.println(res.industry().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1CompanyIndustryHeaderXGustoAPIVersion>](../../models/operations/PutV1CompanyIndustryHeaderXGustoAPIVersion.md)                                                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyIndustrySelectionRequiredBody`                                                                                                                                                                                       | [CompanyIndustrySelectionRequiredBody](../../models/components/CompanyIndustrySelectionRequiredBody.md)                                                                                                                      | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1CompanyIndustryResponse](../../models/operations/PutV1CompanyIndustryResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |