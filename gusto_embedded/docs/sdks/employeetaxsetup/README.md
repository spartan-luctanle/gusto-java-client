# EmployeeTaxSetup

## Overview

### Available Operations

* [getFederalTaxes](#getfederaltaxes) - Get federal taxes for an employee
* [updateFederalTaxes](#updatefederaltaxes) - Update federal taxes for an employee
* [getStateTaxes](#getstatetaxes) - Get an employee's state taxes
* [updateStateTaxes](#updatestatetaxes) - Update an employee's state taxes

## getFederalTaxes

Returns federal tax information for an employee. The response structure varies based on the w4_data_type (pre_2020_w4 or rev_2020_w4).

scope: `employee_federal_taxes:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees-employee_id-federal_taxes" method="get" path="/v1/employees/{employee_uuid}/federal_taxes" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeFederalTax;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdFederalTaxesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdFederalTaxesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesEmployeeIdFederalTaxesResponse res = sdk.employeeTaxSetup().getFederalTaxes()
                .xGustoAPIVersion(GetV1EmployeesEmployeeIdFederalTaxesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeUuid("<id>")
                .call();

        if (res.employeeFederalTax().isPresent()) {
            EmployeeFederalTax unionValue = res.employeeFederalTax().get();
            switch (unionValue.w4DataType()) {
                case "pre_2020_w4":
                    // Handle pre_2020_w4 discriminator variant
                    break;
                case "rev_2020_w4":
                    // Handle rev_2020_w4 discriminator variant
                    break;
                default:
                    // Handle unknown discriminator variant
            }
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1EmployeesEmployeeIdFederalTaxesHeaderXGustoAPIVersion>](../../models/operations/GetV1EmployeesEmployeeIdFederalTaxesHeaderXGustoAPIVersion.md)                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeUuid`                                                                                                                                                                                                               | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |

### Response

**[GetV1EmployeesEmployeeIdFederalTaxesResponse](../../models/operations/GetV1EmployeesEmployeeIdFederalTaxesResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## updateFederalTaxes

Updates federal tax (W4) information for an employee. Only rev_2020_w4 format is accepted for updates.

scope: `employee_federal_taxes:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-federal_taxes" method="put" path="/v1/employees/{employee_uuid}/federal_taxes" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeFederalTax;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdFederalTaxesResponse res = sdk.employeeTaxSetup().updateFederalTaxes()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdFederalTaxesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeUuid("<id>")
                .requestBody(PutV1EmployeesEmployeeIdFederalTaxesRequestBody.builder()
                    .version("<value>")
                    .w4DataType()
                    .filingStatus()
                    .build())
                .call();

        if (res.employeeFederalTax().isPresent()) {
            EmployeeFederalTax unionValue = res.employeeFederalTax().get();
            switch (unionValue.w4DataType()) {
                case "pre_2020_w4":
                    // Handle pre_2020_w4 discriminator variant
                    break;
                case "rev_2020_w4":
                    // Handle rev_2020_w4 discriminator variant
                    break;
                default:
                    // Handle unknown discriminator variant
            }
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-federal_taxes" method="put" path="/v1/employees/{employee_uuid}/federal_taxes" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeFederalTax;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdFederalTaxesResponse res = sdk.employeeTaxSetup().updateFederalTaxes()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdFederalTaxesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeUuid("<id>")
                .requestBody(PutV1EmployeesEmployeeIdFederalTaxesRequestBody.builder()
                    .version("56a489ce86ed6c1b0f0cecc4050a0b01")
                    .w4DataType(W4DataType.REV2020_W4)
                    .filingStatus(FilingStatus.SINGLE)
                    .twoJobs(true)
                    .dependentsAmount(0.0)
                    .otherIncome(0.0)
                    .deductions(0.0)
                    .extraWithholding(0.0)
                    .build())
                .call();

        if (res.employeeFederalTax().isPresent()) {
            EmployeeFederalTax unionValue = res.employeeFederalTax().get();
            switch (unionValue.w4DataType()) {
                case "pre_2020_w4":
                    // Handle pre_2020_w4 discriminator variant
                    break;
                case "rev_2020_w4":
                    // Handle rev_2020_w4 discriminator variant
                    break;
                default:
                    // Handle unknown discriminator variant
            }
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-federal_taxes" method="put" path="/v1/employees/{employee_uuid}/federal_taxes" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeFederalTax;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdFederalTaxesResponse res = sdk.employeeTaxSetup().updateFederalTaxes()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdFederalTaxesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeUuid("<id>")
                .requestBody(PutV1EmployeesEmployeeIdFederalTaxesRequestBody.builder()
                    .version("<value>")
                    .w4DataType()
                    .filingStatus()
                    .build())
                .call();

        if (res.employeeFederalTax().isPresent()) {
            EmployeeFederalTax unionValue = res.employeeFederalTax().get();
            switch (unionValue.w4DataType()) {
                case "pre_2020_w4":
                    // Handle pre_2020_w4 discriminator variant
                    break;
                case "rev_2020_w4":
                    // Handle rev_2020_w4 discriminator variant
                    break;
                default:
                    // Handle unknown discriminator variant
            }
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-federal_taxes" method="put" path="/v1/employees/{employee_uuid}/federal_taxes" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeFederalTax;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdFederalTaxesResponse res = sdk.employeeTaxSetup().updateFederalTaxes()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdFederalTaxesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeUuid("<id>")
                .requestBody(PutV1EmployeesEmployeeIdFederalTaxesRequestBody.builder()
                    .version("<value>")
                    .w4DataType()
                    .filingStatus()
                    .build())
                .call();

        if (res.employeeFederalTax().isPresent()) {
            EmployeeFederalTax unionValue = res.employeeFederalTax().get();
            switch (unionValue.w4DataType()) {
                case "pre_2020_w4":
                    // Handle pre_2020_w4 discriminator variant
                    break;
                case "rev_2020_w4":
                    // Handle rev_2020_w4 discriminator variant
                    break;
                default:
                    // Handle unknown discriminator variant
            }
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1EmployeesEmployeeIdFederalTaxesHeaderXGustoAPIVersion>](../../models/operations/PutV1EmployeesEmployeeIdFederalTaxesHeaderXGustoAPIVersion.md)                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeUuid`                                                                                                                                                                                                               | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `requestBody`                                                                                                                                                                                                                | [PutV1EmployeesEmployeeIdFederalTaxesRequestBody](../../models/operations/PutV1EmployeesEmployeeIdFederalTaxesRequestBody.md)                                                                                                | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1EmployeesEmployeeIdFederalTaxesResponse](../../models/operations/PutV1EmployeesEmployeeIdFederalTaxesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 409, 422                               | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getStateTaxes

Get attributes relevant for an employee's state taxes.

The data required to correctly calculate an employee's state taxes varies by both home and work location. This API returns information about each question that must be answered grouped by state. Mostly commonly, an employee lives and works in the same state and will only have questions for a single state. The response contains metadata about each question, the type of answer expected, and the current answer stored in Gusto for that question.

Answers are represented by an array. Today, this array can only be empty or contain exactly one element, but is designed to allow for forward compatibility with effective-dated fields. The `valid_from` and `valid_up_to` fields are optional and currently ignored.

## About filing new hire reports
Payroll Admins are responsible for filing a new hire report for each Employee. The `file_new_hire_report` question will only be listed if:
- the `employee.onboarding_status` is one of the following:
  - `admin_onboarding_incomplete`
  - `self_onboarding_awaiting_admin_review`
- that employee's work state requires filing a new hire report

scope: `employee_state_taxes:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees-employee_id-state_taxes" method="get" path="/v1/employees/{employee_uuid}/state_taxes" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdStateTaxesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1EmployeesEmployeeIdStateTaxesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesEmployeeIdStateTaxesResponse res = sdk.employeeTaxSetup().getStateTaxes()
                .xGustoAPIVersion(GetV1EmployeesEmployeeIdStateTaxesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeUuid("<id>")
                .call();

        if (res.employeeStateTaxesList().isPresent()) {
            System.out.println(res.employeeStateTaxesList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1EmployeesEmployeeIdStateTaxesHeaderXGustoAPIVersion>](../../models/operations/GetV1EmployeesEmployeeIdStateTaxesHeaderXGustoAPIVersion.md)                                                                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeUuid`                                                                                                                                                                                                               | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |

### Response

**[GetV1EmployeesEmployeeIdStateTaxesResponse](../../models/operations/GetV1EmployeesEmployeeIdStateTaxesResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## updateStateTaxes

Update attributes relevant for an employee's state taxes.

As described for the GET endpoint, the answers must be supplied in the effective-dated format, but currently only a single answer will be accepted. The `valid_from` and `valid_up_to` fields are optional and currently ignored.

scope: `employee_state_taxes:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-state_taxes" method="put" path="/v1/employees/{employee_uuid}/state_taxes" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeStateTaxesRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1EmployeesEmployeeIdStateTaxesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1EmployeesEmployeeIdStateTaxesResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdStateTaxesResponse res = sdk.employeeTaxSetup().updateStateTaxes()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdStateTaxesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .employeeUuid("<id>")
                .employeeStateTaxesRequest(EmployeeStateTaxesRequest.builder()
                    .states(List.of())
                    .build())
                .call();

        if (res.employeeStateTaxesList().isPresent()) {
            System.out.println(res.employeeStateTaxesList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1EmployeesEmployeeIdStateTaxesHeaderXGustoAPIVersion>](../../models/operations/PutV1EmployeesEmployeeIdStateTaxesHeaderXGustoAPIVersion.md)                                                                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeUuid`                                                                                                                                                                                                               | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `employeeStateTaxesRequest`                                                                                                                                                                                                  | [EmployeeStateTaxesRequest](../../models/components/EmployeeStateTaxesRequest.md)                                                                                                                                            | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1EmployeesEmployeeIdStateTaxesResponse](../../models/operations/PutV1EmployeesEmployeeIdStateTaxesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |