# ContractorPaymentMethods

## Overview

### Available Operations

* [createBankAccount](#createbankaccount) - Create a contractor bank account

## createBankAccount

Creates a contractor bank account.

Note: We currently only support one bank account per contractor. Using this endpoint on a contractor who already has a bank account will just replace it.

scope: `contractor_payment_methods:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="post-v1-contractors-contractor_uuid-bank_accounts" method="post" path="/v1/contractors/{contractor_uuid}/bank_accounts" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.ContractorBankAccountCreateRequestBody;
import com.gusto.embedded_api.models.components.ContractorBankAccountCreateRequestBodyAccountType;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1ContractorsContractorUuidBankAccountsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1ContractorsContractorUuidBankAccountsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1ContractorsContractorUuidBankAccountsResponse res = sdk.contractorPaymentMethods().createBankAccount()
                .xGustoAPIVersion(PostV1ContractorsContractorUuidBankAccountsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
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
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="post-v1-contractors-contractor_uuid-bank_accounts" method="post" path="/v1/contractors/{contractor_uuid}/bank_accounts" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.ContractorBankAccountCreateRequestBody;
import com.gusto.embedded_api.models.components.ContractorBankAccountCreateRequestBodyAccountType;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1ContractorsContractorUuidBankAccountsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1ContractorsContractorUuidBankAccountsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1ContractorsContractorUuidBankAccountsResponse res = sdk.contractorPaymentMethods().createBankAccount()
                .xGustoAPIVersion(PostV1ContractorsContractorUuidBankAccountsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .contractorUuid("<id>")
                .contractorBankAccountCreateRequestBody(ContractorBankAccountCreateRequestBody.builder()
                    .name("BoA Checking Account")
                    .routingNumber("266905059")
                    .accountNumber("5809431207")
                    .accountType(ContractorBankAccountCreateRequestBodyAccountType.CHECKING)
                    .build())
                .call();

        if (res.contractorBankAccount().isPresent()) {
            System.out.println(res.contractorBankAccount().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="post-v1-contractors-contractor_uuid-bank_accounts" method="post" path="/v1/contractors/{contractor_uuid}/bank_accounts" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.ContractorBankAccountCreateRequestBody;
import com.gusto.embedded_api.models.components.ContractorBankAccountCreateRequestBodyAccountType;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1ContractorsContractorUuidBankAccountsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1ContractorsContractorUuidBankAccountsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1ContractorsContractorUuidBankAccountsResponse res = sdk.contractorPaymentMethods().createBankAccount()
                .xGustoAPIVersion(PostV1ContractorsContractorUuidBankAccountsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
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
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="post-v1-contractors-contractor_uuid-bank_accounts" method="post" path="/v1/contractors/{contractor_uuid}/bank_accounts" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.ContractorBankAccountCreateRequestBody;
import com.gusto.embedded_api.models.components.ContractorBankAccountCreateRequestBodyAccountType;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1ContractorsContractorUuidBankAccountsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1ContractorsContractorUuidBankAccountsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1ContractorsContractorUuidBankAccountsResponse res = sdk.contractorPaymentMethods().createBankAccount()
                .xGustoAPIVersion(PostV1ContractorsContractorUuidBankAccountsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
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