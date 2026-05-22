# ContractorPayments

## Overview

### Available Operations

* [getReceipt](#getreceipt) - Get a single contractor payment receipt
* [fund](#fund) - Fund a contractor payment [DEMO]
* [list](#list) - Get contractor payments for a company
* [create](#create) - Create a contractor payment
* [get](#get) - Get a single contractor payment
* [delete](#delete) - Cancel a contractor payment
* [preview](#preview) - Preview contractor payment debit date
* [getV1ContractorPaymentsContractorPaymentIdPdf](#getv1contractorpaymentscontractorpaymentidpdf) - Get a contractor payment PDF

## getReceipt

Returns a contractor payment receipt.

Notes:
* Receipts are only available for direct deposit payments and are only available once those payments have been funded.
* Payroll Receipt requests for payrolls which do not have receipts available (e.g. payment by check) will return a 404 status.
* Hour and dollar amounts are returned as string representations of numeric decimals.
* Dollar amounts are represented to the cent.
* If no data has yet be inserted for a given field, it defaults to “0.00” (for fixed amounts).

scope: `payrolls:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-contractor_payments-contractor_payment_uuid-receipt" method="get" path="/v1/contractor_payments/{contractor_payment_uuid}/receipt" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1ContractorPaymentsContractorPaymentUuidReceiptHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1ContractorPaymentsContractorPaymentUuidReceiptResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1ContractorPaymentsContractorPaymentUuidReceiptResponse res = sdk.contractorPayments().getReceipt()
                .xGustoAPIVersion(GetV1ContractorPaymentsContractorPaymentUuidReceiptHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .contractorPaymentUuid("<id>")
                .call();

        if (res.contractorPaymentReceipt().isPresent()) {
            System.out.println(res.contractorPaymentReceipt().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1ContractorPaymentsContractorPaymentUuidReceiptHeaderXGustoAPIVersion>](../../models/operations/GetV1ContractorPaymentsContractorPaymentUuidReceiptHeaderXGustoAPIVersion.md)                                 | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `contractorPaymentUuid`                                                                                                                                                                                                      | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor payment                                                                                                                                                                                           |

### Response

**[GetV1ContractorPaymentsContractorPaymentUuidReceiptResponse](../../models/operations/GetV1ContractorPaymentsContractorPaymentUuidReceiptResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## fund

> 🚧 Demo action
>
> This action is only available in the Demo environment

Simulate funding a contractor payment. Funding only occurs automatically in the production environment when bank transactions are generated. Use this action in the demo environment to transition a contractor payment's `status` from `Unfunded` to `Funded`. A `Funded` status is required for generating a contractor payment receipt.

scope: `payrolls:run`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-contractor_payments-contractor_payment_uuid-fund" method="put" path="/v1/contractor_payments/{contractor_payment_uuid}/fund" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.GetV1ContractorPaymentsContractorPaymentUuidFundHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1ContractorPaymentsContractorPaymentUuidFundResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1ContractorPaymentsContractorPaymentUuidFundResponse res = sdk.contractorPayments().fund()
                .xGustoAPIVersion(GetV1ContractorPaymentsContractorPaymentUuidFundHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .contractorPaymentUuid("<id>")
                .call();

        if (res.contractorPayment().isPresent()) {
            System.out.println(res.contractorPayment().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1ContractorPaymentsContractorPaymentUuidFundHeaderXGustoAPIVersion>](../../models/operations/GetV1ContractorPaymentsContractorPaymentUuidFundHeaderXGustoAPIVersion.md)                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `contractorPaymentUuid`                                                                                                                                                                                                      | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor payment                                                                                                                                                                                           |

### Response

**[GetV1ContractorPaymentsContractorPaymentUuidFundResponse](../../models/operations/GetV1ContractorPaymentsContractorPaymentUuidFundResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## list

Returns an object containing individual contractor payments, within a given time period, including totals.

Results are returned in reverse chronological order (newest first).

scope: `payrolls:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_id-contractor_payments" method="get" path="/v1/companies/{company_id}/contractor_payments" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.ContractorPaymentSummary;
import com.gusto.embedded_api.models.components.ContractorPaymentSummaryByDates;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;
import java.lang.Object;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyIdContractorPaymentsRequest req = GetV1CompaniesCompanyIdContractorPaymentsRequest.builder()
                .companyId("<id>")
                .startDate("2020-01-01")
                .endDate("2020-12-31")
                .build();

        GetV1CompaniesCompanyIdContractorPaymentsResponse res = sdk.contractorPayments().list()
                .request(req)
                .call();

        if (res.oneOf().isPresent()) {
            GetV1CompaniesCompanyIdContractorPaymentsResponseBody unionValue = res.oneOf().get();
            Object raw = unionValue.value();
            if (raw instanceof ContractorPaymentSummary) {
                ContractorPaymentSummary contractorPaymentSummaryValue = (ContractorPaymentSummary) raw;
                // Handle contractorPaymentSummary variant
            } else if (raw instanceof ContractorPaymentSummaryByDates) {
                ContractorPaymentSummaryByDates contractorPaymentSummaryByDatesValue = (ContractorPaymentSummaryByDates) raw;
                // Handle contractorPaymentSummaryByDates variant
            } else {
                // Unknown or unsupported variant
            }
        }
    }
}
```

### Parameters

| Parameter                                                                                                                       | Type                                                                                                                            | Required                                                                                                                        | Description                                                                                                                     |
| ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `request`                                                                                                                       | [GetV1CompaniesCompanyIdContractorPaymentsRequest](../../models/operations/GetV1CompaniesCompanyIdContractorPaymentsRequest.md) | :heavy_check_mark:                                                                                                              | The request object to use for the request.                                                                                      |

### Response

**[GetV1CompaniesCompanyIdContractorPaymentsResponse](../../models/operations/GetV1CompaniesCompanyIdContractorPaymentsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## create

Pay a contractor. Information needed depends on the contractor's wage type (hourly vs fixed)

scope: `payrolls:run`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-contractor_payments" method="post" path="/v1/companies/{company_id}/contractor_payments" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.ContractorPaymentBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdContractorPaymentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdContractorPaymentsResponse;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyIdContractorPaymentsResponse res = sdk.contractorPayments().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdContractorPaymentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .contractorPaymentBody(ContractorPaymentBody.builder()
                    .contractorUuid("<id>")
                    .date(LocalDate.parse("2020-01-01"))
                    .wage("5000")
                    .hours("40")
                    .bonus("500")
                    .reimbursement("20")
                    .build())
                .call();

        if (res.contractorPayment().isPresent()) {
            System.out.println(res.contractorPayment().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-contractor_payments" method="post" path="/v1/companies/{company_id}/contractor_payments" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.ContractorPaymentBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdContractorPaymentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdContractorPaymentsResponse;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyIdContractorPaymentsResponse res = sdk.contractorPayments().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdContractorPaymentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .contractorPaymentBody(ContractorPaymentBody.builder()
                    .contractorUuid("<id>")
                    .date(LocalDate.parse("2020-01-01"))
                    .wage("5000")
                    .hours("40")
                    .bonus("500")
                    .reimbursement("20")
                    .build())
                .call();

        if (res.contractorPayment().isPresent()) {
            System.out.println(res.contractorPayment().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-contractor_payments" method="post" path="/v1/companies/{company_id}/contractor_payments" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.ContractorPaymentBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdContractorPaymentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdContractorPaymentsResponse;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyIdContractorPaymentsResponse res = sdk.contractorPayments().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdContractorPaymentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .contractorPaymentBody(ContractorPaymentBody.builder()
                    .contractorUuid("<id>")
                    .date(LocalDate.parse("2020-01-01"))
                    .wage("5000")
                    .hours("40")
                    .bonus("500")
                    .reimbursement("20")
                    .build())
                .call();

        if (res.contractorPayment().isPresent()) {
            System.out.println(res.contractorPayment().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-contractor_payments" method="post" path="/v1/companies/{company_id}/contractor_payments" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.ContractorPaymentBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdContractorPaymentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdContractorPaymentsResponse;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyIdContractorPaymentsResponse res = sdk.contractorPayments().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdContractorPaymentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .contractorPaymentBody(ContractorPaymentBody.builder()
                    .contractorUuid("<id>")
                    .date(LocalDate.parse("2020-01-01"))
                    .wage("5000")
                    .hours("40")
                    .bonus("500")
                    .reimbursement("20")
                    .build())
                .call();

        if (res.contractorPayment().isPresent()) {
            System.out.println(res.contractorPayment().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompaniesCompanyIdContractorPaymentsHeaderXGustoAPIVersion>](../../models/operations/PostV1CompaniesCompanyIdContractorPaymentsHeaderXGustoAPIVersion.md)                                                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `contractorPaymentBody`                                                                                                                                                                                                      | [ContractorPaymentBody](../../models/components/ContractorPaymentBody.md)                                                                                                                                                    | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompaniesCompanyIdContractorPaymentsResponse](../../models/operations/PostV1CompaniesCompanyIdContractorPaymentsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## get

Returns a single contractor payment.

scope: `payrolls:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_id-contractor_payment-contractor-payment" method="get" path="/v1/companies/{company_id}/contractor_payments/{contractor_payment_id}" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyIdContractorPaymentContractorPaymentHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyIdContractorPaymentContractorPaymentResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyIdContractorPaymentContractorPaymentResponse res = sdk.contractorPayments().get()
                .xGustoAPIVersion(GetV1CompaniesCompanyIdContractorPaymentContractorPaymentHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .contractorPaymentId("<id>")
                .call();

        if (res.contractorPayment().isPresent()) {
            System.out.println(res.contractorPayment().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompaniesCompanyIdContractorPaymentContractorPaymentHeaderXGustoAPIVersion>](../../models/operations/GetV1CompaniesCompanyIdContractorPaymentContractorPaymentHeaderXGustoAPIVersion.md)                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `contractorPaymentId`                                                                                                                                                                                                        | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor payment                                                                                                                                                                                           |

### Response

**[GetV1CompaniesCompanyIdContractorPaymentContractorPaymentResponse](../../models/operations/GetV1CompaniesCompanyIdContractorPaymentContractorPaymentResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## delete

Cancels and deletes a contractor payment. If the contractor payment has already started processing ("may_cancel": true), the payment cannot be cancelled.

scope: `payrolls:run`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-companies-company_id-contractor_payment-contractor-payment" method="delete" path="/v1/companies/{company_id}/contractor_payments/{contractor_payment_id}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.DeleteV1CompaniesCompanyIdContractorPaymentContractorPaymentHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.DeleteV1CompaniesCompanyIdContractorPaymentContractorPaymentResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1CompaniesCompanyIdContractorPaymentContractorPaymentResponse res = sdk.contractorPayments().delete()
                .xGustoAPIVersion(DeleteV1CompaniesCompanyIdContractorPaymentContractorPaymentHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .contractorPaymentId("<id>")
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1CompaniesCompanyIdContractorPaymentContractorPaymentHeaderXGustoAPIVersion>](../../models/operations/DeleteV1CompaniesCompanyIdContractorPaymentContractorPaymentHeaderXGustoAPIVersion.md)               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `contractorPaymentId`                                                                                                                                                                                                        | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor payment                                                                                                                                                                                           |

### Response

**[DeleteV1CompaniesCompanyIdContractorPaymentContractorPaymentResponse](../../models/operations/DeleteV1CompaniesCompanyIdContractorPaymentContractorPaymentResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## preview

Returns a debit_date dependent on the ACH payment speed of the company.

If the payment method is Check or Historical payment, the debit_date will be the same as the check_date.

scope: `payrolls:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-companies-company_uuid-contractor_payments-preview" method="get" path="/v1/companies/{company_uuid}/contractor_payments/preview" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.ContractorPaymentsPreviewBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.GetCompaniesCompanyUuidContractorPaymentsPreviewHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetCompaniesCompanyUuidContractorPaymentsPreviewResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetCompaniesCompanyUuidContractorPaymentsPreviewResponse res = sdk.contractorPayments().preview()
                .xGustoAPIVersion(GetCompaniesCompanyUuidContractorPaymentsPreviewHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .contractorPaymentsPreviewBody(ContractorPaymentsPreviewBody.builder()
                    .contractorPayments(List.of())
                    .build())
                .call();

        if (res.contractorPaymentsPreview().isPresent()) {
            System.out.println(res.contractorPaymentsPreview().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetCompaniesCompanyUuidContractorPaymentsPreviewHeaderXGustoAPIVersion>](../../models/operations/GetCompaniesCompanyUuidContractorPaymentsPreviewHeaderXGustoAPIVersion.md)                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `contractorPaymentsPreviewBody`                                                                                                                                                                                              | [ContractorPaymentsPreviewBody](../../models/components/ContractorPaymentsPreviewBody.md)                                                                                                                                    | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[GetCompaniesCompanyUuidContractorPaymentsPreviewResponse](../../models/operations/GetCompaniesCompanyUuidContractorPaymentsPreviewResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getV1ContractorPaymentsContractorPaymentIdPdf

Get a PDF document for a single contractor payment.

scope: `payrolls:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-contractor_payments-contractor_payment_id-pdf" method="get" path="/v1/contractor_payments/{contractor_payment_id}/pdf" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.operations.GetV1ContractorPaymentsContractorPaymentIdPdfHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1ContractorPaymentsContractorPaymentIdPdfResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1ContractorPaymentsContractorPaymentIdPdfResponse res = sdk.contractorPayments().getV1ContractorPaymentsContractorPaymentIdPdf()
                .xGustoAPIVersion(GetV1ContractorPaymentsContractorPaymentIdPdfHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .contractorPaymentId("<id>")
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1ContractorPaymentsContractorPaymentIdPdfHeaderXGustoAPIVersion>](../../models/operations/GetV1ContractorPaymentsContractorPaymentIdPdfHeaderXGustoAPIVersion.md)                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `contractorPaymentId`                                                                                                                                                                                                        | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor payment                                                                                                                                                                                           |

### Response

**[GetV1ContractorPaymentsContractorPaymentIdPdfResponse](../../models/operations/GetV1ContractorPaymentsContractorPaymentIdPdfResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |