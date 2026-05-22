# Invoices

## Overview

### Available Operations

* [get](#get) - Retrieve invoicing data for companies

## get

Retrieve data for active companies used to calculate invoices for Gusto Embedded Payroll. A company is considered active for an invoice period if they are an active partner managed company, have run payroll or created contractor payments since becoming a partner managed company, and are not suspended at any point during the invoice period.  This endpoint forces pagination, with 100 results returned at a time. You can learn more about our pagination here: [pagination guide](https://docs.gusto.com/embedded-payroll/docs/pagination)

📘 System Access Authentication

This endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)

scope: `invoices:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-invoices-invoice-period" method="get" path="/v1/invoices/{invoice_period}" example="example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        GetInvoicesInvoicePeriodRequest req = GetInvoicesInvoicePeriodRequest.builder()
                .invoicePeriod("2020-01")
                .build();

        GetInvoicesInvoicePeriodResponse res = sdk.invoices().get()
                .request(req)
                .security(GetInvoicesInvoicePeriodSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .call();

        if (res.invoiceData().isPresent()) {
            System.out.println(res.invoiceData().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                | Type                                                                                                                                     | Required                                                                                                                                 | Description                                                                                                                              |
| ---------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `request`                                                                                                                                | [GetInvoicesInvoicePeriodRequest](../../models/operations/GetInvoicesInvoicePeriodRequest.md)                                            | :heavy_check_mark:                                                                                                                       | The request object to use for the request.                                                                                               |
| `security`                                                                                                                               | [com.gusto.embedded_api.models.operations.GetInvoicesInvoicePeriodSecurity](../../models/operations/GetInvoicesInvoicePeriodSecurity.md) | :heavy_check_mark:                                                                                                                       | The security requirements to use for the request.                                                                                        |

### Response

**[GetInvoicesInvoicePeriodResponse](../../models/operations/GetInvoicesInvoicePeriodResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |