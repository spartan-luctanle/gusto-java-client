# BankAccounts

## Overview

### Available Operations

* [get](#get) - Get all company bank accounts
* [create](#create) - Create a company bank account
* [verify](#verify) - Verify a company bank account
* [createFromPlaidToken](#createfromplaidtoken) - Create a bank account from a plaid processor token
* [deleteV1CompaniesCompanyIdBankAccountsBankAccountId](#deletev1companiescompanyidbankaccountsbankaccountid) - Delete a company bank account

## get

Returns company bank accounts. Currently, we only support a single default bank account per company.

scope: `company_bank_accounts:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_id-bank-accounts" method="get" path="/v1/companies/{company_id}/bank_accounts" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyIdBankAccountsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyIdBankAccountsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyIdBankAccountsResponse res = sdk.bankAccounts().get()
                .xGustoAPIVersion(GetV1CompaniesCompanyIdBankAccountsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .call();

        if (res.companyBankAccounts().isPresent()) {
            System.out.println(res.companyBankAccounts().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompaniesCompanyIdBankAccountsHeaderXGustoAPIVersion>](../../models/operations/GetV1CompaniesCompanyIdBankAccountsHeaderXGustoAPIVersion.md)                                                                 | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |

### Response

**[GetV1CompaniesCompanyIdBankAccountsResponse](../../models/operations/GetV1CompaniesCompanyIdBankAccountsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## create

This endpoint creates a new company bank account.

Upon being created, two verification deposits are automatically sent to the bank account, and the bank account's verification_status is 'awaiting_deposits'.

When the deposits are successfully transferred, the verification_status changes to 'ready_for_verification', at which point the verify endpoint can be used to verify the bank account.
After successful verification, the bank account's verification_status is 'verified'.


>🚧 Warning
>
> If a default bank account exists, it will be disabled and the new bank account will replace it as the company's default funding method.

scope: `company_bank_accounts:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-bank-accounts" method="post" path="/v1/companies/{company_id}/bank_accounts" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyBankAccountRequest;
import com.gusto.embedded_api.models.components.CompanyBankAccountRequestAccountType;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdBankAccountsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdBankAccountsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyIdBankAccountsResponse res = sdk.bankAccounts().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdBankAccountsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .companyBankAccountRequest(CompanyBankAccountRequest.builder()
                    .routingNumber("<value>")
                    .accountNumber("<value>")
                    .accountType(CompanyBankAccountRequestAccountType.SAVINGS)
                    .build())
                .call();

        if (res.companyBankAccount().isPresent()) {
            System.out.println(res.companyBankAccount().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompaniesCompanyIdBankAccountsHeaderXGustoAPIVersion>](../../models/operations/PostV1CompaniesCompanyIdBankAccountsHeaderXGustoAPIVersion.md)                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `companyBankAccountRequest`                                                                                                                                                                                                  | [CompanyBankAccountRequest](../../models/components/CompanyBankAccountRequest.md)                                                                                                                                            | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompaniesCompanyIdBankAccountsResponse](../../models/operations/PostV1CompaniesCompanyIdBankAccountsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## verify

Verify a company bank account by confirming the two micro-deposits sent to the bank account.

Note that the order of the two deposits specified in request parameters does not matter.
There's a maximum of 5 verification attempts, after which we will automatically initiate a new set of micro-deposits and require the bank account to be verified with the new micro-deposits.

### Bank account verification in demo
In the demo environment, use the `POST /v1/companies/{company_id}/bank_accounts/{bank_account_uuid}/send_test_deposits` endpoint to simulate the micro-deposits transfer and return the two amounts in the response. You can call this endpoint as many times as you wish to retrieve the values of the two micro-deposits.

### Webhooks
- `company.bank_account.verified`: Fires when the company bank account is successfully verified.

### Related guides
- [Manage company bank accounts](doc:manage-company-bank-accounts)
- [Bank Account Events](doc:bank-account-events)

scope: `company_bank_accounts:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_id-bank-accounts-verify" method="put" path="/v1/companies/{company_id}/bank_accounts/{bank_account_uuid}/verify" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyBankAccountVerifyRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyIdBankAccountsVerifyHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyIdBankAccountsVerifyResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompaniesCompanyIdBankAccountsVerifyResponse res = sdk.bankAccounts().verify()
                .xGustoAPIVersion(PutV1CompaniesCompanyIdBankAccountsVerifyHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .bankAccountUuid("<id>")
                .companyBankAccountVerifyRequest(CompanyBankAccountVerifyRequest.builder()
                    .deposit1(8299.3f)
                    .deposit2(7367.9f)
                    .build())
                .call();

        if (res.companyBankAccount().isPresent()) {
            System.out.println(res.companyBankAccount().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_id-bank-accounts-verify" method="put" path="/v1/companies/{company_id}/bank_accounts/{bank_account_uuid}/verify" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyBankAccountVerifyRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyIdBankAccountsVerifyHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyIdBankAccountsVerifyResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompaniesCompanyIdBankAccountsVerifyResponse res = sdk.bankAccounts().verify()
                .xGustoAPIVersion(PutV1CompaniesCompanyIdBankAccountsVerifyHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .bankAccountUuid("<id>")
                .companyBankAccountVerifyRequest(CompanyBankAccountVerifyRequest.builder()
                    .deposit1(0.02f)
                    .deposit2(0.42f)
                    .build())
                .call();

        if (res.companyBankAccount().isPresent()) {
            System.out.println(res.companyBankAccount().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_id-bank-accounts-verify" method="put" path="/v1/companies/{company_id}/bank_accounts/{bank_account_uuid}/verify" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyBankAccountVerifyRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyIdBankAccountsVerifyHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyIdBankAccountsVerifyResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompaniesCompanyIdBankAccountsVerifyResponse res = sdk.bankAccounts().verify()
                .xGustoAPIVersion(PutV1CompaniesCompanyIdBankAccountsVerifyHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .bankAccountUuid("<id>")
                .companyBankAccountVerifyRequest(CompanyBankAccountVerifyRequest.builder()
                    .deposit1(8299.3f)
                    .deposit2(7367.9f)
                    .build())
                .call();

        if (res.companyBankAccount().isPresent()) {
            System.out.println(res.companyBankAccount().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_id-bank-accounts-verify" method="put" path="/v1/companies/{company_id}/bank_accounts/{bank_account_uuid}/verify" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyBankAccountVerifyRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyIdBankAccountsVerifyHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyIdBankAccountsVerifyResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompaniesCompanyIdBankAccountsVerifyResponse res = sdk.bankAccounts().verify()
                .xGustoAPIVersion(PutV1CompaniesCompanyIdBankAccountsVerifyHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .bankAccountUuid("<id>")
                .companyBankAccountVerifyRequest(CompanyBankAccountVerifyRequest.builder()
                    .deposit1(8299.3f)
                    .deposit2(7367.9f)
                    .build())
                .call();

        if (res.companyBankAccount().isPresent()) {
            System.out.println(res.companyBankAccount().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1CompaniesCompanyIdBankAccountsVerifyHeaderXGustoAPIVersion>](../../models/operations/PutV1CompaniesCompanyIdBankAccountsVerifyHeaderXGustoAPIVersion.md)                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `bankAccountUuid`                                                                                                                                                                                                            | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company bank account                                                                                                                                                                                         |
| `companyBankAccountVerifyRequest`                                                                                                                                                                                            | [CompanyBankAccountVerifyRequest](../../models/components/CompanyBankAccountVerifyRequest.md)                                                                                                                                | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1CompaniesCompanyIdBankAccountsVerifyResponse](../../models/operations/PutV1CompaniesCompanyIdBankAccountsVerifyResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## createFromPlaidToken

This endpoint creates a new **verified** bank account by using a plaid processor token to retrieve its information.

> 📘
> To create a token please use the [plaid api](https://plaid.com/docs/api/processors/#processortokencreate) and select "gusto" as processor.

> 🚧 Warning - Company Bank Accounts
>
> If a default company bank account exists, it will be disabled and the new bank account will replace it as the company's default funding method.

scope: `plaid_processor:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="post-v1-plaid-processor_token" method="post" path="/v1/plaid/processor_token" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.OwnerType;
import com.gusto.embedded_api.models.components.PlaidProcessorTokenRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1PlaidProcessorTokenHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1PlaidProcessorTokenResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1PlaidProcessorTokenResponse res = sdk.bankAccounts().createFromPlaidToken()
                .xGustoAPIVersion(PostV1PlaidProcessorTokenHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .plaidProcessorTokenRequest(PlaidProcessorTokenRequest.builder()
                    .ownerType(OwnerType.COMPANY)
                    .ownerId("<id>")
                    .processorToken("<value>")
                    .build())
                .call();

        if (res.companyBankAccount().isPresent()) {
            System.out.println(res.companyBankAccount().get());
        }
    }
}
```
### Example Usage: Create a company bank account

<!-- UsageSnippet language="java" operationID="post-v1-plaid-processor_token" method="post" path="/v1/plaid/processor_token" example="Create a company bank account" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.OwnerType;
import com.gusto.embedded_api.models.components.PlaidProcessorTokenRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1PlaidProcessorTokenHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1PlaidProcessorTokenResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1PlaidProcessorTokenResponse res = sdk.bankAccounts().createFromPlaidToken()
                .xGustoAPIVersion(PostV1PlaidProcessorTokenHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .plaidProcessorTokenRequest(PlaidProcessorTokenRequest.builder()
                    .ownerType(OwnerType.COMPANY)
                    .ownerId("ef279fbd-0fc6-4cf1-a977-6939d621c429")
                    .processorToken("processor-sandbox-0asd1-a92nc")
                    .build())
                .call();

        if (res.companyBankAccount().isPresent()) {
            System.out.println(res.companyBankAccount().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="post-v1-plaid-processor_token" method="post" path="/v1/plaid/processor_token" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.OwnerType;
import com.gusto.embedded_api.models.components.PlaidProcessorTokenRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1PlaidProcessorTokenHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1PlaidProcessorTokenResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1PlaidProcessorTokenResponse res = sdk.bankAccounts().createFromPlaidToken()
                .xGustoAPIVersion(PostV1PlaidProcessorTokenHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .plaidProcessorTokenRequest(PlaidProcessorTokenRequest.builder()
                    .ownerType(OwnerType.COMPANY)
                    .ownerId("<id>")
                    .processorToken("<value>")
                    .build())
                .call();

        if (res.companyBankAccount().isPresent()) {
            System.out.println(res.companyBankAccount().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="post-v1-plaid-processor_token" method="post" path="/v1/plaid/processor_token" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.OwnerType;
import com.gusto.embedded_api.models.components.PlaidProcessorTokenRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1PlaidProcessorTokenHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1PlaidProcessorTokenResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1PlaidProcessorTokenResponse res = sdk.bankAccounts().createFromPlaidToken()
                .xGustoAPIVersion(PostV1PlaidProcessorTokenHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .plaidProcessorTokenRequest(PlaidProcessorTokenRequest.builder()
                    .ownerType(OwnerType.COMPANY)
                    .ownerId("<id>")
                    .processorToken("<value>")
                    .build())
                .call();

        if (res.companyBankAccount().isPresent()) {
            System.out.println(res.companyBankAccount().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1PlaidProcessorTokenHeaderXGustoAPIVersion>](../../models/operations/PostV1PlaidProcessorTokenHeaderXGustoAPIVersion.md)                                                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `plaidProcessorTokenRequest`                                                                                                                                                                                                 | [PlaidProcessorTokenRequest](../../models/components/PlaidProcessorTokenRequest.md)                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1PlaidProcessorTokenResponse](../../models/operations/PostV1PlaidProcessorTokenResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## deleteV1CompaniesCompanyIdBankAccountsBankAccountId

This endpoint disables a company bank account.

A bank account cannot be disabled if it is used for any unprocessed payments.

scope: `company_bank_accounts:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-companies-company_id-bank-accounts-bank_account_id" method="delete" path="/v1/companies/{company_id}/bank_accounts/{bank_account_id}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.DeleteV1CompaniesCompanyIdBankAccountsBankAccountIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.DeleteV1CompaniesCompanyIdBankAccountsBankAccountIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1CompaniesCompanyIdBankAccountsBankAccountIdResponse res = sdk.bankAccounts().deleteV1CompaniesCompanyIdBankAccountsBankAccountId()
                .xGustoAPIVersion(DeleteV1CompaniesCompanyIdBankAccountsBankAccountIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .bankAccountId("<id>")
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1CompaniesCompanyIdBankAccountsBankAccountIdHeaderXGustoAPIVersion>](../../models/operations/DeleteV1CompaniesCompanyIdBankAccountsBankAccountIdHeaderXGustoAPIVersion.md)                                 | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `bankAccountId`                                                                                                                                                                                                              | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company bank account                                                                                                                                                                                         |

### Response

**[DeleteV1CompaniesCompanyIdBankAccountsBankAccountIdResponse](../../models/operations/DeleteV1CompaniesCompanyIdBankAccountsBankAccountIdResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |