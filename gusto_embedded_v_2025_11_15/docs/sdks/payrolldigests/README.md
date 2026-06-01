# PayrollDigests

## Overview

### Available Operations

* [postV1PayrollDigests](#postv1payrolldigests) - Create a payroll digest batch
* [getV1PayrollDigestsPayrollDigestUuid](#getv1payrolldigestspayrolldigestuuid) - Get a payroll digest batch

## postV1PayrollDigests

Triggers an asynchronous computation of payroll digest data (statuses, blockers, pay periods, totals) across up to 25 companies that the partner is mapped to.

The batch is processed asynchronously. Use the returned batch UUID to poll `GET /v1/payroll_digests/{payroll_digest_uuid}` for status and results.

Idempotency is scoped per `(partner, idempotency_key)`. A duplicate POST with the same `idempotency_key` returns a 409 Conflict referencing the existing batch UUID — no duplicate computation occurs.

📘 System Access Authentication

This endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)

scope: `payroll_digests:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-payroll_digests" method="post" path="/v1/payroll_digests" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.PayrollDigestConflictError;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws PayrollDigestConflictError, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        PostV1PayrollDigestsResponse res = sdk.payrollDigests().postV1PayrollDigests()
                .security(PostV1PayrollDigestsSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .xGustoAPIVersion(PostV1PayrollDigestsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .requestBody(PostV1PayrollDigestsRequestBody.builder()
                    .idempotencyKey("80a74f8b-2c16-45e5-9038-aa108849c6e6")
                    .batchAction(PostV1PayrollDigestsBatchAction.CREATE)
                    .batch(List.of())
                    .build())
                .call();

        if (res.payrollDigest().isPresent()) {
            System.out.println(res.payrollDigest().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `security`                                                                                                                                                                                                                   | [com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1PayrollDigestsSecurity](../../models/operations/PostV1PayrollDigestsSecurity.md)                                                                                | :heavy_check_mark:                                                                                                                                                                                                           | The security requirements to use for the request.                                                                                                                                                                            |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1PayrollDigestsHeaderXGustoAPIVersion>](../../models/operations/PostV1PayrollDigestsHeaderXGustoAPIVersion.md)                                                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `requestBody`                                                                                                                                                                                                                | [PostV1PayrollDigestsRequestBody](../../models/operations/PostV1PayrollDigestsRequestBody.md)                                                                                                                                | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1PayrollDigestsResponse](../../models/operations/PostV1PayrollDigestsResponse.md)**

### Errors

| Error Type                               | Status Code                              | Content Type                             |
| ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| models/errors/PayrollDigestConflictError | 409                                      | application/json                         |
| models/errors/UnprocessableEntityError   | 422                                      | application/json                         |
| models/errors/APIException               | 4XX, 5XX                                 | \*/\*                                    |

## getV1PayrollDigestsPayrollDigestUuid

Returns the status and results of a payroll digest batch.

Poll this endpoint until the batch `status` reaches a terminal value (`completed` or `failed`). Once terminal, the response includes the full `results` array (one entry per attempted company, each with its own per-company `status` — `success`, `partial_success`, or `failed`) and the `exclusions` array (one entry per company that could not be looked up or processed).

Note that the top-level batch `status` (`pending` / `processing` / `completed` / `failed`) is distinct from the per-company `status` returned inside `results[]` and `exclusions[]`. A `completed` batch does not imply every company succeeded — inspect the arrays for per-company outcomes.

Results are stored in Redis with a short TTL after completion. If the partner polls after results have expired, this endpoint returns 410 Gone — partners should re-submit a new batch to fetch fresh data.

📘 System Access Authentication

This endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)

scope: `payroll_digests:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-payroll_digests-payroll_digest_uuid" method="get" path="/v1/payroll_digests/{payroll_digest_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        GetV1PayrollDigestsPayrollDigestUuidResponse res = sdk.payrollDigests().getV1PayrollDigestsPayrollDigestUuid()
                .security(GetV1PayrollDigestsPayrollDigestUuidSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .payrollDigestUuid("<id>")
                .xGustoAPIVersion(GetV1PayrollDigestsPayrollDigestUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .call();

        if (res.payrollDigestResults().isPresent()) {
            System.out.println(res.payrollDigestResults().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `security`                                                                                                                                                                                                                   | [com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1PayrollDigestsPayrollDigestUuidSecurity](../../models/operations/GetV1PayrollDigestsPayrollDigestUuidSecurity.md)                                                | :heavy_check_mark:                                                                                                                                                                                                           | The security requirements to use for the request.                                                                                                                                                                            |
| `payrollDigestUuid`                                                                                                                                                                                                          | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the payroll digest batch returned by `POST /v1/payroll_digests`.                                                                                                                                                 |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1PayrollDigestsPayrollDigestUuidHeaderXGustoAPIVersion>](../../models/operations/GetV1PayrollDigestsPayrollDigestUuidHeaderXGustoAPIVersion.md)                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1PayrollDigestsPayrollDigestUuidResponse](../../models/operations/GetV1PayrollDigestsPayrollDigestUuidResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404, 410                          | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |