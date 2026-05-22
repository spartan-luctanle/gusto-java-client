# Signatories

## Overview

### Available Operations

* [list](#list) - Get the signatories for a company
* [create](#create) - Create a signatory
* [invite](#invite) - Invite a signatory
* [update](#update) - Update a signatory
* [delete](#delete) - Delete a signatory

## list

Returns the signatories for a company. A company has at most one signatory.

## Related guides
- [Signatory Events](doc:signatory-events)

scope: `signatories:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-company_uuid-signatories" method="get" path="/v1/companies/{company_uuid}/signatories" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyUuidSignatoriesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetV1CompaniesCompanyUuidSignatoriesResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesCompanyUuidSignatoriesResponse res = sdk.signatories().list()
                .companyUuid("<id>")
                .xGustoAPIVersion(GetV1CompaniesCompanyUuidSignatoriesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.signatories().isPresent()) {
            System.out.println(res.signatories().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompaniesCompanyUuidSignatoriesHeaderXGustoAPIVersion>](../../models/operations/GetV1CompaniesCompanyUuidSignatoriesHeaderXGustoAPIVersion.md)                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1CompaniesCompanyUuidSignatoriesResponse](../../models/operations/GetV1CompaniesCompanyUuidSignatoriesResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## create

Creates a company signatory with complete information. The company must not already have a signatory.

A signatory can legally sign forms once the identity verification process is successful. The signatory should be an officer, owner, general partner or LLC member manager, plan administrator, fiduciary, or an authorized representative who is designated to sign agreements on the company's behalf. An officer is the president, vice president, treasurer, chief accounting officer, etc. There can only be a single primary signatory in a company.

### Webhooks
- `signatory.created`: Fires when a signatory is successfully created.

### Related guides
- [Signatory Events](doc:signatory-events)

scope: `signatories:manage`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="post-v1-company-signatories" method="post" path="/v1/companies/{company_uuid}/signatories" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.SignatoryCreateRequest;
import com.gusto.embedded_api.models.components.SignatoryCreateRequestHomeAddress;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompanySignatoriesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompanySignatoriesResponse;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompanySignatoriesResponse res = sdk.signatories().create()
                .companyUuid("<id>")
                .xGustoAPIVersion(PostV1CompanySignatoriesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .signatoryCreateRequest(SignatoryCreateRequest.builder()
                    .firstName("Ed")
                    .lastName("Reichert")
                    .title("<value>")
                    .phone("1-346-396-8392 x69356")
                    .birthday(LocalDate.parse("<value>"))
                    .email("Shanny62@hotmail.com")
                    .ssn("<value>")
                    .homeAddress(SignatoryCreateRequestHomeAddress.builder()
                        .street1("<value>")
                        .city("East Clydefield")
                        .state("Kentucky")
                        .zip("13719-5134")
                        .build())
                    .build())
                .call();

        if (res.signatory().isPresent()) {
            System.out.println(res.signatory().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="post-v1-company-signatories" method="post" path="/v1/companies/{company_uuid}/signatories" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.SignatoryCreateRequest;
import com.gusto.embedded_api.models.components.SignatoryCreateRequestHomeAddress;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompanySignatoriesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompanySignatoriesResponse;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompanySignatoriesResponse res = sdk.signatories().create()
                .companyUuid("<id>")
                .xGustoAPIVersion(PostV1CompanySignatoriesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .signatoryCreateRequest(SignatoryCreateRequest.builder()
                    .firstName("Ed")
                    .lastName("Reichert")
                    .title("<value>")
                    .phone("1-346-396-8392 x69356")
                    .birthday(LocalDate.parse("<value>"))
                    .email("Shanny62@hotmail.com")
                    .ssn("<value>")
                    .homeAddress(SignatoryCreateRequestHomeAddress.builder()
                        .street1("<value>")
                        .city("East Clydefield")
                        .state("Kentucky")
                        .zip("13719-5134")
                        .build())
                    .build())
                .call();

        if (res.signatory().isPresent()) {
            System.out.println(res.signatory().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="post-v1-company-signatories" method="post" path="/v1/companies/{company_uuid}/signatories" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.SignatoryCreateRequest;
import com.gusto.embedded_api.models.components.SignatoryCreateRequestHomeAddress;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompanySignatoriesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompanySignatoriesResponse;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompanySignatoriesResponse res = sdk.signatories().create()
                .companyUuid("<id>")
                .xGustoAPIVersion(PostV1CompanySignatoriesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .signatoryCreateRequest(SignatoryCreateRequest.builder()
                    .firstName("Ed")
                    .lastName("Reichert")
                    .title("<value>")
                    .phone("1-346-396-8392 x69356")
                    .birthday(LocalDate.parse("<value>"))
                    .email("Shanny62@hotmail.com")
                    .ssn("<value>")
                    .homeAddress(SignatoryCreateRequestHomeAddress.builder()
                        .street1("<value>")
                        .city("East Clydefield")
                        .state("Kentucky")
                        .zip("13719-5134")
                        .build())
                    .build())
                .call();

        if (res.signatory().isPresent()) {
            System.out.println(res.signatory().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="post-v1-company-signatories" method="post" path="/v1/companies/{company_uuid}/signatories" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.SignatoryCreateRequest;
import com.gusto.embedded_api.models.components.SignatoryCreateRequestHomeAddress;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompanySignatoriesHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompanySignatoriesResponse;
import java.lang.Exception;
import java.time.LocalDate;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompanySignatoriesResponse res = sdk.signatories().create()
                .companyUuid("<id>")
                .xGustoAPIVersion(PostV1CompanySignatoriesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .signatoryCreateRequest(SignatoryCreateRequest.builder()
                    .firstName("Ed")
                    .lastName("Reichert")
                    .title("<value>")
                    .phone("1-346-396-8392 x69356")
                    .birthday(LocalDate.parse("<value>"))
                    .email("Shanny62@hotmail.com")
                    .ssn("<value>")
                    .homeAddress(SignatoryCreateRequestHomeAddress.builder()
                        .street1("<value>")
                        .city("East Clydefield")
                        .state("Kentucky")
                        .zip("13719-5134")
                        .build())
                    .build())
                .call();

        if (res.signatory().isPresent()) {
            System.out.println(res.signatory().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompanySignatoriesHeaderXGustoAPIVersion>](../../models/operations/PostV1CompanySignatoriesHeaderXGustoAPIVersion.md)                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `signatoryCreateRequest`                                                                                                                                                                                                     | [SignatoryCreateRequest](../../models/components/SignatoryCreateRequest.md)                                                                                                                                                  | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompanySignatoriesResponse](../../models/operations/PostV1CompanySignatoriesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## invite

Creates a signatory with minimal information. This signatory can be invited to provide more information through the [Update a signatory](ref:put-v1-companies-company_uuid-signatories-signatory_uuid) endpoint. This will start the identity verification process and allow the signatory to be verified to sign documents.

## Related guides
- [Signatory Events](doc:signatory-events)

scope: `signatories:manage`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_uuid-signatories-invite" method="post" path="/v1/companies/{company_uuid}/signatories/invite" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.SignatoryInviteRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyUuidSignatoriesInviteHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyUuidSignatoriesInviteResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyUuidSignatoriesInviteResponse res = sdk.signatories().invite()
                .companyUuid("<id>")
                .xGustoAPIVersion(PostV1CompaniesCompanyUuidSignatoriesInviteHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .signatoryInviteRequest(SignatoryInviteRequest.builder()
                    .firstName("Madelyn")
                    .lastName("Littel")
                    .email("Kamron.Nikolaus@yahoo.com")
                    .build())
                .call();

        if (res.signatory().isPresent()) {
            System.out.println(res.signatory().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_uuid-signatories-invite" method="post" path="/v1/companies/{company_uuid}/signatories/invite" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.SignatoryInviteRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyUuidSignatoriesInviteHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyUuidSignatoriesInviteResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyUuidSignatoriesInviteResponse res = sdk.signatories().invite()
                .companyUuid("<id>")
                .xGustoAPIVersion(PostV1CompaniesCompanyUuidSignatoriesInviteHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .signatoryInviteRequest(SignatoryInviteRequest.builder()
                    .firstName("Lucienne")
                    .lastName("Watsica")
                    .email("Kamron.Nikolaus@yahoo.com")
                    .build())
                .call();

        if (res.signatory().isPresent()) {
            System.out.println(res.signatory().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_uuid-signatories-invite" method="post" path="/v1/companies/{company_uuid}/signatories/invite" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.SignatoryInviteRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyUuidSignatoriesInviteHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyUuidSignatoriesInviteResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyUuidSignatoriesInviteResponse res = sdk.signatories().invite()
                .companyUuid("<id>")
                .xGustoAPIVersion(PostV1CompaniesCompanyUuidSignatoriesInviteHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .signatoryInviteRequest(SignatoryInviteRequest.builder()
                    .firstName("Fatima")
                    .lastName("Ruecker")
                    .email("Kamron.Nikolaus@yahoo.com")
                    .build())
                .call();

        if (res.signatory().isPresent()) {
            System.out.println(res.signatory().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_uuid-signatories-invite" method="post" path="/v1/companies/{company_uuid}/signatories/invite" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.SignatoryInviteRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyUuidSignatoriesInviteHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostV1CompaniesCompanyUuidSignatoriesInviteResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyUuidSignatoriesInviteResponse res = sdk.signatories().invite()
                .companyUuid("<id>")
                .xGustoAPIVersion(PostV1CompaniesCompanyUuidSignatoriesInviteHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .signatoryInviteRequest(SignatoryInviteRequest.builder()
                    .firstName("Mac")
                    .lastName("Hudson")
                    .email("Kamron.Nikolaus@yahoo.com")
                    .build())
                .call();

        if (res.signatory().isPresent()) {
            System.out.println(res.signatory().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompaniesCompanyUuidSignatoriesInviteHeaderXGustoAPIVersion>](../../models/operations/PostV1CompaniesCompanyUuidSignatoriesInviteHeaderXGustoAPIVersion.md)                                                 | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `signatoryInviteRequest`                                                                                                                                                                                                     | [SignatoryInviteRequest](../../models/components/SignatoryInviteRequest.md)                                                                                                                                                  | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompaniesCompanyUuidSignatoriesInviteResponse](../../models/operations/PostV1CompaniesCompanyUuidSignatoriesInviteResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## update

Updates a signatory that has been either invited or created. If the signatory has been created with minimal information through the [Invite a signatory](ref:post-v1-companies-company_uuid-signatories-invite) endpoint, then the first update must contain all attributes specified in the request body in order to start the identity verification process.

## Related guides
- [Signatory Events](doc:signatory-events)

scope: `signatories:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_uuid-signatories-signatory_uuid" method="put" path="/v1/companies/{company_uuid}/signatories/{signatory_uuid}" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.SignatoryUpdateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidResponse res = sdk.signatories().update()
                .companyUuid("<id>")
                .signatoryUuid("<id>")
                .xGustoAPIVersion(PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .signatoryUpdateRequest(SignatoryUpdateRequest.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.signatory().isPresent()) {
            System.out.println(res.signatory().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_uuid-signatories-signatory_uuid" method="put" path="/v1/companies/{company_uuid}/signatories/{signatory_uuid}" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.SignatoryUpdateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidResponse res = sdk.signatories().update()
                .companyUuid("<id>")
                .signatoryUuid("<id>")
                .xGustoAPIVersion(PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .signatoryUpdateRequest(SignatoryUpdateRequest.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.signatory().isPresent()) {
            System.out.println(res.signatory().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_uuid-signatories-signatory_uuid" method="put" path="/v1/companies/{company_uuid}/signatories/{signatory_uuid}" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.SignatoryUpdateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidResponse res = sdk.signatories().update()
                .companyUuid("<id>")
                .signatoryUuid("<id>")
                .xGustoAPIVersion(PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .signatoryUpdateRequest(SignatoryUpdateRequest.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.signatory().isPresent()) {
            System.out.println(res.signatory().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-companies-company_uuid-signatories-signatory_uuid" method="put" path="/v1/companies/{company_uuid}/signatories/{signatory_uuid}" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.SignatoryUpdateRequest;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidResponse res = sdk.signatories().update()
                .companyUuid("<id>")
                .signatoryUuid("<id>")
                .xGustoAPIVersion(PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .signatoryUpdateRequest(SignatoryUpdateRequest.builder()
                    .version("<value>")
                    .build())
                .call();

        if (res.signatory().isPresent()) {
            System.out.println(res.signatory().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `signatoryUuid`                                                                                                                                                                                                              | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the signatory                                                                                                                                                                                                    |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidHeaderXGustoAPIVersion>](../../models/operations/PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidHeaderXGustoAPIVersion.md)                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `signatoryUpdateRequest`                                                                                                                                                                                                     | [SignatoryUpdateRequest](../../models/components/SignatoryUpdateRequest.md)                                                                                                                                                  | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidResponse](../../models/operations/PutV1CompaniesCompanyUuidSignatoriesSignatoryUuidResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 409, 422                               | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## delete

Deletes a company signatory.

## Related guides
- [Signatory Events](doc:signatory-events)

scope: `signatories:manage`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-companies-company_uuid-signatories-signatory_uuid" method="delete" path="/v1/companies/{company_uuid}/signatories/{signatory_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.DeleteV1CompaniesCompanyUuidSignatoriesSignatoryUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.DeleteV1CompaniesCompanyUuidSignatoriesSignatoryUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1CompaniesCompanyUuidSignatoriesSignatoryUuidResponse res = sdk.signatories().delete()
                .companyUuid("<id>")
                .signatoryUuid("<id>")
                .xGustoAPIVersion(DeleteV1CompaniesCompanyUuidSignatoriesSignatoryUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `signatoryUuid`                                                                                                                                                                                                              | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the signatory                                                                                                                                                                                                    |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1CompaniesCompanyUuidSignatoriesSignatoryUuidHeaderXGustoAPIVersion>](../../models/operations/DeleteV1CompaniesCompanyUuidSignatoriesSignatoryUuidHeaderXGustoAPIVersion.md)                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[DeleteV1CompaniesCompanyUuidSignatoriesSignatoryUuidResponse](../../models/operations/DeleteV1CompaniesCompanyUuidSignatoriesSignatoryUuidResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |