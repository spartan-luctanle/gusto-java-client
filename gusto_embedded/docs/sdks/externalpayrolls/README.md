# ExternalPayrolls

## Overview

### Available Operations

* [get](#get) - Get external payrolls for a company
* [create](#create) - Create an external payroll for a company
* [retrieve](#retrieve) - Get an external payroll
* [update](#update) - Update an external payroll
* [delete](#delete) - Delete an external payroll
* [calculateTaxes](#calculatetaxes) - Get tax suggestions for an external payroll
* [listTaxLiabilities](#listtaxliabilities) - Get tax liabilities
* [updateTaxLiabilities](#updatetaxliabilities) - Update tax liabilities
* [finalizeTaxLiabilities](#finalizetaxliabilities) - Finalize tax liabilities options and convert into processed payrolls

## get

Get external payrolls for a company.

scope: `external_payrolls:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-company-external-payrolls" method="get" path="/v1/companies/{company_uuid}/external_payrolls" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1CompanyExternalPayrollsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1CompanyExternalPayrollsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompanyExternalPayrollsResponse res = sdk.externalPayrolls().get()
                .xGustoAPIVersion(GetV1CompanyExternalPayrollsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .call();

        if (res.externalPayrollBasics().isPresent()) {
            System.out.println(res.externalPayrollBasics().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompanyExternalPayrollsHeaderXGustoAPIVersion>](../../models/operations/GetV1CompanyExternalPayrollsHeaderXGustoAPIVersion.md)                                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `page`                                                                                                                                                                                                                       | *Optional\<Long>*                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                           | The page that is requested. When unspecified, will load all objects unless endpoint forces pagination.                                                                                                                       |
| `per`                                                                                                                                                                                                                        | *Optional\<Long>*                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                           | Number of objects per page. For majority of endpoints will default to 25                                                                                                                                                     |

### Response

**[GetV1CompanyExternalPayrollsResponse](../../models/operations/GetV1CompanyExternalPayrollsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## create

Creates a new external payroll for a company.

scope: `external_payrolls:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="post-v1-external-payroll" method="post" path="/v1/companies/{company_uuid}/external_payrolls" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.ExternalPayrollCreateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1ExternalPayrollHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1ExternalPayrollResponse;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1ExternalPayrollResponse res = sdk.externalPayrolls().create()
                .xGustoAPIVersion(PostV1ExternalPayrollHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .externalPayrollCreateRequest(ExternalPayrollCreateRequest.builder()
                    .checkDate(LocalDate.parse("<value>"))
                    .paymentPeriodStartDate(LocalDate.parse("<value>"))
                    .paymentPeriodEndDate(LocalDate.parse("<value>"))
                    .build())
                .call();

        if (res.externalPayroll().isPresent()) {
            System.out.println(res.externalPayroll().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="post-v1-external-payroll" method="post" path="/v1/companies/{company_uuid}/external_payrolls" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.ExternalPayrollCreateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1ExternalPayrollHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1ExternalPayrollResponse;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1ExternalPayrollResponse res = sdk.externalPayrolls().create()
                .xGustoAPIVersion(PostV1ExternalPayrollHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .externalPayrollCreateRequest(ExternalPayrollCreateRequest.builder()
                    .checkDate(LocalDate.parse("2022-06-01"))
                    .paymentPeriodStartDate(LocalDate.parse("2022-05-15"))
                    .paymentPeriodEndDate(LocalDate.parse("2022-05-30"))
                    .build())
                .call();

        if (res.externalPayroll().isPresent()) {
            System.out.println(res.externalPayroll().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="post-v1-external-payroll" method="post" path="/v1/companies/{company_uuid}/external_payrolls" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.ExternalPayrollCreateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1ExternalPayrollHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1ExternalPayrollResponse;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1ExternalPayrollResponse res = sdk.externalPayrolls().create()
                .xGustoAPIVersion(PostV1ExternalPayrollHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .externalPayrollCreateRequest(ExternalPayrollCreateRequest.builder()
                    .checkDate(LocalDate.parse("<value>"))
                    .paymentPeriodStartDate(LocalDate.parse("<value>"))
                    .paymentPeriodEndDate(LocalDate.parse("<value>"))
                    .build())
                .call();

        if (res.externalPayroll().isPresent()) {
            System.out.println(res.externalPayroll().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="post-v1-external-payroll" method="post" path="/v1/companies/{company_uuid}/external_payrolls" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.ExternalPayrollCreateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1ExternalPayrollHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1ExternalPayrollResponse;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1ExternalPayrollResponse res = sdk.externalPayrolls().create()
                .xGustoAPIVersion(PostV1ExternalPayrollHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .externalPayrollCreateRequest(ExternalPayrollCreateRequest.builder()
                    .checkDate(LocalDate.parse("<value>"))
                    .paymentPeriodStartDate(LocalDate.parse("<value>"))
                    .paymentPeriodEndDate(LocalDate.parse("<value>"))
                    .build())
                .call();

        if (res.externalPayroll().isPresent()) {
            System.out.println(res.externalPayroll().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1ExternalPayrollHeaderXGustoAPIVersion>](../../models/operations/PostV1ExternalPayrollHeaderXGustoAPIVersion.md)                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `externalPayrollCreateRequest`                                                                                                                                                                                               | [ExternalPayrollCreateRequest](../../models/components/ExternalPayrollCreateRequest.md)                                                                                                                                      | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1ExternalPayrollResponse](../../models/operations/PostV1ExternalPayrollResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## retrieve

Get an external payroll for a given company.

scope: `external_payrolls:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-external-payroll" method="get" path="/v1/companies/{company_uuid}/external_payrolls/{external_payroll_id}" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1ExternalPayrollHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1ExternalPayrollResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1ExternalPayrollResponse res = sdk.externalPayrolls().retrieve()
                .xGustoAPIVersion(GetV1ExternalPayrollHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .externalPayrollId("<id>")
                .call();

        if (res.externalPayroll().isPresent()) {
            System.out.println(res.externalPayroll().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1ExternalPayrollHeaderXGustoAPIVersion>](../../models/operations/GetV1ExternalPayrollHeaderXGustoAPIVersion.md)                                                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `externalPayrollId`                                                                                                                                                                                                          | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the external payroll                                                                                                                                                                                             |

### Response

**[GetV1ExternalPayrollResponse](../../models/operations/GetV1ExternalPayrollResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## update

Update an external payroll with a list of external payroll items.

scope: `external_payrolls:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-external-payroll" method="put" path="/v1/companies/{company_uuid}/external_payrolls/{external_payroll_id}" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.*;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1ExternalPayrollHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1ExternalPayrollResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1ExternalPayrollResponse res = sdk.externalPayrolls().update()
                .xGustoAPIVersion(PutV1ExternalPayrollHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .externalPayrollId("<id>")
                .externalPayrollUpdateRequest(ExternalPayrollUpdateRequest.builder()
                    .externalPayrollItems(List.of(
                        ExternalPayrollUpdateRequestExternalPayrollItems.builder()
                            .employeeUuid("44f7cba9-7a3d-4f08-b7bd-6fcf5211f8ca")
                            .earnings(List.of(
                                ExternalPayrollUpdateRequestEarnings.builder()
                                    .earningType(ExternalPayrollUpdateRequestEarningType.COMPANY_PAY_TYPE)
                                    .earningId(1L)
                                    .amount("10000.00")
                                    .hours("80.0")
                                    .build()))
                            .benefits(List.of(
                                ExternalPayrollUpdateRequestBenefits.builder()
                                    .benefitId(22L)
                                    .companyContributionAmount("100.00")
                                    .employeeDeductionAmount("50.00")
                                    .build()))
                            .taxes(List.of(
                                ExternalPayrollUpdateRequestTaxes.builder()
                                    .taxId(1L)
                                    .amount("400.00")
                                    .build()))
                            .build()))
                    .build())
                .call();

        if (res.externalPayroll().isPresent()) {
            System.out.println(res.externalPayroll().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-external-payroll" method="put" path="/v1/companies/{company_uuid}/external_payrolls/{external_payroll_id}" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.*;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1ExternalPayrollHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1ExternalPayrollResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1ExternalPayrollResponse res = sdk.externalPayrolls().update()
                .xGustoAPIVersion(PutV1ExternalPayrollHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .externalPayrollId("<id>")
                .externalPayrollUpdateRequest(ExternalPayrollUpdateRequest.builder()
                    .externalPayrollItems(List.of(
                        ExternalPayrollUpdateRequestExternalPayrollItems.builder()
                            .employeeUuid("403c6ee3-5f58-40ef-a117-ff7175cd9ee3")
                            .earnings(List.of(
                                ExternalPayrollUpdateRequestEarnings.builder()
                                    .earningType(ExternalPayrollUpdateRequestEarningType.COMPANY_PAY_TYPE)
                                    .earningId(1L)
                                    .amount("200.00")
                                    .hours("0.0")
                                    .build(),
                                ExternalPayrollUpdateRequestEarnings.builder()
                                    .earningType(ExternalPayrollUpdateRequestEarningType.COMPANY_EARNING_TYPE)
                                    .earningId(2L)
                                    .amount("5000.00")
                                    .hours("0.0")
                                    .build()))
                            .benefits(List.of(
                                ExternalPayrollUpdateRequestBenefits.builder()
                                    .benefitId(10L)
                                    .companyContributionAmount("300.0")
                                    .employeeDeductionAmount("300.0")
                                    .build(),
                                ExternalPayrollUpdateRequestBenefits.builder()
                                    .benefitId(21L)
                                    .companyContributionAmount("50.0")
                                    .employeeDeductionAmount("100.0")
                                    .build()))
                            .taxes(List.of(
                                ExternalPayrollUpdateRequestTaxes.builder()
                                    .taxId(1L)
                                    .amount("20.0")
                                    .build(),
                                ExternalPayrollUpdateRequestTaxes.builder()
                                    .taxId(2L)
                                    .amount("100.0")
                                    .build()))
                            .build()))
                    .replaceFields(true)
                    .build())
                .call();

        if (res.externalPayroll().isPresent()) {
            System.out.println(res.externalPayroll().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-external-payroll" method="put" path="/v1/companies/{company_uuid}/external_payrolls/{external_payroll_id}" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.*;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1ExternalPayrollHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1ExternalPayrollResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1ExternalPayrollResponse res = sdk.externalPayrolls().update()
                .xGustoAPIVersion(PutV1ExternalPayrollHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .externalPayrollId("<id>")
                .externalPayrollUpdateRequest(ExternalPayrollUpdateRequest.builder()
                    .externalPayrollItems(List.of(
                        ExternalPayrollUpdateRequestExternalPayrollItems.builder()
                            .employeeUuid("44f7cba9-7a3d-4f08-b7bd-6fcf5211f8ca")
                            .earnings(List.of(
                                ExternalPayrollUpdateRequestEarnings.builder()
                                    .earningType(ExternalPayrollUpdateRequestEarningType.COMPANY_PAY_TYPE)
                                    .earningId(1L)
                                    .amount("10000.00")
                                    .hours("80.0")
                                    .build()))
                            .benefits(List.of(
                                ExternalPayrollUpdateRequestBenefits.builder()
                                    .benefitId(22L)
                                    .companyContributionAmount("100.00")
                                    .employeeDeductionAmount("50.00")
                                    .build()))
                            .taxes(List.of(
                                ExternalPayrollUpdateRequestTaxes.builder()
                                    .taxId(1L)
                                    .amount("400.00")
                                    .build()))
                            .build()))
                    .build())
                .call();

        if (res.externalPayroll().isPresent()) {
            System.out.println(res.externalPayroll().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-external-payroll" method="put" path="/v1/companies/{company_uuid}/external_payrolls/{external_payroll_id}" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.ExternalPayrollUpdateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1ExternalPayrollHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1ExternalPayrollResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1ExternalPayrollResponse res = sdk.externalPayrolls().update()
                .xGustoAPIVersion(PutV1ExternalPayrollHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .externalPayrollId("<id>")
                .externalPayrollUpdateRequest(ExternalPayrollUpdateRequest.builder()
                    .externalPayrollItems(List.of())
                    .build())
                .call();

        if (res.externalPayroll().isPresent()) {
            System.out.println(res.externalPayroll().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1ExternalPayrollHeaderXGustoAPIVersion>](../../models/operations/PutV1ExternalPayrollHeaderXGustoAPIVersion.md)                                                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `externalPayrollId`                                                                                                                                                                                                          | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the external payroll                                                                                                                                                                                             |
| `externalPayrollUpdateRequest`                                                                                                                                                                                               | [ExternalPayrollUpdateRequest](../../models/components/ExternalPayrollUpdateRequest.md)                                                                                                                                      | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1ExternalPayrollResponse](../../models/operations/PutV1ExternalPayrollResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## delete

Delete an external payroll.

scope: `external_payrolls:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-external-payroll" method="delete" path="/v1/companies/{company_uuid}/external_payrolls/{external_payroll_id}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.operations.DeleteV1ExternalPayrollHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.DeleteV1ExternalPayrollResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1ExternalPayrollResponse res = sdk.externalPayrolls().delete()
                .xGustoAPIVersion(DeleteV1ExternalPayrollHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .externalPayrollId("<id>")
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1ExternalPayrollHeaderXGustoAPIVersion>](../../models/operations/DeleteV1ExternalPayrollHeaderXGustoAPIVersion.md)                                                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `externalPayrollId`                                                                                                                                                                                                          | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the external payroll                                                                                                                                                                                             |

### Response

**[DeleteV1ExternalPayrollResponse](../../models/operations/DeleteV1ExternalPayrollResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |

## calculateTaxes

Get tax suggestions for an external payroll. Earnings and/or benefits data must be saved prior to the calculation in order to retrieve accurate tax calculation.

scope: `external_payrolls:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-external-payroll-calculate-taxes" method="get" path="/v1/companies/{company_uuid}/external_payrolls/{external_payroll_id}/calculate_taxes" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.GetV1ExternalPayrollCalculateTaxesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1ExternalPayrollCalculateTaxesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1ExternalPayrollCalculateTaxesResponse res = sdk.externalPayrolls().calculateTaxes()
                .xGustoAPIVersion(GetV1ExternalPayrollCalculateTaxesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .externalPayrollId("<id>")
                .call();

        if (res.externalPayrollTaxSuggestions().isPresent()) {
            System.out.println(res.externalPayrollTaxSuggestions().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1ExternalPayrollCalculateTaxesHeaderXGustoAPIVersion>](../../models/operations/GetV1ExternalPayrollCalculateTaxesHeaderXGustoAPIVersion.md)                                                                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `externalPayrollId`                                                                                                                                                                                                          | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the external payroll                                                                                                                                                                                             |

### Response

**[GetV1ExternalPayrollCalculateTaxesResponse](../../models/operations/GetV1ExternalPayrollCalculateTaxesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## listTaxLiabilities

Get tax liabilities from aggregate external payrolls for a company.

scope: `external_payrolls:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-tax-liabilities" method="get" path="/v1/companies/{company_uuid}/external_payrolls/tax_liabilities" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1TaxLiabilitiesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1TaxLiabilitiesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1TaxLiabilitiesResponse res = sdk.externalPayrolls().listTaxLiabilities()
                .xGustoAPIVersion(GetV1TaxLiabilitiesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .call();

        if (res.taxLiabilitiesSelections().isPresent()) {
            System.out.println(res.taxLiabilitiesSelections().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1TaxLiabilitiesHeaderXGustoAPIVersion>](../../models/operations/GetV1TaxLiabilitiesHeaderXGustoAPIVersion.md)                                                                                                 | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |

### Response

**[GetV1TaxLiabilitiesResponse](../../models/operations/GetV1TaxLiabilitiesResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## updateTaxLiabilities

Update tax liabilities for a company.

scope: `external_payrolls:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-tax-liabilities" method="put" path="/v1/companies/{company_uuid}/external_payrolls/tax_liabilities" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.TaxLiabilitySelectionsRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.PutV1TaxLiabilitiesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1TaxLiabilitiesResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1TaxLiabilitiesResponse res = sdk.externalPayrolls().updateTaxLiabilities()
                .xGustoAPIVersion(PutV1TaxLiabilitiesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .taxLiabilitySelectionsRequest(TaxLiabilitySelectionsRequest.builder()
                    .liabilitySelections(List.of())
                    .build())
                .call();

        if (res.taxLiabilitiesSelections().isPresent()) {
            System.out.println(res.taxLiabilitiesSelections().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-tax-liabilities" method="put" path="/v1/companies/{company_uuid}/external_payrolls/tax_liabilities" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.LiabilitySelections;
import com.gusto.embedded_api.models.components.TaxLiabilitySelectionsRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.PutV1TaxLiabilitiesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1TaxLiabilitiesResponse;
import java.lang.Exception;
import java.util.List;
import java.util.Optional;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1TaxLiabilitiesResponse res = sdk.externalPayrolls().updateTaxLiabilities()
                .xGustoAPIVersion(PutV1TaxLiabilitiesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .taxLiabilitySelectionsRequest(TaxLiabilitySelectionsRequest.builder()
                    .liabilitySelections(List.of(
                        LiabilitySelections.builder()
                            .taxId(1L)
                            .lastUnpaidExternalPayrollUuid("7985032c-ee3a-4e98-af27-d56551eb5f1c")
                            .unpaidLiabilityAmount("50")
                            .build(),
                        LiabilitySelections.builder()
                            .taxId(2L)
                            .lastUnpaidExternalPayrollUuid("5ed14dbb-958f-47c8-b16e-c4fed82dc486")
                            .unpaidLiabilityAmount("400")
                            .build(),
                        LiabilitySelections.builder()
                            .taxId(8L)
                            .lastUnpaidExternalPayrollUuid(Optional.empty())
                            .unpaidLiabilityAmount("0")
                            .build()))
                    .build())
                .call();

        if (res.taxLiabilitiesSelections().isPresent()) {
            System.out.println(res.taxLiabilitiesSelections().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-tax-liabilities" method="put" path="/v1/companies/{company_uuid}/external_payrolls/tax_liabilities" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.LiabilitySelections;
import com.gusto.embedded_api.models.components.TaxLiabilitySelectionsRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.PutV1TaxLiabilitiesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1TaxLiabilitiesResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1TaxLiabilitiesResponse res = sdk.externalPayrolls().updateTaxLiabilities()
                .xGustoAPIVersion(PutV1TaxLiabilitiesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .taxLiabilitySelectionsRequest(TaxLiabilitySelectionsRequest.builder()
                    .liabilitySelections(List.of(
                        LiabilitySelections.builder()
                            .taxId(1L)
                            .lastUnpaidExternalPayrollUuid("1bf1efe1-72d4-4e6e-a181-611f3ea66435")
                            .unpaidLiabilityAmount("47.5")
                            .build()))
                    .build())
                .call();

        if (res.taxLiabilitiesSelections().isPresent()) {
            System.out.println(res.taxLiabilitiesSelections().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-tax-liabilities" method="put" path="/v1/companies/{company_uuid}/external_payrolls/tax_liabilities" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.LiabilitySelections;
import com.gusto.embedded_api.models.components.TaxLiabilitySelectionsRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.PutV1TaxLiabilitiesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1TaxLiabilitiesResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1TaxLiabilitiesResponse res = sdk.externalPayrolls().updateTaxLiabilities()
                .xGustoAPIVersion(PutV1TaxLiabilitiesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .taxLiabilitySelectionsRequest(TaxLiabilitySelectionsRequest.builder()
                    .liabilitySelections(List.of(
                        LiabilitySelections.builder()
                            .taxId(1L)
                            .lastUnpaidExternalPayrollUuid("1bf1efe1-72d4-4e6e-a181-611f3ea66435")
                            .unpaidLiabilityAmount("47.5")
                            .build()))
                    .build())
                .call();

        if (res.taxLiabilitiesSelections().isPresent()) {
            System.out.println(res.taxLiabilitiesSelections().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1TaxLiabilitiesHeaderXGustoAPIVersion>](../../models/operations/PutV1TaxLiabilitiesHeaderXGustoAPIVersion.md)                                                                                                 | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `taxLiabilitySelectionsRequest`                                                                                                                                                                                              | [TaxLiabilitySelectionsRequest](../../models/components/TaxLiabilitySelectionsRequest.md)                                                                                                                                    | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1TaxLiabilitiesResponse](../../models/operations/PutV1TaxLiabilitiesResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## finalizeTaxLiabilities

Finalizes tax liabilities for a company. All external payrolls edit action will be disabled.

### Asynchronous processing
This endpoint triggers an asynchronous operation. The external payrolls will be processed in the background after finalization.

scope: `external_payrolls:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-tax-liabilities-finish" method="put" path="/v1/companies/{company_uuid}/external_payrolls/tax_liabilities/finish" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.operations.PutV1TaxLiabilitiesFinishHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1TaxLiabilitiesFinishResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1TaxLiabilitiesFinishResponse res = sdk.externalPayrolls().finalizeTaxLiabilities()
                .xGustoAPIVersion(PutV1TaxLiabilitiesFinishHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1TaxLiabilitiesFinishHeaderXGustoAPIVersion>](../../models/operations/PutV1TaxLiabilitiesFinishHeaderXGustoAPIVersion.md)                                                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |

### Response

**[PutV1TaxLiabilitiesFinishResponse](../../models/operations/PutV1TaxLiabilitiesFinishResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |