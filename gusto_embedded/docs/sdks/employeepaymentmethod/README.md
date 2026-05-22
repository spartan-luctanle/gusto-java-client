# EmployeePaymentMethod

## Overview

### Available Operations

* [create](#create) - Create an employee bank account
* [updateBankAccount](#updatebankaccount) - Update an employee bank account
* [deleteBankAccount](#deletebankaccount) - Delete an employee bank account
* [get](#get) - Get payment method for an employee
* [update](#update) - Update payment method for an employee

## create

Creates an employee bank account. An employee can have multiple bank accounts. Note that creating an employee bank account will also update the employee's payment method.

scope: `employee_payment_methods:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-bank_accounts" method="post" path="/v1/employees/{employee_id}/bank_accounts" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBankAccountRequest;
import com.gusto.embedded_api.models.components.EmployeeBankAccountRequestAccountType;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdBankAccountsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdBankAccountsResponse res = sdk.employeePaymentMethod().create()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .employeeBankAccountRequest(EmployeeBankAccountRequest.builder()
                    .routingNumber("<value>")
                    .accountNumber("<value>")
                    .accountType(EmployeeBankAccountRequestAccountType.CHECKING)
                    .name("<value>")
                    .build())
                .call();

        if (res.employeeBankAccount().isPresent()) {
            System.out.println(res.employeeBankAccount().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-bank_accounts" method="post" path="/v1/employees/{employee_id}/bank_accounts" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBankAccountRequest;
import com.gusto.embedded_api.models.components.EmployeeBankAccountRequestAccountType;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdBankAccountsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdBankAccountsResponse res = sdk.employeePaymentMethod().create()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .employeeBankAccountRequest(EmployeeBankAccountRequest.builder()
                    .routingNumber("266905059")
                    .accountNumber("5809431207")
                    .accountType(EmployeeBankAccountRequestAccountType.CHECKING)
                    .name("BoA Checking Account")
                    .build())
                .call();

        if (res.employeeBankAccount().isPresent()) {
            System.out.println(res.employeeBankAccount().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-bank_accounts" method="post" path="/v1/employees/{employee_id}/bank_accounts" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBankAccountRequest;
import com.gusto.embedded_api.models.components.EmployeeBankAccountRequestAccountType;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdBankAccountsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdBankAccountsResponse res = sdk.employeePaymentMethod().create()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .employeeBankAccountRequest(EmployeeBankAccountRequest.builder()
                    .routingNumber("<value>")
                    .accountNumber("<value>")
                    .accountType(EmployeeBankAccountRequestAccountType.CHECKING)
                    .name("<value>")
                    .build())
                .call();

        if (res.employeeBankAccount().isPresent()) {
            System.out.println(res.employeeBankAccount().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-bank_accounts" method="post" path="/v1/employees/{employee_id}/bank_accounts" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBankAccountRequest;
import com.gusto.embedded_api.models.components.EmployeeBankAccountRequestAccountType;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1EmployeesEmployeeIdBankAccountsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdBankAccountsResponse res = sdk.employeePaymentMethod().create()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .employeeBankAccountRequest(EmployeeBankAccountRequest.builder()
                    .routingNumber("<value>")
                    .accountNumber("<value>")
                    .accountType(EmployeeBankAccountRequestAccountType.CHECKING)
                    .name("<value>")
                    .build())
                .call();

        if (res.employeeBankAccount().isPresent()) {
            System.out.println(res.employeeBankAccount().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion>](../../models/operations/PostV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion.md)                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `employeeBankAccountRequest`                                                                                                                                                                                                 | [EmployeeBankAccountRequest](../../models/components/EmployeeBankAccountRequest.md)                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1EmployeesEmployeeIdBankAccountsResponse](../../models/operations/PostV1EmployeesEmployeeIdBankAccountsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## updateBankAccount

Updates an employee bank account.

scope: `employee_payment_methods:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-bank_accounts" method="put" path="/v1/employees/{employee_id}/bank_accounts/{bank_account_uuid}" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBankAccountRequest;
import com.gusto.embedded_api.models.components.EmployeeBankAccountRequestAccountType;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1EmployeesEmployeeIdBankAccountsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdBankAccountsResponse res = sdk.employeePaymentMethod().updateBankAccount()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .bankAccountUuid("<id>")
                .employeeBankAccountRequest(EmployeeBankAccountRequest.builder()
                    .routingNumber("<value>")
                    .accountNumber("<value>")
                    .accountType(EmployeeBankAccountRequestAccountType.SAVINGS)
                    .name("<value>")
                    .build())
                .call();

        if (res.employeeBankAccount().isPresent()) {
            System.out.println(res.employeeBankAccount().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-bank_accounts" method="put" path="/v1/employees/{employee_id}/bank_accounts/{bank_account_uuid}" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBankAccountRequest;
import com.gusto.embedded_api.models.components.EmployeeBankAccountRequestAccountType;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1EmployeesEmployeeIdBankAccountsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdBankAccountsResponse res = sdk.employeePaymentMethod().updateBankAccount()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .bankAccountUuid("<id>")
                .employeeBankAccountRequest(EmployeeBankAccountRequest.builder()
                    .routingNumber("266905059")
                    .accountNumber("5809431207")
                    .accountType(EmployeeBankAccountRequestAccountType.CHECKING)
                    .name("BoA Checking Account")
                    .build())
                .call();

        if (res.employeeBankAccount().isPresent()) {
            System.out.println(res.employeeBankAccount().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-bank_accounts" method="put" path="/v1/employees/{employee_id}/bank_accounts/{bank_account_uuid}" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBankAccountRequest;
import com.gusto.embedded_api.models.components.EmployeeBankAccountRequestAccountType;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1EmployeesEmployeeIdBankAccountsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdBankAccountsResponse res = sdk.employeePaymentMethod().updateBankAccount()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .bankAccountUuid("<id>")
                .employeeBankAccountRequest(EmployeeBankAccountRequest.builder()
                    .routingNumber("<value>")
                    .accountNumber("<value>")
                    .accountType(EmployeeBankAccountRequestAccountType.SAVINGS)
                    .name("<value>")
                    .build())
                .call();

        if (res.employeeBankAccount().isPresent()) {
            System.out.println(res.employeeBankAccount().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-bank_accounts" method="put" path="/v1/employees/{employee_id}/bank_accounts/{bank_account_uuid}" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBankAccountRequest;
import com.gusto.embedded_api.models.components.EmployeeBankAccountRequestAccountType;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1EmployeesEmployeeIdBankAccountsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdBankAccountsResponse res = sdk.employeePaymentMethod().updateBankAccount()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .bankAccountUuid("<id>")
                .employeeBankAccountRequest(EmployeeBankAccountRequest.builder()
                    .routingNumber("<value>")
                    .accountNumber("<value>")
                    .accountType(EmployeeBankAccountRequestAccountType.SAVINGS)
                    .name("<value>")
                    .build())
                .call();

        if (res.employeeBankAccount().isPresent()) {
            System.out.println(res.employeeBankAccount().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion>](../../models/operations/PutV1EmployeesEmployeeIdBankAccountsHeaderXGustoAPIVersion.md)                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `bankAccountUuid`                                                                                                                                                                                                            | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the bank account                                                                                                                                                                                                 |
| `employeeBankAccountRequest`                                                                                                                                                                                                 | [EmployeeBankAccountRequest](../../models/components/EmployeeBankAccountRequest.md)                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1EmployeesEmployeeIdBankAccountsResponse](../../models/operations/PutV1EmployeesEmployeeIdBankAccountsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## deleteBankAccount

Deletes an employee bank account. To update an employee's bank account details, delete the bank account first and create a new one.

scope: `employee_payment_methods:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-employees-employee_id-bank_accounts-bank_account_id" method="delete" path="/v1/employees/{employee_id}/bank_accounts/{bank_account_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.operations.DeleteV1EmployeesEmployeeIdBankAccountsBankAccountIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.DeleteV1EmployeesEmployeeIdBankAccountsBankAccountIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1EmployeesEmployeeIdBankAccountsBankAccountIdResponse res = sdk.employeePaymentMethod().deleteBankAccount()
                .xGustoAPIVersion(DeleteV1EmployeesEmployeeIdBankAccountsBankAccountIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .bankAccountUuid("<id>")
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1EmployeesEmployeeIdBankAccountsBankAccountIdHeaderXGustoAPIVersion>](../../models/operations/DeleteV1EmployeesEmployeeIdBankAccountsBankAccountIdHeaderXGustoAPIVersion.md)                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `bankAccountUuid`                                                                                                                                                                                                            | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the bank account                                                                                                                                                                                                 |

### Response

**[DeleteV1EmployeesEmployeeIdBankAccountsBankAccountIdResponse](../../models/operations/DeleteV1EmployeesEmployeeIdBankAccountsBankAccountIdResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |

## get

Returns the payment method for an employee (e.g. Check or Direct Deposit with split configuration).

scope: `employee_payment_methods:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees-employee_id-payment_method" method="get" path="/v1/employees/{employee_id}/payment_method" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdPaymentMethodHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdPaymentMethodResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesEmployeeIdPaymentMethodResponse res = sdk.employeePaymentMethod().get()
                .xGustoAPIVersion(GetV1EmployeesEmployeeIdPaymentMethodHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .call();

        if (res.employeePaymentMethod().isPresent()) {
            System.out.println(res.employeePaymentMethod().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1EmployeesEmployeeIdPaymentMethodHeaderXGustoAPIVersion>](../../models/operations/GetV1EmployeesEmployeeIdPaymentMethodHeaderXGustoAPIVersion.md)                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |

### Response

**[GetV1EmployeesEmployeeIdPaymentMethodResponse](../../models/operations/GetV1EmployeesEmployeeIdPaymentMethodResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## update

Updates the payment method for an employee. Can set to Check or Direct Deposit with split configuration.

scope: `employee_payment_methods:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-payment_method" method="put" path="/v1/employees/{employee_id}/payment_method" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdPaymentMethodResponse res = sdk.employeePaymentMethod().update()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdPaymentMethodHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .requestBody(PutV1EmployeesEmployeeIdPaymentMethodRequestBody.builder()
                    .version("<value>")
                    .type(Type.DIRECT_DEPOSIT)
                    .build())
                .call();

        if (res.employeePaymentMethod().isPresent()) {
            System.out.println(res.employeePaymentMethod().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-payment_method" method="put" path="/v1/employees/{employee_id}/payment_method" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdPaymentMethodResponse res = sdk.employeePaymentMethod().update()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdPaymentMethodHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .requestBody(PutV1EmployeesEmployeeIdPaymentMethodRequestBody.builder()
                    .version("<value>")
                    .type(Type.DIRECT_DEPOSIT)
                    .build())
                .call();

        if (res.employeePaymentMethod().isPresent()) {
            System.out.println(res.employeePaymentMethod().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-payment_method" method="put" path="/v1/employees/{employee_id}/payment_method" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdPaymentMethodResponse res = sdk.employeePaymentMethod().update()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdPaymentMethodHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .requestBody(PutV1EmployeesEmployeeIdPaymentMethodRequestBody.builder()
                    .version("<value>")
                    .type(Type.DIRECT_DEPOSIT)
                    .build())
                .call();

        if (res.employeePaymentMethod().isPresent()) {
            System.out.println(res.employeePaymentMethod().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-payment_method" method="put" path="/v1/employees/{employee_id}/payment_method" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdPaymentMethodResponse res = sdk.employeePaymentMethod().update()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdPaymentMethodHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .requestBody(PutV1EmployeesEmployeeIdPaymentMethodRequestBody.builder()
                    .version("<value>")
                    .type(Type.DIRECT_DEPOSIT)
                    .build())
                .call();

        if (res.employeePaymentMethod().isPresent()) {
            System.out.println(res.employeePaymentMethod().get());
        }
    }
}
```
### Example Usage: example-1

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-payment_method" method="put" path="/v1/employees/{employee_id}/payment_method" example="example-1" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;
import java.util.List;
import org.openapitools.jackson.nullable.JsonNullable;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdPaymentMethodResponse res = sdk.employeePaymentMethod().update()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdPaymentMethodHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .requestBody(PutV1EmployeesEmployeeIdPaymentMethodRequestBody.builder()
                    .version("63859768485e218ccf8a449bb60f14ed")
                    .type(Type.DIRECT_DEPOSIT)
                    .splitBy(SplitBy.AMOUNT)
                    .splits(List.of(
                        Splits.builder()
                            .uuid("e88f9436-b74e-49a8-87e9-777b9bfe715e")
                            .name("BoA Checking Account")
                            .priority(1L)
                            .splitAmount(50000d)
                            .build(),
                        Splits.builder()
                            .uuid("0d2b7f73-05d6-4184-911d-269edeecc30a")
                            .name("Chase Checking Account")
                            .priority(2L)
                            .splitAmount(100000d)
                            .build(),
                        Splits.builder()
                            .uuid("1531e824-8d9e-4bd8-9f90-0d04608125d7")
                            .name("US Bank Checking Account")
                            .priority(3L)
                            .splitAmount(JsonNullable.of(null))
                            .build()))
                    .build())
                .call();

        if (res.employeePaymentMethod().isPresent()) {
            System.out.println(res.employeePaymentMethod().get());
        }
    }
}
```
### Example Usage: example-2

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-payment_method" method="put" path="/v1/employees/{employee_id}/payment_method" example="example-2" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdPaymentMethodResponse res = sdk.employeePaymentMethod().update()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdPaymentMethodHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .requestBody(PutV1EmployeesEmployeeIdPaymentMethodRequestBody.builder()
                    .version("63859768485e218ccf8a449bb60f14ed")
                    .type(Type.DIRECT_DEPOSIT)
                    .splitBy(SplitBy.PERCENTAGE)
                    .splits(List.of(
                        Splits.builder()
                            .uuid("e88f9436-b74e-49a8-87e9-777b9bfe715e")
                            .name("BoA Checking Account")
                            .priority(1L)
                            .splitAmount(60d)
                            .build(),
                        Splits.builder()
                            .uuid("0d2b7f73-05d6-4184-911d-269edeecc30a")
                            .name("Chase Checking Account")
                            .priority(2L)
                            .splitAmount(40d)
                            .build()))
                    .build())
                .call();

        if (res.employeePaymentMethod().isPresent()) {
            System.out.println(res.employeePaymentMethod().get());
        }
    }
}
```
### Example Usage: example-3

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-payment_method" method="put" path="/v1/employees/{employee_id}/payment_method" example="example-3" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdPaymentMethodResponse res = sdk.employeePaymentMethod().update()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdPaymentMethodHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeId("<id>")
                .requestBody(PutV1EmployeesEmployeeIdPaymentMethodRequestBody.builder()
                    .version("63859768485e218ccf8a449bb60f14ed")
                    .type(Type.CHECK)
                    .build())
                .call();

        if (res.employeePaymentMethod().isPresent()) {
            System.out.println(res.employeePaymentMethod().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1EmployeesEmployeeIdPaymentMethodHeaderXGustoAPIVersion>](../../models/operations/PutV1EmployeesEmployeeIdPaymentMethodHeaderXGustoAPIVersion.md)                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `requestBody`                                                                                                                                                                                                                | [PutV1EmployeesEmployeeIdPaymentMethodRequestBody](../../models/operations/PutV1EmployeesEmployeeIdPaymentMethodRequestBody.md)                                                                                              | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1EmployeesEmployeeIdPaymentMethodResponse](../../models/operations/PutV1EmployeesEmployeeIdPaymentMethodResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 409, 422                               | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |