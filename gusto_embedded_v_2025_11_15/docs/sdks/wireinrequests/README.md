# WireInRequests

## Overview

### Available Operations

* [get](#get) - Get a single Wire In Request
* [submit](#submit) - Submit a wire in request
* [list](#list) - Get all Wire In Requests for a company

## get

Fetch a Wire In Request.

scope: `payrolls:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-wire_in_requests-wire_in_request_uuid" method="get" path="/v1/wire_in_requests/{wire_in_request_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetWireInRequestsWireInRequestUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetWireInRequestsWireInRequestUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetWireInRequestsWireInRequestUuidResponse res = sdk.wireInRequests().get()
                .wireInRequestUuid("<id>")
                .xGustoAPIVersion(GetWireInRequestsWireInRequestUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .call();

        if (res.wireInRequest().isPresent()) {
            System.out.println(res.wireInRequest().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `wireInRequestUuid`                                                                                                                                                                                                          | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the Wire In Request                                                                                                                                                                                              |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetWireInRequestsWireInRequestUuidHeaderXGustoAPIVersion>](../../models/operations/GetWireInRequestsWireInRequestUuidHeaderXGustoAPIVersion.md)                                                                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetWireInRequestsWireInRequestUuidResponse](../../models/operations/GetWireInRequestsWireInRequestUuidResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## submit

Submit a wire in request for a payment

scope: `payrolls:run`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-wire_in_requests-wire_in_request_uuid" method="put" path="/v1/wire_in_requests/{wire_in_request_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.WireInRequestUpdateRequestBody;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutWireInRequestsWireInRequestUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutWireInRequestsWireInRequestUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutWireInRequestsWireInRequestUuidResponse res = sdk.wireInRequests().submit()
                .wireInRequestUuid("<id>")
                .xGustoAPIVersion(PutWireInRequestsWireInRequestUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .wireInRequestUpdateRequestBody(WireInRequestUpdateRequestBody.builder()
                    .dateSent("2024-06-10")
                    .bankName("Chase")
                    .amountSent("314500.00")
                    .additionalNotes("Wire for 2024-06-15 payroll.")
                    .build())
                .call();

        if (res.wireInRequest().isPresent()) {
            System.out.println(res.wireInRequest().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `wireInRequestUuid`                                                                                                                                                                                                          | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the Wire In Request                                                                                                                                                                                              |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutWireInRequestsWireInRequestUuidHeaderXGustoAPIVersion>](../../models/operations/PutWireInRequestsWireInRequestUuidHeaderXGustoAPIVersion.md)                                                                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `wireInRequestUpdateRequestBody`                                                                                                                                                                                             | [WireInRequestUpdateRequestBody](../../models/components/WireInRequestUpdateRequestBody.md)                                                                                                                                  | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutWireInRequestsWireInRequestUuidResponse](../../models/operations/PutWireInRequestsWireInRequestUuidResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## list

Fetches all Wire In Requests for a company.

scope: `payrolls:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-companies-company_uuid-wire_in_request_uuid" method="get" path="/v1/companies/{company_uuid}/wire_in_requests" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetCompaniesCompanyUuidWireInRequestUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetCompaniesCompanyUuidWireInRequestUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetCompaniesCompanyUuidWireInRequestUuidResponse res = sdk.wireInRequests().list()
                .companyUuid("<id>")
                .xGustoAPIVersion(GetCompaniesCompanyUuidWireInRequestUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .call();

        if (res.wireInRequestList().isPresent()) {
            System.out.println(res.wireInRequestList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetCompaniesCompanyUuidWireInRequestUuidHeaderXGustoAPIVersion>](../../models/operations/GetCompaniesCompanyUuidWireInRequestUuidHeaderXGustoAPIVersion.md)                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `page`                                                                                                                                                                                                                       | *Optional\<Long>*                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                           | The page that is requested. When unspecified, will load all objects unless endpoint forces pagination.                                                                                                                       |
| `per`                                                                                                                                                                                                                        | *Optional\<Long>*                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                           | Number of objects per page. For majority of endpoints will default to 25                                                                                                                                                     |

### Response

**[GetCompaniesCompanyUuidWireInRequestUuidResponse](../../models/operations/GetCompaniesCompanyUuidWireInRequestUuidResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |