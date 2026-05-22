# PeopleBatches

## Overview

### Available Operations

* [postV1CompaniesCompanyIdPeopleBatches](#postv1companiescompanyidpeoplebatches) - Create a people batch
* [getV1PeopleBatchesPeopleBatchUuid](#getv1peoplebatchespeoplebatchuuid) - Get a people batch

## postV1CompaniesCompanyIdPeopleBatches

Creates a batch for bulk employee creation.

The batch is processed asynchronously. Use the returned batch UUID to poll for status and results.

scope: `people_batches:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-companies-company_id-people_batches" method="post" path="/v1/companies/{company_id}/people_batches" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.*;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, PeopleBatchConflictError, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompaniesCompanyIdPeopleBatchesResponse res = sdk.peopleBatches().postV1CompaniesCompanyIdPeopleBatches()
                .companyId("<id>")
                .xGustoAPIVersion(PostV1CompaniesCompanyIdPeopleBatchesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .requestBody(PostV1CompaniesCompanyIdPeopleBatchesRequestBody.builder()
                    .idempotencyKey("550e8400-e29b-41d4-a716-446655440000")
                    .batchAction(BatchAction.CREATE)
                    .batch(List.of())
                    .build())
                .call();

        if (res.peopleBatch().isPresent()) {
            System.out.println(res.peopleBatch().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompaniesCompanyIdPeopleBatchesHeaderXGustoAPIVersion>](../../models/operations/PostV1CompaniesCompanyIdPeopleBatchesHeaderXGustoAPIVersion.md)                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `requestBody`                                                                                                                                                                                                                | [PostV1CompaniesCompanyIdPeopleBatchesRequestBody](../../models/operations/PostV1CompaniesCompanyIdPeopleBatchesRequestBody.md)                                                                                              | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompaniesCompanyIdPeopleBatchesResponse](../../models/operations/PostV1CompaniesCompanyIdPeopleBatchesResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/PeopleBatchConflictError | 409                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getV1PeopleBatchesPeopleBatchUuid

Returns the status and results of a people batch.

Poll this endpoint to check the batch processing status and retrieve results.

scope: `people_batches:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-people_batches-people_batch_uuid" method="get" path="/v1/people_batches/{people_batch_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1PeopleBatchesPeopleBatchUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1PeopleBatchesPeopleBatchUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1PeopleBatchesPeopleBatchUuidResponse res = sdk.peopleBatches().getV1PeopleBatchesPeopleBatchUuid()
                .peopleBatchUuid("<id>")
                .xGustoAPIVersion(GetV1PeopleBatchesPeopleBatchUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .call();

        if (res.peopleBatchResults().isPresent()) {
            System.out.println(res.peopleBatchResults().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `peopleBatchUuid`                                                                                                                                                                                                            | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the people batch                                                                                                                                                                                                 |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1PeopleBatchesPeopleBatchUuidHeaderXGustoAPIVersion>](../../models/operations/GetV1PeopleBatchesPeopleBatchUuidHeaderXGustoAPIVersion.md)                                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1PeopleBatchesPeopleBatchUuidResponse](../../models/operations/GetV1PeopleBatchesPeopleBatchUuidResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |