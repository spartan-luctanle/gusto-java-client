# CompanyBenefits

## Overview

### Available Operations

* [list](#list) - Get benefits for a company
* [create](#create) - Create a company benefit
* [get](#get) - Get a company benefit
* [update](#update) - Update a company benefit
* [delete](#delete) - Delete a company benefit
* [getAll](#getall) - Get all supported benefits
* [getSupported](#getsupported) - Get a supported benefit
* [getSummary](#getsummary) - Get company benefit summary by company benefit id.
* [getEmployeeBenefits](#getemployeebenefits) - Get all employee benefits for a company benefit
* [updateEmployeeBenefits](#updateemployeebenefits) - Bulk update employee benefits for a company benefit
* [getRequirements](#getrequirements) - Get benefit fields requirements by benefit type
* [getV1CompanyBenefitsCompanyBenefitIdContributionExclusions](#getv1companybenefitscompanybenefitidcontributionexclusions) - Get contribution exclusions for a company benefit
* [putV1CompanyBenefitsCompanyBenefitIdContributionExclusions](#putv1companybenefitscompanybenefitidcontributionexclusions) - Update contribution exclusions for a company benefit

## list

Company benefits represent the benefits that a company is offering to employees. This ties together a particular supported benefit with the company-specific information for the offering of that benefit.

Note that company benefits can be deactivated only when no employees are enrolled.

Benefits containing PHI are only visible to applications with the `company_benefits:read:phi` scope.

scope: `company_benefits:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_id-company_benefits" method="get" path="/v1/companies/{company_id}/company_benefits" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyIdCompanyBenefitsRequest;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyIdCompanyBenefitsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyIdCompanyBenefitsRequest req = GetV1CompaniesCompanyIdCompanyBenefitsRequest.builder()
                .companyId("<id>")
                .build();

        GetV1CompaniesCompanyIdCompanyBenefitsResponse res = sdk.companyBenefits().list()
                .request(req)
                .call();

        if (res.companyBenefits().isPresent()) {
            System.out.println(res.companyBenefits().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                 | Type                                                                                                                      | Required                                                                                                                  | Description                                                                                                               |
| ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `request`                                                                                                                 | [GetV1CompaniesCompanyIdCompanyBenefitsRequest](../../models/operations/GetV1CompaniesCompanyIdCompanyBenefitsRequest.md) | :heavy_check_mark:                                                                                                        | The request object to use for the request.                                                                                |

### Response

**[GetV1CompaniesCompanyIdCompanyBenefitsResponse](../../models/operations/GetV1CompaniesCompanyIdCompanyBenefitsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## create

Company benefits represent the benefits that a company is offering to employees. This ties together a particular supported benefit with the company-specific information for the offering of that benefit.

Note that company benefits can be deactivated only when no employees are enrolled.

When the application has the `company_benefits:write:benefit_type_limited` data scope, the application can only create company benefits for benefit types that are permitted for the application.

scope: `company_benefits:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-company_benefits" method="post" path="/v1/companies/{company_id}/company_benefits" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyBenefitCreateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdCompanyBenefitsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdCompanyBenefitsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyIdCompanyBenefitsResponse res = sdk.companyBenefits().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdCompanyBenefitsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .companyBenefitCreateRequest(CompanyBenefitCreateRequest.builder()
                    .description("hm pfft surge beyond")
                    .build())
                .call();

        if (res.companyBenefit().isPresent()) {
            System.out.println(res.companyBenefit().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-company_benefits" method="post" path="/v1/companies/{company_id}/company_benefits" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyBenefitCreateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdCompanyBenefitsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdCompanyBenefitsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyIdCompanyBenefitsResponse res = sdk.companyBenefits().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdCompanyBenefitsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .companyBenefitCreateRequest(CompanyBenefitCreateRequest.builder()
                    .description("hm pfft surge beyond")
                    .build())
                .call();

        if (res.companyBenefit().isPresent()) {
            System.out.println(res.companyBenefit().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-company_benefits" method="post" path="/v1/companies/{company_id}/company_benefits" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyBenefitCreateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdCompanyBenefitsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdCompanyBenefitsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyIdCompanyBenefitsResponse res = sdk.companyBenefits().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdCompanyBenefitsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .companyBenefitCreateRequest(CompanyBenefitCreateRequest.builder()
                    .description("hm pfft surge beyond")
                    .build())
                .call();

        if (res.companyBenefit().isPresent()) {
            System.out.println(res.companyBenefit().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-company_benefits" method="post" path="/v1/companies/{company_id}/company_benefits" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyBenefitCreateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdCompanyBenefitsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdCompanyBenefitsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyIdCompanyBenefitsResponse res = sdk.companyBenefits().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdCompanyBenefitsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .companyBenefitCreateRequest(CompanyBenefitCreateRequest.builder()
                    .description("hm pfft surge beyond")
                    .build())
                .call();

        if (res.companyBenefit().isPresent()) {
            System.out.println(res.companyBenefit().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompaniesCompanyIdCompanyBenefitsHeaderXGustoAPIVersion>](../../models/operations/PostV1CompaniesCompanyIdCompanyBenefitsHeaderXGustoAPIVersion.md)                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `companyBenefitCreateRequest`                                                                                                                                                                                                | [CompanyBenefitCreateRequest](../../models/components/CompanyBenefitCreateRequest.md)                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompaniesCompanyIdCompanyBenefitsResponse](../../models/operations/PostV1CompaniesCompanyIdCompanyBenefitsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## get

Company benefits represent the benefits that a company is offering to employees. This ties together a particular supported benefit with the company-specific information for the offering of that benefit.

Note that company benefits can be deactivated only when no employees are enrolled.

When with_employee_benefits parameter with true value is passed, employee_benefits:read scope is required to return employee_benefits.

scope: `company_benefits:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-company_benefits-company_benefit_id" method="get" path="/v1/company_benefits/{company_benefit_id}" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1CompanyBenefitsCompanyBenefitIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1CompanyBenefitsCompanyBenefitIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompanyBenefitsCompanyBenefitIdResponse res = sdk.companyBenefits().get()
                .xGustoAPIVersion(GetV1CompanyBenefitsCompanyBenefitIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyBenefitId("<id>")
                .call();

        if (res.companyBenefitWithEmployeeBenefits().isPresent()) {
            System.out.println(res.companyBenefitWithEmployeeBenefits().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompanyBenefitsCompanyBenefitIdHeaderXGustoAPIVersion>](../../models/operations/GetV1CompanyBenefitsCompanyBenefitIdHeaderXGustoAPIVersion.md)                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyBenefitId`                                                                                                                                                                                                           | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company benefit                                                                                                                                                                                              |
| `withEmployeeBenefits`                                                                                                                                                                                                       | *Optional\<Boolean>*                                                                                                                                                                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Whether to return employee benefits associated with the benefit                                                                                                                                                              |
| `include`                                                                                                                                                                                                                    | [Optional\<GetV1CompanyBenefitsCompanyBenefitIdQueryParamInclude>](../../models/operations/GetV1CompanyBenefitsCompanyBenefitIdQueryParamInclude.md)                                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Available options:<br/>- all_benefits: If with_employee_benefits=true, include all effective dated benefits for each employee instead of only the current benefits.                                                          |

### Response

**[GetV1CompanyBenefitsCompanyBenefitIdResponse](../../models/operations/GetV1CompanyBenefitsCompanyBenefitIdResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## update

Company benefits represent the benefits that a company is offering to employees. This ties together a particular supported benefit with the company-specific information for the offering of that benefit.

Note that company benefits can be deactivated only when no employees are enrolled.

When the application has the `company_benefits:write:benefit_type_limited` data scope, the application can only update company benefits for benefit types that are permitted for the application.

scope: `company_benefits:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-company_benefits-company_benefit_id" method="put" path="/v1/company_benefits/{company_benefit_id}" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyBenefitUpdateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompanyBenefitsCompanyBenefitIdResponse res = sdk.companyBenefits().update()
                .xGustoAPIVersion(PutV1CompanyBenefitsCompanyBenefitIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyBenefitId("<id>")
                .companyBenefitUpdateRequest(CompanyBenefitUpdateRequest.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.companyBenefit().isPresent()) {
            System.out.println(res.companyBenefit().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-company_benefits-company_benefit_id" method="put" path="/v1/company_benefits/{company_benefit_id}" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyBenefitUpdateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompanyBenefitsCompanyBenefitIdResponse res = sdk.companyBenefits().update()
                .xGustoAPIVersion(PutV1CompanyBenefitsCompanyBenefitIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyBenefitId("<id>")
                .companyBenefitUpdateRequest(CompanyBenefitUpdateRequest.builder()
                    .version("98jr3289h3298hr9329gf9egskt3kagri32qqgiqe3872")
                    .active(false)
                    .build())
                .call();

        if (res.companyBenefit().isPresent()) {
            System.out.println(res.companyBenefit().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-company_benefits-company_benefit_id" method="put" path="/v1/company_benefits/{company_benefit_id}" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyBenefitUpdateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompanyBenefitsCompanyBenefitIdResponse res = sdk.companyBenefits().update()
                .xGustoAPIVersion(PutV1CompanyBenefitsCompanyBenefitIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyBenefitId("<id>")
                .companyBenefitUpdateRequest(CompanyBenefitUpdateRequest.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.companyBenefit().isPresent()) {
            System.out.println(res.companyBenefit().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-company_benefits-company_benefit_id" method="put" path="/v1/company_benefits/{company_benefit_id}" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyBenefitUpdateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompanyBenefitsCompanyBenefitIdResponse res = sdk.companyBenefits().update()
                .xGustoAPIVersion(PutV1CompanyBenefitsCompanyBenefitIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyBenefitId("<id>")
                .companyBenefitUpdateRequest(CompanyBenefitUpdateRequest.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.companyBenefit().isPresent()) {
            System.out.println(res.companyBenefit().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1CompanyBenefitsCompanyBenefitIdHeaderXGustoAPIVersion>](../../models/operations/PutV1CompanyBenefitsCompanyBenefitIdHeaderXGustoAPIVersion.md)                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyBenefitId`                                                                                                                                                                                                           | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company benefit                                                                                                                                                                                              |
| `companyBenefitUpdateRequest`                                                                                                                                                                                                | [CompanyBenefitUpdateRequest](../../models/components/CompanyBenefitUpdateRequest.md)                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1CompanyBenefitsCompanyBenefitIdResponse](../../models/operations/PutV1CompanyBenefitsCompanyBenefitIdResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## delete

The following must be true in order to delete a company benefit

  - There are no employee benefits associated with the company benefit
  - There are no payroll items associated with the company benefit
  - The benefit is not managed by a Partner or by Gusto (type must be 'External')

When the application has the `company_benefits:write:benefit_type_limited` data scope, the application can only delete company benefits for benefit types that are permitted for the application.

scope: `company_benefits:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-company_benefits-company_benefit_id" method="delete" path="/v1/company_benefits/{company_benefit_id}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.operations.DeleteV1CompanyBenefitsCompanyBenefitIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.DeleteV1CompanyBenefitsCompanyBenefitIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1CompanyBenefitsCompanyBenefitIdResponse res = sdk.companyBenefits().delete()
                .xGustoAPIVersion(DeleteV1CompanyBenefitsCompanyBenefitIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyBenefitId("<id>")
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1CompanyBenefitsCompanyBenefitIdHeaderXGustoAPIVersion>](../../models/operations/DeleteV1CompanyBenefitsCompanyBenefitIdHeaderXGustoAPIVersion.md)                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyBenefitId`                                                                                                                                                                                                           | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company benefit                                                                                                                                                                                              |

### Response

**[DeleteV1CompanyBenefitsCompanyBenefitIdResponse](../../models/operations/DeleteV1CompanyBenefitsCompanyBenefitIdResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |

## getAll

Returns all benefits supported by Gusto. The benefit object in Gusto contains high level information about a particular benefit type and its tax considerations. When companies choose to offer a benefit, they are creating a Company Benefit object associated with a particular benefit.

scope: `benefits:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-benefits" method="get" path="/v1/benefits" example="Supported Benefits" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.operations.GetV1BenefitsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1BenefitsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1BenefitsResponse res = sdk.companyBenefits().getAll()
                .xGustoAPIVersion(GetV1BenefitsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.supportedBenefits().isPresent()) {
            System.out.println(res.supportedBenefits().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1BenefitsHeaderXGustoAPIVersion>](../../models/operations/GetV1BenefitsHeaderXGustoAPIVersion.md)                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1BenefitsResponse](../../models/operations/GetV1BenefitsResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |

## getSupported

Returns a benefit supported by Gusto. The benefit object in Gusto contains high level information about a particular benefit type and its tax considerations. When companies choose to offer a benefit, they are creating a Company Benefit object associated with a particular benefit.

scope: `benefits:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-benefits-benefit_id" method="get" path="/v1/benefits/{benefit_id}" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.operations.GetV1BenefitsBenefitIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1BenefitsBenefitIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1BenefitsBenefitIdResponse res = sdk.companyBenefits().getSupported()
                .xGustoAPIVersion(GetV1BenefitsBenefitIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .benefitId("<id>")
                .call();

        if (res.supportedBenefit().isPresent()) {
            System.out.println(res.supportedBenefit().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1BenefitsBenefitIdHeaderXGustoAPIVersion>](../../models/operations/GetV1BenefitsBenefitIdHeaderXGustoAPIVersion.md)                                                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `benefitId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The benefit type in Gusto.                                                                                                                                                                                                   |

### Response

**[GetV1BenefitsBenefitIdResponse](../../models/operations/GetV1BenefitsBenefitIdResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |

## getSummary

Returns summary benefit data for the requested company benefit id.

Benefits containing PHI are only visible to applications with the `company_benefits:read:phi` scope.

scope: `company_benefits:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-benefits-company_benefit_id-summary" method="get" path="/v1/company_benefits/{company_benefit_id}/summary" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1BenefitsCompanyBenefitIdSummaryRequest;
import com.gusto.embedded_api.models.operations.GetV1BenefitsCompanyBenefitIdSummaryResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1BenefitsCompanyBenefitIdSummaryRequest req = GetV1BenefitsCompanyBenefitIdSummaryRequest.builder()
                .companyBenefitId("<id>")
                .startDate("2022-01-01")
                .endDate("2022-12-31")
                .build();

        GetV1BenefitsCompanyBenefitIdSummaryResponse res = sdk.companyBenefits().getSummary()
                .request(req)
                .call();

        if (res.benefitSummary().isPresent()) {
            System.out.println(res.benefitSummary().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                             | Type                                                                                                                  | Required                                                                                                              | Description                                                                                                           |
| --------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| `request`                                                                                                             | [GetV1BenefitsCompanyBenefitIdSummaryRequest](../../models/operations/GetV1BenefitsCompanyBenefitIdSummaryRequest.md) | :heavy_check_mark:                                                                                                    | The request object to use for the request.                                                                            |

### Response

**[GetV1BenefitsCompanyBenefitIdSummaryResponse](../../models/operations/GetV1BenefitsCompanyBenefitIdSummaryResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## getEmployeeBenefits

Employee benefits represent an employee enrolled in a particular company benefit. It includes information specific to that employee's enrollment.

Returns an array of all employee benefits enrolled for this company benefit.

Benefits containing PHI are only visible to applications with the `employee_benefits:read:phi` scope.

scope: `employee_benefits:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-company_benefits-company_benefit_id-employee_benefits" method="get" path="/v1/company_benefits/{company_benefit_id}/employee_benefits" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsRequest;
import com.gusto.embedded_api.models.operations.GetV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsRequest req = GetV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsRequest.builder()
                .companyBenefitId("<id>")
                .build();

        GetV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsResponse res = sdk.companyBenefits().getEmployeeBenefits()
                .request(req)
                .call();

        if (res.employeeBenefits().isPresent()) {
            System.out.println(res.employeeBenefits().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                             | Type                                                                                                                                                  | Required                                                                                                                                              | Description                                                                                                                                           |
| ----------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| `request`                                                                                                                                             | [GetV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsRequest](../../models/operations/GetV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsRequest.md) | :heavy_check_mark:                                                                                                                                    | The request object to use for the request.                                                                                                            |

### Response

**[GetV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsResponse](../../models/operations/GetV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## updateEmployeeBenefits

Employee benefits represent an employee enrolled in a particular company benefit. It includes information specific to that employee's enrollment.

Create or update(if the employee is already enrolled in the company benefit previously) an employee benefit for the company benefit.

Benefits containing PHI are only visible to applications with the `employee_benefits:read:phi` scope.

When the application has the `employee_benefits:write:benefit_type_limited` data scope, the application can only create or update employee benefits for benefit types that are permitted for the application.

scope: `employee_benefits:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-company_benefits-company_benefit_id-employee_benefits" method="put" path="/v1/company_benefits/{company_benefit_id}/employee_benefits" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBenefitBulkUpdateRequest;
import com.gusto.embedded_api.models.components.EmployeeBenefitForCompanyBenefit;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsResponse res = sdk.companyBenefits().updateEmployeeBenefits()
                .xGustoAPIVersion(PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyBenefitId("<id>")
                .employeeBenefitBulkUpdateRequest(EmployeeBenefitBulkUpdateRequest.builder()
                    .employeeBenefits(List.of(
                        EmployeeBenefitForCompanyBenefit.builder()
                            .employeeUuid("<id>")
                            .build()))
                    .build())
                .call();

        if (res.employeeBenefits().isPresent()) {
            System.out.println(res.employeeBenefits().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-company_benefits-company_benefit_id-employee_benefits" method="put" path="/v1/company_benefits/{company_benefit_id}/employee_benefits" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBenefitBulkUpdateRequest;
import com.gusto.embedded_api.models.components.EmployeeBenefitForCompanyBenefit;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsResponse res = sdk.companyBenefits().updateEmployeeBenefits()
                .xGustoAPIVersion(PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyBenefitId("<id>")
                .employeeBenefitBulkUpdateRequest(EmployeeBenefitBulkUpdateRequest.builder()
                    .employeeBenefits(List.of(
                        EmployeeBenefitForCompanyBenefit.builder()
                            .employeeUuid("8f9f3f68-8fd3-499d-ade7-4a052e56494e")
                            .version("09j3d29jqdpj92109j9j2d90dq")
                            .employeeDeduction("250.00")
                            .build()))
                    .build())
                .call();

        if (res.employeeBenefits().isPresent()) {
            System.out.println(res.employeeBenefits().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-company_benefits-company_benefit_id-employee_benefits" method="put" path="/v1/company_benefits/{company_benefit_id}/employee_benefits" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBenefitBulkUpdateRequest;
import com.gusto.embedded_api.models.components.EmployeeBenefitForCompanyBenefit;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsResponse res = sdk.companyBenefits().updateEmployeeBenefits()
                .xGustoAPIVersion(PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyBenefitId("<id>")
                .employeeBenefitBulkUpdateRequest(EmployeeBenefitBulkUpdateRequest.builder()
                    .employeeBenefits(List.of(
                        EmployeeBenefitForCompanyBenefit.builder()
                            .employeeUuid("<id>")
                            .build()))
                    .build())
                .call();

        if (res.employeeBenefits().isPresent()) {
            System.out.println(res.employeeBenefits().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-company_benefits-company_benefit_id-employee_benefits" method="put" path="/v1/company_benefits/{company_benefit_id}/employee_benefits" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.EmployeeBenefitBulkUpdateRequest;
import com.gusto.embedded_api.models.components.EmployeeBenefitForCompanyBenefit;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsResponse res = sdk.companyBenefits().updateEmployeeBenefits()
                .xGustoAPIVersion(PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyBenefitId("<id>")
                .employeeBenefitBulkUpdateRequest(EmployeeBenefitBulkUpdateRequest.builder()
                    .employeeBenefits(List.of(
                        EmployeeBenefitForCompanyBenefit.builder()
                            .employeeUuid("<id>")
                            .build()))
                    .build())
                .call();

        if (res.employeeBenefits().isPresent()) {
            System.out.println(res.employeeBenefits().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsHeaderXGustoAPIVersion>](../../models/operations/PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsHeaderXGustoAPIVersion.md)                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyBenefitId`                                                                                                                                                                                                           | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company benefit                                                                                                                                                                                              |
| `employeeBenefitBulkUpdateRequest`                                                                                                                                                                                           | [EmployeeBenefitBulkUpdateRequest](../../models/components/EmployeeBenefitBulkUpdateRequest.md)                                                                                                                              | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsResponse](../../models/operations/PutV1CompanyBenefitsCompanyBenefitIdEmployeeBenefitsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getRequirements

Returns the field requirements for a given benefit type.

scope: `benefits:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-benefits-benefits_id-requirements" method="get" path="/v1/benefits/{benefit_id}/requirements" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1BenefitsBenefitsIdRequirementsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1BenefitsBenefitsIdRequirementsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1BenefitsBenefitsIdRequirementsResponse res = sdk.companyBenefits().getRequirements()
                .xGustoAPIVersion(GetV1BenefitsBenefitsIdRequirementsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .benefitId("<id>")
                .call();

        if (res.benefitTypeRequirements().isPresent()) {
            System.out.println(res.benefitTypeRequirements().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1BenefitsBenefitsIdRequirementsHeaderXGustoAPIVersion>](../../models/operations/GetV1BenefitsBenefitsIdRequirementsHeaderXGustoAPIVersion.md)                                                                 | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `benefitId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The benefit type in Gusto.                                                                                                                                                                                                   |

### Response

**[GetV1BenefitsBenefitsIdRequirementsResponse](../../models/operations/GetV1BenefitsBenefitsIdRequirementsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## getV1CompanyBenefitsCompanyBenefitIdContributionExclusions

Returns all contributions for a given company benefit and whether they are excluded or not.

Currently this endpoint only works for 401-k and Roth 401-k benefit types.

scope: `company_benefits:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-company_benefits-company_benefit_id-contribution_exclusions" method="get" path="/v1/company_benefits/{company_benefit_id}/contribution_exclusions" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1CompanyBenefitsCompanyBenefitIdContributionExclusionsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1CompanyBenefitsCompanyBenefitIdContributionExclusionsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompanyBenefitsCompanyBenefitIdContributionExclusionsResponse res = sdk.companyBenefits().getV1CompanyBenefitsCompanyBenefitIdContributionExclusions()
                .xGustoAPIVersion(GetV1CompanyBenefitsCompanyBenefitIdContributionExclusionsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyBenefitId("<id>")
                .call();

        if (res.contributionExclusions().isPresent()) {
            System.out.println(res.contributionExclusions().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompanyBenefitsCompanyBenefitIdContributionExclusionsHeaderXGustoAPIVersion>](../../models/operations/GetV1CompanyBenefitsCompanyBenefitIdContributionExclusionsHeaderXGustoAPIVersion.md)                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyBenefitId`                                                                                                                                                                                                           | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company benefit                                                                                                                                                                                              |

### Response

**[GetV1CompanyBenefitsCompanyBenefitIdContributionExclusionsResponse](../../models/operations/GetV1CompanyBenefitsCompanyBenefitIdContributionExclusionsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## putV1CompanyBenefitsCompanyBenefitIdContributionExclusions

Updates contribution exclusions for a given company benefit.

Currently this endpoint only works for 401-k and Roth 401-k benefit types.

scope: `company_benefits:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-company_benefits-company_benefit_id-contribution_exclusions" method="put" path="/v1/company_benefits/{company_benefit_id}/contribution_exclusions" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.ContributionExclusion;
import com.gusto.embedded_api.models.components.ContributionExclusionUpdateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsResponse res = sdk.companyBenefits().putV1CompanyBenefitsCompanyBenefitIdContributionExclusions()
                .xGustoAPIVersion(PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyBenefitId("<id>")
                .contributionExclusionUpdateRequest(ContributionExclusionUpdateRequest.builder()
                    .contributionExclusions(List.of(
                        ContributionExclusion.builder()
                            .contributionUuid("<id>")
                            .contributionType("<value>")
                            .excluded(true)
                            .build()))
                    .build())
                .call();

        if (res.contributionExclusions().isPresent()) {
            System.out.println(res.contributionExclusions().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-company_benefits-company_benefit_id-contribution_exclusions" method="put" path="/v1/company_benefits/{company_benefit_id}/contribution_exclusions" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.ContributionExclusion;
import com.gusto.embedded_api.models.components.ContributionExclusionUpdateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsResponse res = sdk.companyBenefits().putV1CompanyBenefitsCompanyBenefitIdContributionExclusions()
                .xGustoAPIVersion(PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyBenefitId("<id>")
                .contributionExclusionUpdateRequest(ContributionExclusionUpdateRequest.builder()
                    .contributionExclusions(List.of(
                        ContributionExclusion.builder()
                            .contributionUuid("082dfd3e-5b55-11f0-bb42-ab7136ba04e2")
                            .contributionType("Bonus")
                            .excluded(true)
                            .build(),
                        ContributionExclusion.builder()
                            .contributionUuid("082e034c-5b55-11f0-bb42-ab7136ba04e2")
                            .contributionType("Commission")
                            .excluded(false)
                            .build(),
                        ContributionExclusion.builder()
                            .contributionUuid("082e1f6c-5b55-11f0-bb42-ab7136ba04e2")
                            .contributionType("Regular")
                            .excluded(true)
                            .build()))
                    .build())
                .call();

        if (res.contributionExclusions().isPresent()) {
            System.out.println(res.contributionExclusions().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-company_benefits-company_benefit_id-contribution_exclusions" method="put" path="/v1/company_benefits/{company_benefit_id}/contribution_exclusions" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.ContributionExclusion;
import com.gusto.embedded_api.models.components.ContributionExclusionUpdateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsResponse res = sdk.companyBenefits().putV1CompanyBenefitsCompanyBenefitIdContributionExclusions()
                .xGustoAPIVersion(PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyBenefitId("<id>")
                .contributionExclusionUpdateRequest(ContributionExclusionUpdateRequest.builder()
                    .contributionExclusions(List.of(
                        ContributionExclusion.builder()
                            .contributionUuid("<id>")
                            .contributionType("<value>")
                            .excluded(true)
                            .build()))
                    .build())
                .call();

        if (res.contributionExclusions().isPresent()) {
            System.out.println(res.contributionExclusions().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-company_benefits-company_benefit_id-contribution_exclusions" method="put" path="/v1/company_benefits/{company_benefit_id}/contribution_exclusions" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.ContributionExclusion;
import com.gusto.embedded_api.models.components.ContributionExclusionUpdateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsResponse res = sdk.companyBenefits().putV1CompanyBenefitsCompanyBenefitIdContributionExclusions()
                .xGustoAPIVersion(PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyBenefitId("<id>")
                .contributionExclusionUpdateRequest(ContributionExclusionUpdateRequest.builder()
                    .contributionExclusions(List.of(
                        ContributionExclusion.builder()
                            .contributionUuid("<id>")
                            .contributionType("<value>")
                            .excluded(true)
                            .build()))
                    .build())
                .call();

        if (res.contributionExclusions().isPresent()) {
            System.out.println(res.contributionExclusions().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsHeaderXGustoAPIVersion>](../../models/operations/PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsHeaderXGustoAPIVersion.md)                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyBenefitId`                                                                                                                                                                                                           | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company benefit                                                                                                                                                                                              |
| `contributionExclusionUpdateRequest`                                                                                                                                                                                         | [ContributionExclusionUpdateRequest](../../models/components/ContributionExclusionUpdateRequest.md)                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsResponse](../../models/operations/PutV1CompanyBenefitsCompanyBenefitIdContributionExclusionsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |