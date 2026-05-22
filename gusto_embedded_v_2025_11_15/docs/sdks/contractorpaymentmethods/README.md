# ContractorPaymentMethods

## Overview

### Available Operations

* [createBankAccount](#createbankaccount) - Create a contractor bank account

## createBankAccount

Creates a contractor bank account.

Note: We currently only support one bank account per contractor. Using this endpoint on a contractor who already has a bank account will just replace it.

scope: `contractor_payment_methods:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-contractors-contractor_uuid-bank_accounts" method="post" path="/v1/contractors/{contractor_uuid}/bank_accounts" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.ContractorBankAccountCreateRequestBody;
import com.gusto.embedded_api_v_2025_11_15.models.components.ContractorBankAccountCreateRequestBodyAccountType;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1ContractorsContractorUuidBankAccountsHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1ContractorsContractorUuidBankAccountsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1ContractorsContractorUuidBankAccountsResponse res = sdk.contractorPaymentMethods().createBankAccount()
                .xGustoAPIVersion(PostV1ContractorsContractorUuidBankAccountsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .contractorUuid("<id>")
                .contractorBankAccountCreateRequestBody(ContractorBankAccountCreateRequestBody.builder()
                    .name("<value>")
                    .routingNumber("<value>")
                    .accountNumber("<value>")
                    .accountType(ContractorBankAccountCreateRequestBodyAccountType.SAVINGS)
                    .build())
                .call();

        if (res.contractorBankAccount().isPresent()) {
            System.out.println(res.contractorBankAccount().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1ContractorsContractorUuidBankAccountsHeaderXGustoAPIVersion>](../../models/operations/PostV1ContractorsContractorUuidBankAccountsHeaderXGustoAPIVersion.md)                                                 | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `contractorUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor                                                                                                                                                                                                   |
| `contractorBankAccountCreateRequestBody`                                                                                                                                                                                     | [ContractorBankAccountCreateRequestBody](../../models/components/ContractorBankAccountCreateRequestBody.md)                                                                                                                  | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1ContractorsContractorUuidBankAccountsResponse](../../models/operations/PostV1ContractorsContractorUuidBankAccountsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |