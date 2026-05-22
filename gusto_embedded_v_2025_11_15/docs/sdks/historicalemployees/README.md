# HistoricalEmployees

## Overview

### Available Operations

* [update](#update) - Update a historical employee

## update

Update a historical employee, an employee that was previously dismissed from the company in the current year.

scope: `employees:manage employees:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-historical_employees" method="put" path="/v1/companies/{company_uuid}/historical_employees/{historical_employee_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1HistoricalEmployeesResponse res = sdk.historicalEmployees().update()
                .xGustoAPIVersion(PutV1HistoricalEmployeesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyUuid("7b1d0df1-6403-4a06-8768-c1dd7d24d27a")
                .historicalEmployeeUuid("a2b3c4d-5e6f-7890-abcd-ef1234567890")
                .requestBody(PutV1HistoricalEmployeesRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .firstName("Soren")
                    .lastName("Kierkegaard")
                    .dateOfBirth(LocalDate.parse("1995-05-05"))
                    .ssn("123456294")
                    .workAddress(WorkAddress.builder()
                        .locationUuid("1da85d35-1910-40a7-9c1f-8e2b3d4c5a6f")
                        .build())
                    .homeAddress(HomeAddress.builder()
                        .street1("55 Mission St")
                        .city("San Francisco")
                        .state("CA")
                        .zip("94105")
                        .street2("Floor 3")
                        .build())
                    .termination(Termination.builder()
                        .effectiveDate(LocalDate.parse("2022-01-01"))
                        .build())
                    .job(Job.builder()
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
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1HistoricalEmployeesHeaderXGustoAPIVersion>](../../models/operations/PutV1HistoricalEmployeesHeaderXGustoAPIVersion.md)                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |                                                                                                                                                                                                                              |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company that will employ this historical record.                                                                                                                                                             | 7b1d0df1-6403-4a06-8768-c1dd7d24d27a                                                                                                                                                                                         |
| `historicalEmployeeUuid`                                                                                                                                                                                                     | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the historical employee returned from create or list responses.                                                                                                                                                  | a2b3c4d-5e6f-7890-abcd-ef1234567890                                                                                                                                                                                          |
| `requestBody`                                                                                                                                                                                                                | [PutV1HistoricalEmployeesRequestBody](../../models/operations/PutV1HistoricalEmployeesRequestBody.md)                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |                                                                                                                                                                                                                              |

### Response

**[PutV1HistoricalEmployeesResponse](../../models/operations/PutV1HistoricalEmployeesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |