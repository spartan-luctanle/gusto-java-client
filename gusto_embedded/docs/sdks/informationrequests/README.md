# InformationRequests

## Overview

### Available Operations

* [getInformationRequests](#getinformationrequests) - Get all information requests for a company
* [submit](#submit) - Submit information request responses

## getInformationRequests

Fetch all information requests for a company.

scope: `information_requests:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-information-requests" method="get" path="/v1/companies/{company_uuid}/information_requests" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetInformationRequestsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetInformationRequestsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetInformationRequestsResponse res = sdk.informationRequests().getInformationRequests()
                .xGustoAPIVersion(GetInformationRequestsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .companyUuid("<id>")
                .call();

        if (res.informationRequests().isPresent()) {
            System.out.println(res.informationRequests().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetInformationRequestsHeaderXGustoAPIVersion>](../../models/operations/GetInformationRequestsHeaderXGustoAPIVersion.md)                                                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |

### Response

**[GetInformationRequestsResponse](../../models/operations/GetInformationRequestsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## submit

Submit responses to an information request.
Supports both text responses and file uploads (multipart/form-data).
Maximum file size: 120MB.

scope: `information_requests:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="submit-information-request" method="put" path="/v1/information_requests/{information_request_uuid}/submit" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.SubmitInformationRequestRequestBody;
import com.gusto.embedded_api.models.operations.SubmitInformationRequestResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        SubmitInformationRequestResponse res = sdk.informationRequests().submit()
                .informationRequestUuid("<id>")
                .requestBody(SubmitInformationRequestRequestBody.builder()
                    .build())
                .call();

        if (res.informationRequest().isPresent()) {
            System.out.println(res.informationRequest().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="submit-information-request" method="put" path="/v1/information_requests/{information_request_uuid}/submit" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.SubmitInformationRequestRequestBody;
import com.gusto.embedded_api.models.operations.SubmitInformationRequestResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        SubmitInformationRequestResponse res = sdk.informationRequests().submit()
                .informationRequestUuid("<id>")
                .requestBody(SubmitInformationRequestRequestBody.builder()
                    .build())
                .call();

        if (res.informationRequest().isPresent()) {
            System.out.println(res.informationRequest().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="submit-information-request" method="put" path="/v1/information_requests/{information_request_uuid}/submit" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.SubmitInformationRequestRequestBody;
import com.gusto.embedded_api.models.operations.SubmitInformationRequestResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        SubmitInformationRequestResponse res = sdk.informationRequests().submit()
                .informationRequestUuid("<id>")
                .requestBody(SubmitInformationRequestRequestBody.builder()
                    .build())
                .call();

        if (res.informationRequest().isPresent()) {
            System.out.println(res.informationRequest().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                             | Type                                                                                                  | Required                                                                                              | Description                                                                                           |
| ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| `informationRequestUuid`                                                                              | *String*                                                                                              | :heavy_check_mark:                                                                                    | The UUID of the information request                                                                   |
| `requestBody`                                                                                         | [SubmitInformationRequestRequestBody](../../models/operations/SubmitInformationRequestRequestBody.md) | :heavy_check_mark:                                                                                    | N/A                                                                                                   |

### Response

**[SubmitInformationRequestResponse](../../models/operations/SubmitInformationRequestResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |