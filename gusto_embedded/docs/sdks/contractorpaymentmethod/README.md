# ContractorPaymentMethod

## Overview

### Available Operations

* [getBankAccounts](#getbankaccounts) - Get all contractor bank accounts
* [get](#get) - Get a contractor's payment method
* [update](#update) - Update a contractor's payment method

## getBankAccounts

Returns all contractor bank accounts.

scope: `contractor_payment_methods:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-contractors-contractor_uuid-bank_accounts" method="get" path="/v1/contractors/{contractor_uuid}/bank_accounts" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1ContractorsContractorUuidBankAccountsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1ContractorsContractorUuidBankAccountsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1ContractorsContractorUuidBankAccountsResponse res = sdk.contractorPaymentMethod().getBankAccounts()
                .xGustoAPIVersion(GetV1ContractorsContractorUuidBankAccountsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .contractorUuid("<id>")
                .call();

        if (res.contractorBankAccountList().isPresent()) {
            System.out.println(res.contractorBankAccountList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1ContractorsContractorUuidBankAccountsHeaderXGustoAPIVersion>](../../models/operations/GetV1ContractorsContractorUuidBankAccountsHeaderXGustoAPIVersion.md)                                                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `contractorUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor                                                                                                                                                                                                   |

### Response

**[GetV1ContractorsContractorUuidBankAccountsResponse](../../models/operations/GetV1ContractorsContractorUuidBankAccountsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## get

Fetches a contractor's payment method. A contractor payment method
describes how the payment should be split across the contractor's associated
bank accounts.

scope: `contractor_payment_methods:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-contractors-contractor_uuid-payment_method" method="get" path="/v1/contractors/{contractor_uuid}/payment_method" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1ContractorsContractorUuidPaymentMethodHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1ContractorsContractorUuidPaymentMethodResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1ContractorsContractorUuidPaymentMethodResponse res = sdk.contractorPaymentMethod().get()
                .xGustoAPIVersion(GetV1ContractorsContractorUuidPaymentMethodHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .contractorUuid("<id>")
                .call();

        if (res.contractorPaymentMethod().isPresent()) {
            System.out.println(res.contractorPaymentMethod().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1ContractorsContractorUuidPaymentMethodHeaderXGustoAPIVersion>](../../models/operations/GetV1ContractorsContractorUuidPaymentMethodHeaderXGustoAPIVersion.md)                                                 | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `contractorUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor                                                                                                                                                                                                   |

### Response

**[GetV1ContractorsContractorUuidPaymentMethodResponse](../../models/operations/GetV1ContractorsContractorUuidPaymentMethodResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## update

Updates a contractor's payment method. Note that creating a contractor
bank account will also update the contractor's payment method.

scope: `contractor_payment_methods:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-contractors-contractor_id-payment_method" method="put" path="/v1/contractors/{contractor_uuid}/payment_method" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.*;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, ConflictErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1ContractorsContractorIdPaymentMethodResponse res = sdk.contractorPaymentMethod().update()
                .xGustoAPIVersion(PutV1ContractorsContractorIdPaymentMethodHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .contractorUuid("<id>")
                .requestBody(PutV1ContractorsContractorIdPaymentMethodRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .type(PutV1ContractorsContractorIdPaymentMethodType.DIRECT_DEPOSIT)
                    .build())
                .call();

        if (res.contractorPaymentMethod().isPresent()) {
            System.out.println(res.contractorPaymentMethod().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-contractors-contractor_id-payment_method" method="put" path="/v1/contractors/{contractor_uuid}/payment_method" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.*;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, ConflictErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1ContractorsContractorIdPaymentMethodResponse res = sdk.contractorPaymentMethod().update()
                .xGustoAPIVersion(PutV1ContractorsContractorIdPaymentMethodHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .contractorUuid("<id>")
                .requestBody(PutV1ContractorsContractorIdPaymentMethodRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .type(PutV1ContractorsContractorIdPaymentMethodType.DIRECT_DEPOSIT)
                    .build())
                .call();

        if (res.contractorPaymentMethod().isPresent()) {
            System.out.println(res.contractorPaymentMethod().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-contractors-contractor_id-payment_method" method="put" path="/v1/contractors/{contractor_uuid}/payment_method" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.*;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, ConflictErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1ContractorsContractorIdPaymentMethodResponse res = sdk.contractorPaymentMethod().update()
                .xGustoAPIVersion(PutV1ContractorsContractorIdPaymentMethodHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .contractorUuid("<id>")
                .requestBody(PutV1ContractorsContractorIdPaymentMethodRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .type(PutV1ContractorsContractorIdPaymentMethodType.DIRECT_DEPOSIT)
                    .build())
                .call();

        if (res.contractorPaymentMethod().isPresent()) {
            System.out.println(res.contractorPaymentMethod().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-contractors-contractor_id-payment_method" method="put" path="/v1/contractors/{contractor_uuid}/payment_method" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.*;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, ConflictErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1ContractorsContractorIdPaymentMethodResponse res = sdk.contractorPaymentMethod().update()
                .xGustoAPIVersion(PutV1ContractorsContractorIdPaymentMethodHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .contractorUuid("<id>")
                .requestBody(PutV1ContractorsContractorIdPaymentMethodRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .type(PutV1ContractorsContractorIdPaymentMethodType.DIRECT_DEPOSIT)
                    .build())
                .call();

        if (res.contractorPaymentMethod().isPresent()) {
            System.out.println(res.contractorPaymentMethod().get());
        }
    }
}
```
### Example Usage: example-1

<!-- UsageSnippet language="java" operationID="put-v1-contractors-contractor_id-payment_method" method="put" path="/v1/contractors/{contractor_uuid}/payment_method" example="example-1" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.*;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, ConflictErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1ContractorsContractorIdPaymentMethodResponse res = sdk.contractorPaymentMethod().update()
                .xGustoAPIVersion(PutV1ContractorsContractorIdPaymentMethodHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .contractorUuid("<id>")
                .requestBody(PutV1ContractorsContractorIdPaymentMethodRequestBody.builder()
                    .version("63859768485e218ccf8a449bb60f14ed")
                    .type(PutV1ContractorsContractorIdPaymentMethodType.DIRECT_DEPOSIT)
                    .build())
                .call();

        if (res.contractorPaymentMethod().isPresent()) {
            System.out.println(res.contractorPaymentMethod().get());
        }
    }
}
```
### Example Usage: example-3

<!-- UsageSnippet language="java" operationID="put-v1-contractors-contractor_id-payment_method" method="put" path="/v1/contractors/{contractor_uuid}/payment_method" example="example-3" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.*;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, ConflictErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1ContractorsContractorIdPaymentMethodResponse res = sdk.contractorPaymentMethod().update()
                .xGustoAPIVersion(PutV1ContractorsContractorIdPaymentMethodHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .contractorUuid("<id>")
                .requestBody(PutV1ContractorsContractorIdPaymentMethodRequestBody.builder()
                    .version("63859768485e218ccf8a449bb60f14ed")
                    .type(PutV1ContractorsContractorIdPaymentMethodType.CHECK)
                    .build())
                .call();

        if (res.contractorPaymentMethod().isPresent()) {
            System.out.println(res.contractorPaymentMethod().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1ContractorsContractorIdPaymentMethodHeaderXGustoAPIVersion>](../../models/operations/PutV1ContractorsContractorIdPaymentMethodHeaderXGustoAPIVersion.md)                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `contractorUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the contractor                                                                                                                                                                                                   |
| `requestBody`                                                                                                                                                                                                                | [PutV1ContractorsContractorIdPaymentMethodRequestBody](../../models/operations/PutV1ContractorsContractorIdPaymentMethodRequestBody.md)                                                                                      | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1ContractorsContractorIdPaymentMethodResponse](../../models/operations/PutV1ContractorsContractorIdPaymentMethodResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/ConflictErrorObject      | 409                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |