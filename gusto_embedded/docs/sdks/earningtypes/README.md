# EarningTypes

## Overview

### Available Operations

* [list](#list) - Get all earning types for a company
* [create](#create) - Create a custom earning type
* [update](#update) - Update an earning type
* [delete](#delete) - Deactivate an earning type

## list

A payroll item in Gusto is associated to an earning type to name the type of earning described by the payroll item.

#### Default Earning Type
Certain earning types are special because they have tax considerations. Those earning types are mostly the same for every company depending on its legal structure (LLC, Corporation, etc.)

#### Custom Earning Type
Custom earning types are all the other earning types added specifically for a company.

scope: `payrolls:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_id-earning_types" method="get" path="/v1/companies/{company_id}/earning_types" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyIdEarningTypesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyIdEarningTypesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyIdEarningTypesResponse res = sdk.earningTypes().list()
                .xGustoAPIVersion(GetV1CompaniesCompanyIdEarningTypesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .call();

        if (res.earningTypeList().isPresent()) {
            System.out.println(res.earningTypeList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompaniesCompanyIdEarningTypesHeaderXGustoAPIVersion>](../../models/operations/GetV1CompaniesCompanyIdEarningTypesHeaderXGustoAPIVersion.md)                                                                 | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |

### Response

**[GetV1CompaniesCompanyIdEarningTypesResponse](../../models/operations/GetV1CompaniesCompanyIdEarningTypesResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## create

Create a custom earning type.

If an inactive earning type exists with the same name, this will reactivate it instead of creating a new one.

scope: `payrolls:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-earning_types" method="post" path="/v1/companies/{company_id}/earning_types" example="Basic" -->
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

        PostV1CompaniesCompanyIdEarningTypesResponse res = sdk.earningTypes().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdEarningTypesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .requestBody(PostV1CompaniesCompanyIdEarningTypesRequestBody.builder()
                    .name("<value>")
                    .build())
                .call();

        if (res.earningType().isPresent()) {
            System.out.println(res.earningType().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-earning_types" method="post" path="/v1/companies/{company_id}/earning_types" example="Example" -->
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

        PostV1CompaniesCompanyIdEarningTypesResponse res = sdk.earningTypes().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdEarningTypesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .requestBody(PostV1CompaniesCompanyIdEarningTypesRequestBody.builder()
                    .name("Gym Membership Stipend")
                    .build())
                .call();

        if (res.earningType().isPresent()) {
            System.out.println(res.earningType().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-earning_types" method="post" path="/v1/companies/{company_id}/earning_types" example="Nested" -->
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

        PostV1CompaniesCompanyIdEarningTypesResponse res = sdk.earningTypes().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdEarningTypesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .requestBody(PostV1CompaniesCompanyIdEarningTypesRequestBody.builder()
                    .name("<value>")
                    .build())
                .call();

        if (res.earningType().isPresent()) {
            System.out.println(res.earningType().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-earning_types" method="post" path="/v1/companies/{company_id}/earning_types" example="Resource" -->
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

        PostV1CompaniesCompanyIdEarningTypesResponse res = sdk.earningTypes().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdEarningTypesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .requestBody(PostV1CompaniesCompanyIdEarningTypesRequestBody.builder()
                    .name("<value>")
                    .build())
                .call();

        if (res.earningType().isPresent()) {
            System.out.println(res.earningType().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompaniesCompanyIdEarningTypesHeaderXGustoAPIVersion>](../../models/operations/PostV1CompaniesCompanyIdEarningTypesHeaderXGustoAPIVersion.md)                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `requestBody`                                                                                                                                                                                                                | [PostV1CompaniesCompanyIdEarningTypesRequestBody](../../models/operations/PostV1CompaniesCompanyIdEarningTypesRequestBody.md)                                                                                                | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompaniesCompanyIdEarningTypesResponse](../../models/operations/PostV1CompaniesCompanyIdEarningTypesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## update

Update an earning type.

scope: `payrolls:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_id-earning_types-earning_type_uuid" method="put" path="/v1/companies/{company_id}/earning_types/{earning_type_uuid}" example="Basic" -->
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

        PutV1CompaniesCompanyIdEarningTypesEarningTypeUuidResponse res = sdk.earningTypes().update()
                .xGustoAPIVersion(PutV1CompaniesCompanyIdEarningTypesEarningTypeUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .earningTypeUuid("<id>")
                .requestBody(PutV1CompaniesCompanyIdEarningTypesEarningTypeUuidRequestBody.builder()
                    .build())
                .call();

        if (res.earningType().isPresent()) {
            System.out.println(res.earningType().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_id-earning_types-earning_type_uuid" method="put" path="/v1/companies/{company_id}/earning_types/{earning_type_uuid}" example="Example" -->
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

        PutV1CompaniesCompanyIdEarningTypesEarningTypeUuidResponse res = sdk.earningTypes().update()
                .xGustoAPIVersion(PutV1CompaniesCompanyIdEarningTypesEarningTypeUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .earningTypeUuid("<id>")
                .requestBody(PutV1CompaniesCompanyIdEarningTypesEarningTypeUuidRequestBody.builder()
                    .name("Gym Membership Stipend")
                    .build())
                .call();

        if (res.earningType().isPresent()) {
            System.out.println(res.earningType().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_id-earning_types-earning_type_uuid" method="put" path="/v1/companies/{company_id}/earning_types/{earning_type_uuid}" example="Nested" -->
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

        PutV1CompaniesCompanyIdEarningTypesEarningTypeUuidResponse res = sdk.earningTypes().update()
                .xGustoAPIVersion(PutV1CompaniesCompanyIdEarningTypesEarningTypeUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .earningTypeUuid("<id>")
                .requestBody(PutV1CompaniesCompanyIdEarningTypesEarningTypeUuidRequestBody.builder()
                    .build())
                .call();

        if (res.earningType().isPresent()) {
            System.out.println(res.earningType().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_id-earning_types-earning_type_uuid" method="put" path="/v1/companies/{company_id}/earning_types/{earning_type_uuid}" example="Resource" -->
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

        PutV1CompaniesCompanyIdEarningTypesEarningTypeUuidResponse res = sdk.earningTypes().update()
                .xGustoAPIVersion(PutV1CompaniesCompanyIdEarningTypesEarningTypeUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .earningTypeUuid("<id>")
                .requestBody(PutV1CompaniesCompanyIdEarningTypesEarningTypeUuidRequestBody.builder()
                    .build())
                .call();

        if (res.earningType().isPresent()) {
            System.out.println(res.earningType().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1CompaniesCompanyIdEarningTypesEarningTypeUuidHeaderXGustoAPIVersion>](../../models/operations/PutV1CompaniesCompanyIdEarningTypesEarningTypeUuidHeaderXGustoAPIVersion.md)                                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `earningTypeUuid`                                                                                                                                                                                                            | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the earning type                                                                                                                                                                                                 |
| `requestBody`                                                                                                                                                                                                                | [PutV1CompaniesCompanyIdEarningTypesEarningTypeUuidRequestBody](../../models/operations/PutV1CompaniesCompanyIdEarningTypesEarningTypeUuidRequestBody.md)                                                                    | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1CompaniesCompanyIdEarningTypesEarningTypeUuidResponse](../../models/operations/PutV1CompaniesCompanyIdEarningTypesEarningTypeUuidResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## delete

Deactivate an earning type.

scope: `payrolls:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-companies-company_id-earning_types-earning_type_uuid" method="delete" path="/v1/companies/{company_id}/earning_types/{earning_type_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.operations.DeleteV1CompaniesCompanyIdEarningTypesEarningTypeUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.DeleteV1CompaniesCompanyIdEarningTypesEarningTypeUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1CompaniesCompanyIdEarningTypesEarningTypeUuidResponse res = sdk.earningTypes().delete()
                .xGustoAPIVersion(DeleteV1CompaniesCompanyIdEarningTypesEarningTypeUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .earningTypeUuid("<id>")
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1CompaniesCompanyIdEarningTypesEarningTypeUuidHeaderXGustoAPIVersion>](../../models/operations/DeleteV1CompaniesCompanyIdEarningTypesEarningTypeUuidHeaderXGustoAPIVersion.md)                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `earningTypeUuid`                                                                                                                                                                                                            | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the earning type                                                                                                                                                                                                 |

### Response

**[DeleteV1CompaniesCompanyIdEarningTypesEarningTypeUuidResponse](../../models/operations/DeleteV1CompaniesCompanyIdEarningTypesEarningTypeUuidResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |