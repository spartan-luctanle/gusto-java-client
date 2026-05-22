# HolidayPayPolicies

## Overview

### Available Operations

* [get](#get) - Get a company's holiday pay policy
* [create](#create) - Create a holiday pay policy for a company
* [update](#update) - Update a company's holiday pay policy
* [delete](#delete) - Delete a company's holiday pay policy
* [addEmployees](#addemployees) - Add employees to a company's holiday pay policy
* [removeEmployees](#removeemployees) - Remove employees from a company's holiday pay policy
* [previewPaidHolidays](#previewpaidholidays) - Preview a company's paid holidays

## get

Get a company's holiday pay policy

scope: `holiday_pay_policies:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_uuid-holiday_pay_policy" method="get" path="/v1/companies/{company_uuid}/holiday_pay_policy" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyUuidHolidayPayPolicyHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesCompanyUuidHolidayPayPolicyResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyUuidHolidayPayPolicyResponse res = sdk.holidayPayPolicies().get()
                .xGustoAPIVersion(GetV1CompaniesCompanyUuidHolidayPayPolicyHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyUuid("<id>")
                .call();

        if (res.holidayPayPolicy().isPresent()) {
            System.out.println(res.holidayPayPolicy().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompaniesCompanyUuidHolidayPayPolicyHeaderXGustoAPIVersion>](../../models/operations/GetV1CompaniesCompanyUuidHolidayPayPolicyHeaderXGustoAPIVersion.md)                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |

### Response

**[GetV1CompaniesCompanyUuidHolidayPayPolicyResponse](../../models/operations/GetV1CompaniesCompanyUuidHolidayPayPolicyResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## create

Create a holiday pay policy for a company

scope: `holiday_pay_policies:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_uuid-holiday_pay_policy" method="post" path="/v1/companies/{company_uuid}/holiday_pay_policy" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1CompaniesCompanyUuidHolidayPayPolicyHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1CompaniesCompanyUuidHolidayPayPolicyResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyUuidHolidayPayPolicyResponse res = sdk.holidayPayPolicies().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyUuidHolidayPayPolicyHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyUuid("<id>")
                .call();

        if (res.holidayPayPolicy().isPresent()) {
            System.out.println(res.holidayPayPolicy().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompaniesCompanyUuidHolidayPayPolicyHeaderXGustoAPIVersion>](../../models/operations/PostV1CompaniesCompanyUuidHolidayPayPolicyHeaderXGustoAPIVersion.md)                                                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `holidayPayPolicyRequest`                                                                                                                                                                                                    | [Optional\<HolidayPayPolicyRequest>](../../models/components/HolidayPayPolicyRequest.md)                                                                                                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompaniesCompanyUuidHolidayPayPolicyResponse](../../models/operations/PostV1CompaniesCompanyUuidHolidayPayPolicyResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## update

Update a company's holiday pay policy

scope: `holiday_pay_policies:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_uuid-holiday_pay_policy" method="put" path="/v1/companies/{company_uuid}/holiday_pay_policy" -->
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

        PutV1CompaniesCompanyUuidHolidayPayPolicyResponse res = sdk.holidayPayPolicies().update()
                .xGustoAPIVersion(PutV1CompaniesCompanyUuidHolidayPayPolicyHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyUuid("<id>")
                .requestBody(PutV1CompaniesCompanyUuidHolidayPayPolicyRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .build())
                .call();

        if (res.holidayPayPolicy().isPresent()) {
            System.out.println(res.holidayPayPolicy().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1CompaniesCompanyUuidHolidayPayPolicyHeaderXGustoAPIVersion>](../../models/operations/PutV1CompaniesCompanyUuidHolidayPayPolicyHeaderXGustoAPIVersion.md)                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `requestBody`                                                                                                                                                                                                                | [PutV1CompaniesCompanyUuidHolidayPayPolicyRequestBody](../../models/operations/PutV1CompaniesCompanyUuidHolidayPayPolicyRequestBody.md)                                                                                      | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1CompaniesCompanyUuidHolidayPayPolicyResponse](../../models/operations/PutV1CompaniesCompanyUuidHolidayPayPolicyResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## delete

Delete a company's holiday pay policy

scope: `holiday_pay_policies:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-companies-company_uuid-holiday_pay_policy" method="delete" path="/v1/companies/{company_uuid}/holiday_pay_policy" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.DeleteV1CompaniesCompanyUuidHolidayPayPolicyHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.DeleteV1CompaniesCompanyUuidHolidayPayPolicyResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1CompaniesCompanyUuidHolidayPayPolicyResponse res = sdk.holidayPayPolicies().delete()
                .xGustoAPIVersion(DeleteV1CompaniesCompanyUuidHolidayPayPolicyHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyUuid("<id>")
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1CompaniesCompanyUuidHolidayPayPolicyHeaderXGustoAPIVersion>](../../models/operations/DeleteV1CompaniesCompanyUuidHolidayPayPolicyHeaderXGustoAPIVersion.md)                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |

### Response

**[DeleteV1CompaniesCompanyUuidHolidayPayPolicyResponse](../../models/operations/DeleteV1CompaniesCompanyUuidHolidayPayPolicyResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## addEmployees

Add employees to a company's holiday pay policy

scope: `holiday_pay_policies:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_uuid-holiday_pay_policy-add" method="put" path="/v1/companies/{company_uuid}/holiday_pay_policy/add" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompaniesCompanyUuidHolidayPayPolicyAddResponse res = sdk.holidayPayPolicies().addEmployees()
                .xGustoAPIVersion(PutV1CompaniesCompanyUuidHolidayPayPolicyAddHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyUuid("<id>")
                .requestBody(PutV1CompaniesCompanyUuidHolidayPayPolicyAddRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .employees(List.of())
                    .build())
                .call();

        if (res.holidayPayPolicy().isPresent()) {
            System.out.println(res.holidayPayPolicy().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1CompaniesCompanyUuidHolidayPayPolicyAddHeaderXGustoAPIVersion>](../../models/operations/PutV1CompaniesCompanyUuidHolidayPayPolicyAddHeaderXGustoAPIVersion.md)                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `requestBody`                                                                                                                                                                                                                | [PutV1CompaniesCompanyUuidHolidayPayPolicyAddRequestBody](../../models/operations/PutV1CompaniesCompanyUuidHolidayPayPolicyAddRequestBody.md)                                                                                | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1CompaniesCompanyUuidHolidayPayPolicyAddResponse](../../models/operations/PutV1CompaniesCompanyUuidHolidayPayPolicyAddResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## removeEmployees

Remove employees from a company's holiday pay policy

scope: `holiday_pay_policies:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_uuid-holiday_pay_policy-remove" method="put" path="/v1/companies/{company_uuid}/holiday_pay_policy/remove" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompaniesCompanyUuidHolidayPayPolicyRemoveResponse res = sdk.holidayPayPolicies().removeEmployees()
                .xGustoAPIVersion(PutV1CompaniesCompanyUuidHolidayPayPolicyRemoveHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyUuid("<id>")
                .requestBody(PutV1CompaniesCompanyUuidHolidayPayPolicyRemoveRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .employees(List.of(
                        PutV1CompaniesCompanyUuidHolidayPayPolicyRemoveEmployees.builder()
                            .build()))
                    .build())
                .call();

        if (res.holidayPayPolicy().isPresent()) {
            System.out.println(res.holidayPayPolicy().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1CompaniesCompanyUuidHolidayPayPolicyRemoveHeaderXGustoAPIVersion>](../../models/operations/PutV1CompaniesCompanyUuidHolidayPayPolicyRemoveHeaderXGustoAPIVersion.md)                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `requestBody`                                                                                                                                                                                                                | [PutV1CompaniesCompanyUuidHolidayPayPolicyRemoveRequestBody](../../models/operations/PutV1CompaniesCompanyUuidHolidayPayPolicyRemoveRequestBody.md)                                                                          | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1CompaniesCompanyUuidHolidayPayPolicyRemoveResponse](../../models/operations/PutV1CompaniesCompanyUuidHolidayPayPolicyRemoveResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## previewPaidHolidays

Preview a company's paid holidays

If a year is passed, paid holidays for that year will be returned. Otherwise, paid holidays for the next three years will be returned.

scope: `holiday_pay_policies:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-companies-company_uuid-paid_holidays" method="get" path="/v1/companies/{company_uuid}/paid_holidays" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetCompaniesCompanyUuidPaidHolidaysHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetCompaniesCompanyUuidPaidHolidaysResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetCompaniesCompanyUuidPaidHolidaysResponse res = sdk.holidayPayPolicies().previewPaidHolidays()
                .xGustoAPIVersion(GetCompaniesCompanyUuidPaidHolidaysHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyUuid("<id>")
                .year("2023")
                .call();

        if (res.paidHolidays().isPresent()) {
            System.out.println(res.paidHolidays().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  | Example                                                                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetCompaniesCompanyUuidPaidHolidaysHeaderXGustoAPIVersion>](../../models/operations/GetCompaniesCompanyUuidPaidHolidaysHeaderXGustoAPIVersion.md)                                                                 | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |                                                                                                                                                                                                                              |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |                                                                                                                                                                                                                              |
| `year`                                                                                                                                                                                                                       | *Optional\<String>*                                                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                                                           | If a year is passed, paid holidays for that year will be returned. Otherwise, paid holidays for the next three years will be returned.                                                                                       | 2023                                                                                                                                                                                                                         |

### Response

**[GetCompaniesCompanyUuidPaidHolidaysResponse](../../models/operations/GetCompaniesCompanyUuidPaidHolidaysResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |