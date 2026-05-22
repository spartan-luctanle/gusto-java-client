# Flows

## Overview

### Available Operations

* [create](#create) - Create a flow

## create

Generate a link to access a pre-built workflow in Gusto white-label UI. For security, all generated flows will expire within 1 hour of inactivity or 24 hours from creation time, whichever comes first.

You can see a list of all possible flow types in our [Flow Types](https://docs.gusto.com/embedded-payroll/docs/flow-types) guide.

You can also mix and match flow_types in the same category to create custom flows suitable for your needs.

For instance, to create a custom onboarding flow that only includes `add_addresses`, `add_employees`, and `sign_all_forms` steps, simply stitch those flow_types together into a comma delimited string:

```json
{
  "flow_type": "add_addresses,add_employees,sign_all_forms"
}
```

Please be mindful of data dependencies in each step to achieve the best user experience.

For more information and in-depth guides review the [Getting Started](https://docs.gusto.com/embedded-payroll/docs/flows-getting-started) guide for flows.

scope: `flows:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="post-v1-company-flows" method="post" path="/v1/companies/{company_uuid}/flows" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.CreateFlowRequest;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1CompanyFlowsHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PostV1CompanyFlowsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostV1CompanyFlowsResponse res = sdk.flows().create()
                .xGustoAPIVersion(PostV1CompanyFlowsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyUuid("<id>")
                .createFlowRequest(CreateFlowRequest.builder()
                    .flowType("company_onboarding")
                    .build())
                .call();

        if (res.flow().isPresent()) {
            System.out.println(res.flow().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1CompanyFlowsHeaderXGustoAPIVersion>](../../models/operations/PostV1CompanyFlowsHeaderXGustoAPIVersion.md)                                                                                                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `createFlowRequest`                                                                                                                                                                                                          | [CreateFlowRequest](../../models/components/CreateFlowRequest.md)                                                                                                                                                            | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1CompanyFlowsResponse](../../models/operations/PostV1CompanyFlowsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |