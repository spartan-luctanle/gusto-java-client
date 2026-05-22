# Locations

## Overview

### Available Operations

* [get](#get) - Get all company locations
* [create](#create) - Create a company location
* [retrieve](#retrieve) - Get a location
* [update](#update) - Update a location
* [getMinimumWages](#getminimumwages) - Get minimum wages for a location

## get

Retrieves all company locations (addresses) associated with a company: mailing addresses, filing
addresses, or work locations. A single address may serve multiple, or all, purposes.

Since all company locations are subsets of locations, use the Locations endpoints to
[get](ref:get-v1-locations-location_id) or [update](ref:put-v1-locations-location_id) an individual record.

scope: `companies:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_id-locations" method="get" path="/v1/companies/{company_id}/locations" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyIdLocationsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyIdLocationsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyIdLocationsResponse res = sdk.locations().get()
                .xGustoAPIVersion(GetV1CompaniesCompanyIdLocationsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .call();

        if (res.companyLocationsList().isPresent()) {
            System.out.println(res.companyLocationsList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  | Example                                                                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompaniesCompanyIdLocationsHeaderXGustoAPIVersion>](../../models/operations/GetV1CompaniesCompanyIdLocationsHeaderXGustoAPIVersion.md)                                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |                                                                                                                                                                                                                              |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      | 7b1d0df1-6403-4a06-8768-c1dd7d24d27a                                                                                                                                                                                         |
| `page`                                                                                                                                                                                                                       | *Optional\<Long>*                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                           | The page that is requested. When unspecified, will load all objects unless endpoint forces pagination.                                                                                                                       |                                                                                                                                                                                                                              |
| `per`                                                                                                                                                                                                                        | *Optional\<Long>*                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                           | Number of objects per page. For majority of endpoints will default to 25                                                                                                                                                     |                                                                                                                                                                                                                              |

### Response

**[GetV1CompaniesCompanyIdLocationsResponse](../../models/operations/GetV1CompaniesCompanyIdLocationsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## create

Create a company location, which represents any address associated with a company: mailing
addresses, filing addresses, or work locations. A single address may serve multiple, or all, purposes.

Since all company locations are subsets of locations, use the Locations endpoints to
[get](ref:get-v1-locations-location_id) or [update](ref:put-v1-locations-location_id) an individual record.

scope: `companies:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-locations" method="post" path="/v1/companies/{company_id}/locations" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyLocationRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdLocationsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdLocationsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyIdLocationsResponse res = sdk.locations().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdLocationsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .companyLocationRequest(CompanyLocationRequest.builder()
                    .street1("<value>")
                    .city("Chynastad")
                    .state("Wisconsin")
                    .zip("88336")
                    .phoneNumber("841-814-9427 x9355")
                    .build())
                .call();

        if (res.location().isPresent()) {
            System.out.println(res.location().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-locations" method="post" path="/v1/companies/{company_id}/locations" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyLocationRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdLocationsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdLocationsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyIdLocationsResponse res = sdk.locations().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdLocationsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .companyLocationRequest(CompanyLocationRequest.builder()
                    .street1("425 2nd Street")
                    .city("San Francisco")
                    .state("CA")
                    .zip("94107")
                    .phoneNumber("8009360383")
                    .street2("Suite 602")
                    .build())
                .call();

        if (res.location().isPresent()) {
            System.out.println(res.location().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-locations" method="post" path="/v1/companies/{company_id}/locations" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyLocationRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdLocationsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdLocationsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyIdLocationsResponse res = sdk.locations().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdLocationsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .companyLocationRequest(CompanyLocationRequest.builder()
                    .street1("<value>")
                    .city("Chynastad")
                    .state("Wisconsin")
                    .zip("88336")
                    .phoneNumber("841-814-9427 x9355")
                    .build())
                .call();

        if (res.location().isPresent()) {
            System.out.println(res.location().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-locations" method="post" path="/v1/companies/{company_id}/locations" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.CompanyLocationRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdLocationsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyIdLocationsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyIdLocationsResponse res = sdk.locations().create()
                .xGustoAPIVersion(PostV1CompaniesCompanyIdLocationsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyId("<id>")
                .companyLocationRequest(CompanyLocationRequest.builder()
                    .street1("<value>")
                    .city("Chynastad")
                    .state("Wisconsin")
                    .zip("88336")
                    .phoneNumber("841-814-9427 x9355")
                    .build())
                .call();

        if (res.location().isPresent()) {
            System.out.println(res.location().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompaniesCompanyIdLocationsHeaderXGustoAPIVersion>](../../models/operations/PostV1CompaniesCompanyIdLocationsHeaderXGustoAPIVersion.md)                                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `companyLocationRequest`                                                                                                                                                                                                     | [CompanyLocationRequest](../../models/components/CompanyLocationRequest.md)                                                                                                                                                  | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompaniesCompanyIdLocationsResponse](../../models/operations/PostV1CompaniesCompanyIdLocationsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## retrieve

Get a location.

scope: `companies:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-locations-location_id" method="get" path="/v1/locations/{location_id}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1LocationsLocationIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1LocationsLocationIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1LocationsLocationIdResponse res = sdk.locations().retrieve()
                .xGustoAPIVersion(GetV1LocationsLocationIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .locationId("<id>")
                .call();

        if (res.location().isPresent()) {
            System.out.println(res.location().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1LocationsLocationIdHeaderXGustoAPIVersion>](../../models/operations/GetV1LocationsLocationIdHeaderXGustoAPIVersion.md)                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `locationId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the location                                                                                                                                                                                                     |

### Response

**[GetV1LocationsLocationIdResponse](../../models/operations/GetV1LocationsLocationIdResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## update

Update a location.

scope: `companies:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-locations-location_id" method="put" path="/v1/locations/{location_id}" -->
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

        PutV1LocationsLocationIdResponse res = sdk.locations().update()
                .xGustoAPIVersion(PutV1LocationsLocationIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .locationId("<id>")
                .requestBody(PutV1LocationsLocationIdRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .phoneNumber("8009360383")
                    .street1("300 3rd Street")
                    .street2("Apartment 318")
                    .city("San Francisco")
                    .zip("94107")
                    .build())
                .call();

        if (res.location().isPresent()) {
            System.out.println(res.location().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1LocationsLocationIdHeaderXGustoAPIVersion>](../../models/operations/PutV1LocationsLocationIdHeaderXGustoAPIVersion.md)                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `locationId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the location                                                                                                                                                                                                     |
| `requestBody`                                                                                                                                                                                                                | [PutV1LocationsLocationIdRequestBody](../../models/operations/PutV1LocationsLocationIdRequestBody.md)                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1LocationsLocationIdResponse](../../models/operations/PutV1LocationsLocationIdResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 409, 422                               | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getMinimumWages

Get minimum wages for a location

scope: `companies:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-locations-location_uuid-minimum_wages" method="get" path="/v1/locations/{location_uuid}/minimum_wages" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1LocationsLocationUuidMinimumWagesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1LocationsLocationUuidMinimumWagesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1LocationsLocationUuidMinimumWagesResponse res = sdk.locations().getMinimumWages()
                .locationUuid("<id>")
                .xGustoAPIVersion(GetV1LocationsLocationUuidMinimumWagesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .effectiveDate("2020-01-31")
                .call();

        if (res.minimumWageList().isPresent()) {
            System.out.println(res.minimumWageList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  | Example                                                                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `locationUuid`                                                                                                                                                                                                               | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the location                                                                                                                                                                                                     |                                                                                                                                                                                                                              |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1LocationsLocationUuidMinimumWagesHeaderXGustoAPIVersion>](../../models/operations/GetV1LocationsLocationUuidMinimumWagesHeaderXGustoAPIVersion.md)                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |                                                                                                                                                                                                                              |
| `effectiveDate`                                                                                                                                                                                                              | *Optional\<String>*                                                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          | 2020-01-31                                                                                                                                                                                                                   |

### Response

**[GetV1LocationsLocationUuidMinimumWagesResponse](../../models/operations/GetV1LocationsLocationUuidMinimumWagesResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |