# Introspection

## Overview

### Available Operations

* [getInfo](#getinfo) - Get info about the current access token
* [oauthAccessToken](#oauthaccesstoken) - Create a System Access Token or Refresh an Access Token

## getInfo

Returns scope and resource information associated with the current access token. Use this endpoint to verify the following for the current access token:
* Resource (company, employee, contractor, or application) and resource owner
* Access level

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-token-info" method="get" path="/v1/token_info" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1TokenInfoResponse;
import com.gusto.embedded_api_v_2025_11_15.models.operations.XGustoAPIVersion;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1TokenInfoResponse res = sdk.introspection().getInfo()
                .xGustoAPIVersion(XGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .call();

        if (res.tokenInfo().isPresent()) {
            System.out.println(res.tokenInfo().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<XGustoAPIVersion>](../../models/operations/XGustoAPIVersion.md)                                                                                                                                                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1TokenInfoResponse](../../models/operations/GetV1TokenInfoResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |

## oauthAccessToken

Creates a system access token or refreshes an oauth access token

### Example Usage

<!-- UsageSnippet language="java" operationID="oauth-access-token" method="post" path="/oauth/token" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.*;
import com.gusto.embedded_api_v_2025_11_15.models.operations.*;
import java.lang.Exception;
import java.lang.Object;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        OauthAccessTokenResponse res = sdk.introspection().oauthAccessToken()
                .xGustoAPIVersion(HeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .requestBody(OauthAccessTokenRequestBody.of(SystemAccessTokenRequest.builder()
                    .clientId("qr6L_9FRkbMVL_GdwvrMW6Ef8tcU6NUxjWpOfqXqOG8")
                    .clientSecret("3aQSHRB3596nZhm6NdNBELZ1u9xbZmvCrKpBhbZYq6w")
                    .grantType(RequestBodyGrantType.SYSTEM_ACCESS)
                    .build()))
                .call();

        if (res.authentication().isPresent()) {
            Authentication unionValue = res.authentication().get();
            Object raw = unionValue.value();
            if (raw instanceof CreateTokenAuthentication) {
                CreateTokenAuthentication createTokenAuthenticationValue = (CreateTokenAuthentication) raw;
                // Handle createTokenAuthentication variant
            } else if (raw instanceof RefreshTokenAuthentication) {
                RefreshTokenAuthentication refreshTokenAuthenticationValue = (RefreshTokenAuthentication) raw;
                // Handle refreshTokenAuthentication variant
            } else {
                // Unknown or unsupported variant
            }
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<HeaderXGustoAPIVersion>](../../models/operations/HeaderXGustoAPIVersion.md)                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `requestBody`                                                                                                                                                                                                                | [OauthAccessTokenRequestBody](../../models/operations/OauthAccessTokenRequestBody.md)                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[OauthAccessTokenResponse](../../models/operations/OauthAccessTokenResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |