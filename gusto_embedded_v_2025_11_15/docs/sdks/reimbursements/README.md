# Reimbursements

## Overview

### Available Operations

* [getV1EmployeesEmployeeIdRecurringReimbursements](#getv1employeesemployeeidrecurringreimbursements) - Get recurring reimbursements for an employee
* [postV1EmployeesEmployeeIdRecurringReimbursements](#postv1employeesemployeeidrecurringreimbursements) - Create a recurring reimbursement
* [getV1RecurringReimbursements](#getv1recurringreimbursements) - Get a recurring reimbursement
* [putV1RecurringReimbursements](#putv1recurringreimbursements) - Update a recurring reimbursement
* [deleteV1RecurringReimbursements](#deletev1recurringreimbursements) - Delete a recurring reimbursement

## getV1EmployeesEmployeeIdRecurringReimbursements

Get all active recurring reimbursements for an employee.

scope: `reimbursements:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees-employee_id-recurring_reimbursements" method="get" path="/v1/employees/{employee_id}/recurring_reimbursements" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1EmployeesEmployeeIdRecurringReimbursementsHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1EmployeesEmployeeIdRecurringReimbursementsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesEmployeeIdRecurringReimbursementsResponse res = sdk.reimbursements().getV1EmployeesEmployeeIdRecurringReimbursements()
                .xGustoAPIVersion(GetV1EmployeesEmployeeIdRecurringReimbursementsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .employeeId("<id>")
                .call();

        if (res.recurringReimbursementList().isPresent()) {
            System.out.println(res.recurringReimbursementList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1EmployeesEmployeeIdRecurringReimbursementsHeaderXGustoAPIVersion>](../../models/operations/GetV1EmployeesEmployeeIdRecurringReimbursementsHeaderXGustoAPIVersion.md)                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `page`                                                                                                                                                                                                                       | *Optional\<Long>*                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                           | The page that is requested. When unspecified, will load all objects unless endpoint forces pagination.                                                                                                                       |
| `per`                                                                                                                                                                                                                        | *Optional\<Long>*                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                           | Number of objects per page. For majority of endpoints will default to 25                                                                                                                                                     |

### Response

**[GetV1EmployeesEmployeeIdRecurringReimbursementsResponse](../../models/operations/GetV1EmployeesEmployeeIdRecurringReimbursementsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## postV1EmployeesEmployeeIdRecurringReimbursements

Create a recurring reimbursement for an employee.

scope: `reimbursements:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-employees-employee_id-recurring_reimbursements" method="post" path="/v1/employees/{employee_id}/recurring_reimbursements" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesEmployeeIdRecurringReimbursementsResponse res = sdk.reimbursements().postV1EmployeesEmployeeIdRecurringReimbursements()
                .xGustoAPIVersion(PostV1EmployeesEmployeeIdRecurringReimbursementsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .employeeId("<id>")
                .requestBody(PostV1EmployeesEmployeeIdRecurringReimbursementsRequestBody.builder()
                    .description("as procrastinate produce provided gracefully huzzah likewise when")
                    .amount(2610.77)
                    .build())
                .call();

        if (res.recurringReimbursement().isPresent()) {
            System.out.println(res.recurringReimbursement().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1EmployeesEmployeeIdRecurringReimbursementsHeaderXGustoAPIVersion>](../../models/operations/PostV1EmployeesEmployeeIdRecurringReimbursementsHeaderXGustoAPIVersion.md)                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `requestBody`                                                                                                                                                                                                                | [PostV1EmployeesEmployeeIdRecurringReimbursementsRequestBody](../../models/operations/PostV1EmployeesEmployeeIdRecurringReimbursementsRequestBody.md)                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1EmployeesEmployeeIdRecurringReimbursementsResponse](../../models/operations/PostV1EmployeesEmployeeIdRecurringReimbursementsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404, 422                          | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## getV1RecurringReimbursements

Get a specific recurring reimbursement.

scope: `reimbursements:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-recurring_reimbursements" method="get" path="/v1/recurring_reimbursements/{id}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1RecurringReimbursementsHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1RecurringReimbursementsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1RecurringReimbursementsResponse res = sdk.reimbursements().getV1RecurringReimbursements()
                .xGustoAPIVersion(GetV1RecurringReimbursementsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .id("<id>")
                .call();

        if (res.recurringReimbursement().isPresent()) {
            System.out.println(res.recurringReimbursement().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1RecurringReimbursementsHeaderXGustoAPIVersion>](../../models/operations/GetV1RecurringReimbursementsHeaderXGustoAPIVersion.md)                                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `id`                                                                                                                                                                                                                         | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the reimbursement                                                                                                                                                                                                |

### Response

**[GetV1RecurringReimbursementsResponse](../../models/operations/GetV1RecurringReimbursementsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## putV1RecurringReimbursements

Update a recurring reimbursement.

scope: `reimbursements:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-recurring_reimbursements" method="put" path="/v1/recurring_reimbursements/{id}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1RecurringReimbursementsResponse res = sdk.reimbursements().putV1RecurringReimbursements()
                .xGustoAPIVersion(PutV1RecurringReimbursementsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .id("<id>")
                .requestBody(PutV1RecurringReimbursementsRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .build())
                .call();

        if (res.recurringReimbursement().isPresent()) {
            System.out.println(res.recurringReimbursement().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1RecurringReimbursementsHeaderXGustoAPIVersion>](../../models/operations/PutV1RecurringReimbursementsHeaderXGustoAPIVersion.md)                                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `id`                                                                                                                                                                                                                         | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the reimbursement                                                                                                                                                                                                |
| `requestBody`                                                                                                                                                                                                                | [PutV1RecurringReimbursementsRequestBody](../../models/operations/PutV1RecurringReimbursementsRequestBody.md)                                                                                                                | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1RecurringReimbursementsResponse](../../models/operations/PutV1RecurringReimbursementsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404, 409, 422                     | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## deleteV1RecurringReimbursements

Delete (soft delete) a recurring reimbursement for an employee.

scope: `reimbursements:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-recurring_reimbursements" method="delete" path="/v1/recurring_reimbursements/{id}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.DeleteV1RecurringReimbursementsHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.DeleteV1RecurringReimbursementsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1RecurringReimbursementsResponse res = sdk.reimbursements().deleteV1RecurringReimbursements()
                .xGustoAPIVersion(DeleteV1RecurringReimbursementsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .id("<id>")
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1RecurringReimbursementsHeaderXGustoAPIVersion>](../../models/operations/DeleteV1RecurringReimbursementsHeaderXGustoAPIVersion.md)                                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `id`                                                                                                                                                                                                                         | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the reimbursement                                                                                                                                                                                                |

### Response

**[DeleteV1RecurringReimbursementsResponse](../../models/operations/DeleteV1RecurringReimbursementsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |