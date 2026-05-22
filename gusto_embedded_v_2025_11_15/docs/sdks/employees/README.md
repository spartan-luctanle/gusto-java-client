# Employees

## Overview

### Available Operations

* [list](#list) - Get employees of a company
* [create](#create) - Create an employee
* [getV1CompaniesCompanyIdEmployeesPaymentDetails](#getv1companiescompanyidemployeespaymentdetails) - Get employee payment details for a company
* [createHistorical](#createhistorical) - Create a historical employee
* [get](#get) - Get an employee
* [update](#update) - Update an employee.
* [delete](#delete) - Delete an onboarding employee
* [getCustomFields](#getcustomfields) - Get an employee's custom fields
* [updateOnboardingDocumentsConfig](#updateonboardingdocumentsconfig) - Update employee onboarding documents config
* [getOnboardingStatus](#getonboardingstatus) - Get the employee's onboarding status
* [updateOnboardingStatus](#updateonboardingstatus) - Update the employee's onboarding status
* [getTimeOffActivities](#gettimeoffactivities) - Get employee time off activities

## list

Get all of the employees, onboarding, active and terminated, for a given company.

Note: Compensation data (pay rate, payment unit, and related fields) represents sensitive employee pay information. When retrieving employee job data, these fields (`rate`, `payment_unit`, `current_compensation_uuid`, `compensations`) are only returned when the `compensations:read` scope is included. This allows you to access employee and job metadata without exposing pay rates.

scope: `employees:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_id-employees" method="get" path="/v1/companies/{company_id}/employees" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdEmployeesRequest;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdEmployeesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyIdEmployeesRequest req = GetV1CompaniesCompanyIdEmployeesRequest.builder()
                .companyId("<id>")
                .sortBy("name:desc")
                .build();

        GetV1CompaniesCompanyIdEmployeesResponse res = sdk.employees().list()
                .request(req)
                .call();

        if (res.showEmployees().isPresent()) {
            System.out.println(res.showEmployees().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                     | Type                                                                                                          | Required                                                                                                      | Description                                                                                                   |
| ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| `request`                                                                                                     | [GetV1CompaniesCompanyIdEmployeesRequest](../../models/operations/GetV1CompaniesCompanyIdEmployeesRequest.md) | :heavy_check_mark:                                                                                            | The request object to use for the request.                                                                    |

### Response

**[GetV1CompaniesCompanyIdEmployeesResponse](../../models/operations/GetV1CompaniesCompanyIdEmployeesResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## create

Create an employee.

scope: `employees:manage`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-employees" method="post" path="/v1/companies/{company_id}/employees" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1EmployeesHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1EmployeesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1EmployeesResponse res = sdk.employees().create()
                .xGustoAPIVersion(PostV1EmployeesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyId("<id>")
                .call();

        if (res.employee().isPresent()) {
            System.out.println(res.employee().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1EmployeesHeaderXGustoAPIVersion>](../../models/operations/PostV1EmployeesHeaderXGustoAPIVersion.md)                                                                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | Company ID                                                                                                                                                                                                                   |
| `requestBody`                                                                                                                                                                                                                | [Optional\<PostV1EmployeesRequestBody>](../../models/operations/PostV1EmployeesRequestBody.md)                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1EmployeesResponse](../../models/operations/PostV1EmployeesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getV1CompaniesCompanyIdEmployeesPaymentDetails

Fetches payment details for employees in a given company. Results are paginated.

Use the `employee_uuid` query parameter to filter for a single employee.
Use the `payroll_uuid` query parameter to filter for employees on a specific payroll.
Providing both `employee_uuid` and `payroll_uuid` will result in a 422 error.
An empty array is returned if the company has no employees or if no employees match the filter criteria.

The `encrypted_account_number` in the `splits` array is only visible if the `employee_payment_methods:read:account_number` scope is present.

scope: `employee_payment_methods:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_id-employees-payment_details" method="get" path="/v1/companies/{company_id}/employees/payment_details" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdEmployeesPaymentDetailsRequest;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyIdEmployeesPaymentDetailsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyIdEmployeesPaymentDetailsRequest req = GetV1CompaniesCompanyIdEmployeesPaymentDetailsRequest.builder()
                .companyId("<id>")
                .build();

        GetV1CompaniesCompanyIdEmployeesPaymentDetailsResponse res = sdk.employees().getV1CompaniesCompanyIdEmployeesPaymentDetails()
                .request(req)
                .call();

        if (res.employeePaymentDetailsList().isPresent()) {
            System.out.println(res.employeePaymentDetailsList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                 | Type                                                                                                                                      | Required                                                                                                                                  | Description                                                                                                                               |
| ----------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `request`                                                                                                                                 | [GetV1CompaniesCompanyIdEmployeesPaymentDetailsRequest](../../models/operations/GetV1CompaniesCompanyIdEmployeesPaymentDetailsRequest.md) | :heavy_check_mark:                                                                                                                        | The request object to use for the request.                                                                                                |

### Response

**[GetV1CompaniesCompanyIdEmployeesPaymentDetailsResponse](../../models/operations/GetV1CompaniesCompanyIdEmployeesPaymentDetailsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## createHistorical

Create a historical employee, an employee that was previously dismissed from the company in the current year.

scope: `employees:manage`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-historical_employees" method="post" path="/v1/companies/{company_uuid}/historical_employees" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.*;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1HistoricalEmployeesHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1HistoricalEmployeesResponse;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1HistoricalEmployeesResponse res = sdk.employees().createHistorical()
                .xGustoAPIVersion(PostV1HistoricalEmployeesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyUuid("7b1d0df1-6403-4a06-8768-c1dd7d24d27a")
                .historicalEmployeeBody(HistoricalEmployeeBody.builder()
                    .firstName("Soren")
                    .lastName("Kierkegaard")
                    .dateOfBirth(LocalDate.parse("1995-05-05"))
                    .ssn("123456294")
                    .workAddress(WorkAddress.builder()
                        .locationUuid("1da85d35-1910-40a7-9c1f-8e2b3d4c5a6f")
                        .build())
                    .homeAddress(HistoricalEmployeeBodyHomeAddress.builder()
                        .street1("55 Mission St")
                        .city("San Francisco")
                        .state("CA")
                        .zip("94105")
                        .street2("Floor 3")
                        .build())
                    .termination(HistoricalEmployeeBodyTermination.builder()
                        .effectiveDate(LocalDate.parse("2022-01-01"))
                        .build())
                    .job(HistoricalEmployeeBodyJob.builder()
                        .hireDate(LocalDate.parse("2020-01-01"))
                        .build())
                    .middleInitial("A")
                    .preferredFirstName("Angel")
                    .email("soren.kierkegaard@example.com")
                    .employeeStateTaxes(EmployeeStateTaxes.builder()
                        .wcCovered(true)
                        .wcClassCode("051000")
                        .build())
                    .build())
                .call();

        if (res.employee().isPresent()) {
            System.out.println(res.employee().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  | Example                                                                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1HistoricalEmployeesHeaderXGustoAPIVersion>](../../models/operations/PostV1HistoricalEmployeesHeaderXGustoAPIVersion.md)                                                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |                                                                                                                                                                                                                              |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company that will employ this historical record.                                                                                                                                                             | 7b1d0df1-6403-4a06-8768-c1dd7d24d27a                                                                                                                                                                                         |
| `historicalEmployeeBody`                                                                                                                                                                                                     | [HistoricalEmployeeBody](../../models/components/HistoricalEmployeeBody.md)                                                                                                                                                  | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |                                                                                                                                                                                                                              |

### Response

**[PostV1HistoricalEmployeesResponse](../../models/operations/PostV1HistoricalEmployeesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## get

Get an employee.

Note: Compensation data (pay rate, payment unit, and related fields) represents sensitive employee pay information. When retrieving employee job data, these fields (`rate`, `payment_unit`, `current_compensation_uuid`, `compensations`) are only returned when the `compensations:read` scope is included. This allows you to access employee and job metadata without exposing pay rates.

scope: `employees:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees" method="get" path="/v1/employees/{employee_id}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1EmployeesHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1EmployeesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesResponse res = sdk.employees().get()
                .xGustoAPIVersion(GetV1EmployeesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .employeeId("<id>")
                .call();

        if (res.employee().isPresent()) {
            System.out.println(res.employee().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1EmployeesHeaderXGustoAPIVersion>](../../models/operations/GetV1EmployeesHeaderXGustoAPIVersion.md)                                                                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `include`                                                                                                                                                                                                                    | List\<[QueryParamInclude](../../models/operations/QueryParamInclude.md)>                                                                                                                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Include the requested attribute(s) in each employee response. Multiple options are comma separated.                                                                                                                          |

### Response

**[GetV1EmployeesResponse](../../models/operations/GetV1EmployeesResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## update

Update an employee.

scope: `employees:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-employees" method="put" path="/v1/employees/{employee_id}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesResponse res = sdk.employees().update()
                .xGustoAPIVersion(PutV1EmployeesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .employeeId("<id>")
                .requestBody(PutV1EmployeesRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .firstName("Weezy")
                    .middleInitial("F")
                    .lastName("Baby")
                    .email("tunechi@cashmoneyrecords.com")
                    .workEmail("new.partner.work@example.com")
                    .dateOfBirth("1991-01-31")
                    .ssn("824920233")
                    .build())
                .call();

        if (res.employee().isPresent()) {
            System.out.println(res.employee().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1EmployeesHeaderXGustoAPIVersion>](../../models/operations/PutV1EmployeesHeaderXGustoAPIVersion.md)                                                                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `requestBody`                                                                                                                                                                                                                | [PutV1EmployeesRequestBody](../../models/operations/PutV1EmployeesRequestBody.md)                                                                                                                                            | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1EmployeesResponse](../../models/operations/PutV1EmployeesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 409, 422                               | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## delete

Use this endpoint to delete an employee who is in onboarding. Deleting
an onboarded employee is not allowed and will return a 422 response. Please check out the Terminations api
if you need to terminate an onboarded employee.

scope: `employees:manage`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-employee" method="delete" path="/v1/employees/{employee_id}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.DeleteV1EmployeeHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.DeleteV1EmployeeResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1EmployeeResponse res = sdk.employees().delete()
                .xGustoAPIVersion(DeleteV1EmployeeHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .employeeId("<id>")
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1EmployeeHeaderXGustoAPIVersion>](../../models/operations/DeleteV1EmployeeHeaderXGustoAPIVersion.md)                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |

### Response

**[DeleteV1EmployeeResponse](../../models/operations/DeleteV1EmployeeResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getCustomFields

Returns a list of the employee's custom fields.

scope: `employees:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees-employee_id-custom_fields" method="get" path="/v1/employees/{employee_id}/custom_fields" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1EmployeesEmployeeIdCustomFieldsHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1EmployeesEmployeeIdCustomFieldsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesEmployeeIdCustomFieldsResponse res = sdk.employees().getCustomFields()
                .employeeId("<id>")
                .xGustoAPIVersion(GetV1EmployeesEmployeeIdCustomFieldsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .call();

        if (res.employeeCustomFieldList().isPresent()) {
            System.out.println(res.employeeCustomFieldList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `page`                                                                                                                                                                                                                       | *Optional\<Long>*                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                           | The page that is requested. When unspecified, will load all objects unless endpoint forces pagination.                                                                                                                       |
| `per`                                                                                                                                                                                                                        | *Optional\<Long>*                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                           | Number of objects per page. For majority of endpoints will default to 25                                                                                                                                                     |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1EmployeesEmployeeIdCustomFieldsHeaderXGustoAPIVersion>](../../models/operations/GetV1EmployeesEmployeeIdCustomFieldsHeaderXGustoAPIVersion.md)                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1EmployeesEmployeeIdCustomFieldsResponse](../../models/operations/GetV1EmployeesEmployeeIdCustomFieldsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## updateOnboardingDocumentsConfig

Indicate whether to include the Form I-9 for an employee during the onboarding process.
If included, the employee will be prompted to complete Form I-9 as part of their onboarding.

## Related guides
- [Employee onboarding](doc:employee-onboarding)

scope: `employees:manage`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-onboarding_documents_config" method="put" path="/v1/employees/{employee_id}/onboarding_documents_config" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1EmployeesEmployeeIdOnboardingDocumentsConfigHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1EmployeesEmployeeIdOnboardingDocumentsConfigResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdOnboardingDocumentsConfigResponse res = sdk.employees().updateOnboardingDocumentsConfig()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdOnboardingDocumentsConfigHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .employeeId("7b1d0df1-6403-4a06-8768-c1dd7d24d27a")
                .call();

        if (res.employeeOnboardingDocument().isPresent()) {
            System.out.println(res.employeeOnboardingDocument().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  | Example                                                                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1EmployeesEmployeeIdOnboardingDocumentsConfigHeaderXGustoAPIVersion>](../../models/operations/PutV1EmployeesEmployeeIdOnboardingDocumentsConfigHeaderXGustoAPIVersion.md)                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |                                                                                                                                                                                                                              |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     | 7b1d0df1-6403-4a06-8768-c1dd7d24d27a                                                                                                                                                                                         |
| `employeeOnboardingDocumentsConfigRequest`                                                                                                                                                                                   | [Optional\<EmployeeOnboardingDocumentsConfigRequest>](../../models/components/EmployeeOnboardingDocumentsConfigRequest.md)                                                                                                   | :heavy_minus_sign:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |                                                                                                                                                                                                                              |

### Response

**[PutV1EmployeesEmployeeIdOnboardingDocumentsConfigResponse](../../models/operations/PutV1EmployeesEmployeeIdOnboardingDocumentsConfigResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## getOnboardingStatus

# Description
Retrieves an employee's onboarding status. The data returned helps inform the required onboarding steps and respective completion status.


## onboarding_status

### Admin-facilitated onboarding
| onboarding_status | Description |
|:------------------|------------:|
| `admin_onboarding_incomplete` | Admin needs to complete the full employee-onboarding. |
| `onboarding_completed` | Employee has been fully onboarded and verified. |

### Employee self-onboarding
| onboarding_status | Description |
|:------------------|------------:|
| `admin_onboarding_incomplete` | Admin needs to enter basic information about the employee. |
| `self_onboarding_pending_invite` | Admin has the intention to invite the employee to self-onboard (e.g., marking a checkbox), but the system has not yet sent the invitation. |
| `self_onboarding_invited` | Employee has been sent an invitation to self-onboard. |
| `self_onboarding_invited_started` | Employee has started the self-onboarding process. |
| `self_onboarding_invited_overdue` | Employee's start date has passed, and employee has still not completed self-onboarding. |
| `self_onboarding_completed_by_employee` | Employee has completed entering in their information. The status should be updated via API to "self_onboarding_awaiting_admin_review" from here, once the Admin has started reviewing. |
| `self_onboarding_awaiting_admin_review` | Admin has started to verify the employee's information. |
| `onboarding_completed` | Employee has been fully onboarded and verified. |

## onboarding_steps

| onboarding_steps | Requirement(s) to be completed |
|:-----------------|-------------------------------:|
| `personal_details` | Add employee's first name, last name, email, date of birth, social security number |
| `compensation_details` | Associate employee to a job & compensation. |
| `add_work_address` | Add employee work address. |
| `add_home_address` | Add employee home address. |
| `federal_tax_setup` | Set up federal tax withholdings. |
| `state_tax_setup` | Set up state tax withholdings. |
| `direct_deposit_setup` | (optional) Set up employee's direct deposit. |
| `employee_form_signing` | Employee forms (e.g., W4, direct deposit authorization) are generated & signed. |
| `file_new_hire_report` | File a new hire report for this employee. |
| `admin_review` | Admin reviews & confirms employee details (only required for Employee self-onboarding) |

scope: `employees:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees-employee_id-onboarding_status" method="get" path="/v1/employees/{employee_id}/onboarding_status" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1EmployeesEmployeeIdOnboardingStatusHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1EmployeesEmployeeIdOnboardingStatusResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesEmployeeIdOnboardingStatusResponse res = sdk.employees().getOnboardingStatus()
                .xGustoAPIVersion(GetV1EmployeesEmployeeIdOnboardingStatusHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .employeeId("<id>")
                .call();

        if (res.employeeOnboardingStatus().isPresent()) {
            System.out.println(res.employeeOnboardingStatus().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1EmployeesEmployeeIdOnboardingStatusHeaderXGustoAPIVersion>](../../models/operations/GetV1EmployeesEmployeeIdOnboardingStatusHeaderXGustoAPIVersion.md)                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |

### Response

**[GetV1EmployeesEmployeeIdOnboardingStatusResponse](../../models/operations/GetV1EmployeesEmployeeIdOnboardingStatusResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## updateOnboardingStatus

Updates an employee's onboarding status.
Below is a list of valid onboarding status changes depending on the intended action to be performed on behalf of the employee.

| Action | current onboarding_status | new onboarding_status |
|:------------------|:------------:|----------:|
| Mark an employee as self-onboarding | `admin_onboarding_incomplete` | `self_onboarding_pending_invite` |
| Invite an employee to self-onboard | `admin_onboarding_incomplete` or `self_onboarding_pending_invite` | `self_onboarding_invited` |
| Cancel an employee's self-onboarding | `self_onboarding_invited` or `self_onboarding_pending_invite` | `admin_onboarding_incomplete` |
| Review an employee's self-onboarded info | `self_onboarding_completed_by_employee` | `self_onboarding_awaiting_admin_review` |
| Finish an employee's onboarding | `admin_onboarding_incomplete` or `self_onboarding_awaiting_admin_review` | `onboarding_completed` |

scope: `employees:manage`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-onboarding_status" method="put" path="/v1/employees/{employee_id}/onboarding_status" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdOnboardingStatusResponse res = sdk.employees().updateOnboardingStatus()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdOnboardingStatusHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .employeeId("<id>")
                .requestBody(PutV1EmployeesEmployeeIdOnboardingStatusRequestBody.builder()
                    .onboardingStatus(OnboardingStatus.ADMIN_ONBOARDING_INCOMPLETE)
                    .build())
                .call();

        if (res.employeeOnboardingStatus().isPresent()) {
            System.out.println(res.employeeOnboardingStatus().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1EmployeesEmployeeIdOnboardingStatusHeaderXGustoAPIVersion>](../../models/operations/PutV1EmployeesEmployeeIdOnboardingStatusHeaderXGustoAPIVersion.md)                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `requestBody`                                                                                                                                                                                                                | [PutV1EmployeesEmployeeIdOnboardingStatusRequestBody](../../models/operations/PutV1EmployeesEmployeeIdOnboardingStatusRequestBody.md)                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1EmployeesEmployeeIdOnboardingStatusResponse](../../models/operations/PutV1EmployeesEmployeeIdOnboardingStatusResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getTimeOffActivities

Get employee time off activities.

scope: `employee_time_off_activities:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-version-employees-time_off_activities" method="get" path="/v1/employees/{employee_uuid}/time_off_activities" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetVersionEmployeesTimeOffActivitiesHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetVersionEmployeesTimeOffActivitiesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetVersionEmployeesTimeOffActivitiesResponse res = sdk.employees().getTimeOffActivities()
                .xGustoAPIVersion(GetVersionEmployeesTimeOffActivitiesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .employeeUuid("<id>")
                .timeOffType("<value>")
                .call();

        if (res.timeOffActivityList().isPresent()) {
            System.out.println(res.timeOffActivityList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetVersionEmployeesTimeOffActivitiesHeaderXGustoAPIVersion>](../../models/operations/GetVersionEmployeesTimeOffActivitiesHeaderXGustoAPIVersion.md)                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeUuid`                                                                                                                                                                                                               | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `timeOffType`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The time off type name you want to query data for. ex: 'sick' or 'vacation'                                                                                                                                                  |

### Response

**[GetVersionEmployeesTimeOffActivitiesResponse](../../models/operations/GetVersionEmployeesTimeOffActivitiesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |