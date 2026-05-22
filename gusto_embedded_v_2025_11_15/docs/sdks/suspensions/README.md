# Companies.Suspensions

## Overview

### Available Operations

* [get](#get) - Get suspensions for this company
* [suspend](#suspend) - Suspend a company's account

## get

Get existing suspension records for this company. A company may have multiple suspension records if they have suspended their Gusto account more than once.

>📘 To check if company is already suspended
>
> To determine if a company is _currently_ suspended, use the `is_suspended` and `company_status` fields in the [Get a company](https://docs.gusto.com/embedded-payroll/reference/get-v1-companies) endpoint.

scope: `company_suspensions:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-companies-company_uuid-suspensions" method="get" path="/v1/companies/{company_uuid}/suspensions" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetCompaniesCompanyUuidSuspensionsHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetCompaniesCompanyUuidSuspensionsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetCompaniesCompanyUuidSuspensionsResponse res = sdk.companies().suspensions().get()
                .xGustoAPIVersion(GetCompaniesCompanyUuidSuspensionsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyUuid("<id>")
                .call();

        if (res.companySuspensionList().isPresent()) {
            System.out.println(res.companySuspensionList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetCompaniesCompanyUuidSuspensionsHeaderXGustoAPIVersion>](../../models/operations/GetCompaniesCompanyUuidSuspensionsHeaderXGustoAPIVersion.md)                                                                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |

### Response

**[GetCompaniesCompanyUuidSuspensionsResponse](../../models/operations/GetCompaniesCompanyUuidSuspensionsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## suspend

Use this endpoint to suspend a company. After suspension, company will no longer be able to run payroll but will retain access to their information, such as retrieving employee info or retrieving past payrolls.

scope: `company_suspensions:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-companies-company_uuid-suspensions" method="post" path="/v1/companies/{company_uuid}/suspensions" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostCompaniesCompanyUuidSuspensionsResponse res = sdk.companies().suspensions().suspend()
                .xGustoAPIVersion(PostCompaniesCompanyUuidSuspensionsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyUuid("<id>")
                .requestBody(PostCompaniesCompanyUuidSuspensionsRequestBody.builder()
                    .fileQuarterlyForms(true)
                    .fileYearlyForms(false)
                    .reconcileTaxMethod(ReconcileTaxMethod.PAY_TAXES)
                    .reason(Reason.ACQUIRED)
                    .build())
                .call();

        if (res.companySuspension().isPresent()) {
            System.out.println(res.companySuspension().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostCompaniesCompanyUuidSuspensionsHeaderXGustoAPIVersion>](../../models/operations/PostCompaniesCompanyUuidSuspensionsHeaderXGustoAPIVersion.md)                                                                 | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `requestBody`                                                                                                                                                                                                                | [PostCompaniesCompanyUuidSuspensionsRequestBody](../../models/operations/PostCompaniesCompanyUuidSuspensionsRequestBody.md)                                                                                                  | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostCompaniesCompanyUuidSuspensionsResponse](../../models/operations/PostCompaniesCompanyUuidSuspensionsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |