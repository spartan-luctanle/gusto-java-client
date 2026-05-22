# PaymentConfigs

## Overview

### Available Operations

* [get](#get) - Get a company's payment configs
* [update](#update) - Update a company's payment configs

## get

Get payment speed configurations for the company: payment speed (1-day, 2-day, or 4-day ACH), fast payment limit, partner-owned disbursement setting, and earned fast ACH blockers when applicable. 1-day is only available to partners that opt in.

### Related guides
- [Payroll Processing Speeds](doc:2-day-vs-4-day)

scope: `company_payment_configs:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-company-payment-configs" method="get" path="/v1/companies/{company_uuid}/payment_configs" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompanyPaymentConfigsHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompanyPaymentConfigsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompanyPaymentConfigsResponse res = sdk.paymentConfigs().get()
                .xGustoAPIVersion(GetV1CompanyPaymentConfigsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyUuid("<id>")
                .call();

        if (res.paymentConfigs().isPresent()) {
            System.out.println(res.paymentConfigs().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompanyPaymentConfigsHeaderXGustoAPIVersion>](../../models/operations/GetV1CompanyPaymentConfigsHeaderXGustoAPIVersion.md)                                                                                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |

### Response

**[GetV1CompanyPaymentConfigsResponse](../../models/operations/GetV1CompanyPaymentConfigsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## update

Update payment speed, fast payment limit, and/or partner-owned disbursement for a company.

At least one of `payment_speed`, `fast_payment_limit`, or `partner_owned_disbursement` is required.
1-day payment speed is only applicable to partners that opt in. 1-day is not allowed when AutoPilot is enabled.

### Related guides
- [Payroll Processing Speeds](doc:2-day-vs-4-day)

scope: `company_payment_configs:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-company-payment-configs" method="put" path="/v1/companies/{company_uuid}/payment_configs" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.PaymentConfigsUpdateRequest;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1CompanyPaymentConfigsHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1CompanyPaymentConfigsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompanyPaymentConfigsResponse res = sdk.paymentConfigs().update()
                .xGustoAPIVersion(PutV1CompanyPaymentConfigsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyUuid("<id>")
                .paymentConfigsUpdateRequest(PaymentConfigsUpdateRequest.builder()
                    .build())
                .call();

        if (res.paymentConfigs().isPresent()) {
            System.out.println(res.paymentConfigs().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1CompanyPaymentConfigsHeaderXGustoAPIVersion>](../../models/operations/PutV1CompanyPaymentConfigsHeaderXGustoAPIVersion.md)                                                                                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `paymentConfigsUpdateRequest`                                                                                                                                                                                                | [PaymentConfigsUpdateRequest](../../models/components/PaymentConfigsUpdateRequest.md)                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1CompanyPaymentConfigsResponse](../../models/operations/PutV1CompanyPaymentConfigsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |