# Webhooks

## Overview

### Available Operations

* [listSubscriptions](#listsubscriptions) - List webhook subscriptions
* [createSubscription](#createsubscription) - Create a webhook subscription
* [getSubscription](#getsubscription) - Get a webhook subscription
* [updateSubscription](#updatesubscription) - Update a webhook subscription
* [deleteSubscription](#deletesubscription) - Delete a webhook subscription
* [verify](#verify) - Verify a webhook subscription
* [requestVerificationToken](#requestverificationtoken) - Request a verification token for a webhook subscription
* [getV1WebhooksHealthCheck](#getv1webhookshealthcheck) - Get the webhooks health status

## listSubscriptions

Returns all webhook subscriptions associated with the provided Partner API token.

📘 System Access Authentication

This endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)

scope: `webhook_subscriptions:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-webhook-subscriptions" method="get" path="/v1/webhook_subscriptions" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        GetV1WebhookSubscriptionsResponse res = sdk.webhooks().listSubscriptions()
                .security(GetV1WebhookSubscriptionsSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .xGustoAPIVersion(GetV1WebhookSubscriptionsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.webhookSubscriptions().isPresent()) {
            System.out.println(res.webhookSubscriptions().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `security`                                                                                                                                                                                                                   | [com.gusto.embedded_api.models.operations.GetV1WebhookSubscriptionsSecurity](../../models/operations/GetV1WebhookSubscriptionsSecurity.md)                                                                                   | :heavy_check_mark:                                                                                                                                                                                                           | The security requirements to use for the request.                                                                                                                                                                            |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1WebhookSubscriptionsHeaderXGustoAPIVersion>](../../models/operations/GetV1WebhookSubscriptionsHeaderXGustoAPIVersion.md)                                                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1WebhookSubscriptionsResponse](../../models/operations/GetV1WebhookSubscriptionsResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |

## createSubscription

Create a webhook subscription to receive events of the specified subscription_types whenever there is a state change.

📘 System Access Authentication

This endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)

scope: `webhook_subscriptions:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="post-v1-webhook-subscription" method="post" path="/v1/webhook_subscriptions" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        PostV1WebhookSubscriptionResponse res = sdk.webhooks().createSubscription()
                .security(PostV1WebhookSubscriptionSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .xGustoAPIVersion(PostV1WebhookSubscriptionHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PostV1WebhookSubscriptionRequestBody.builder()
                    .url("https://slow-median.com")
                    .subscriptionTypes(List.of(
                        SubscriptionTypes.LOCATION))
                    .build())
                .call();

        if (res.webhookSubscription().isPresent()) {
            System.out.println(res.webhookSubscription().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="post-v1-webhook-subscription" method="post" path="/v1/webhook_subscriptions" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        PostV1WebhookSubscriptionResponse res = sdk.webhooks().createSubscription()
                .security(PostV1WebhookSubscriptionSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .xGustoAPIVersion(PostV1WebhookSubscriptionHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PostV1WebhookSubscriptionRequestBody.builder()
                    .url("https://partner-app.com/subscriber")
                    .subscriptionTypes(List.of(
                        SubscriptionTypes.COMPANY,
                        SubscriptionTypes.EMPLOYEE))
                    .build())
                .call();

        if (res.webhookSubscription().isPresent()) {
            System.out.println(res.webhookSubscription().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="post-v1-webhook-subscription" method="post" path="/v1/webhook_subscriptions" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        PostV1WebhookSubscriptionResponse res = sdk.webhooks().createSubscription()
                .security(PostV1WebhookSubscriptionSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .xGustoAPIVersion(PostV1WebhookSubscriptionHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PostV1WebhookSubscriptionRequestBody.builder()
                    .url("https://slow-median.com")
                    .subscriptionTypes(List.of(
                        SubscriptionTypes.LOCATION))
                    .build())
                .call();

        if (res.webhookSubscription().isPresent()) {
            System.out.println(res.webhookSubscription().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="post-v1-webhook-subscription" method="post" path="/v1/webhook_subscriptions" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        PostV1WebhookSubscriptionResponse res = sdk.webhooks().createSubscription()
                .security(PostV1WebhookSubscriptionSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .xGustoAPIVersion(PostV1WebhookSubscriptionHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PostV1WebhookSubscriptionRequestBody.builder()
                    .url("https://slow-median.com")
                    .subscriptionTypes(List.of(
                        SubscriptionTypes.LOCATION))
                    .build())
                .call();

        if (res.webhookSubscription().isPresent()) {
            System.out.println(res.webhookSubscription().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `security`                                                                                                                                                                                                                   | [com.gusto.embedded_api.models.operations.PostV1WebhookSubscriptionSecurity](../../models/operations/PostV1WebhookSubscriptionSecurity.md)                                                                                   | :heavy_check_mark:                                                                                                                                                                                                           | The security requirements to use for the request.                                                                                                                                                                            |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostV1WebhookSubscriptionHeaderXGustoAPIVersion>](../../models/operations/PostV1WebhookSubscriptionHeaderXGustoAPIVersion.md)                                                                                     | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `requestBody`                                                                                                                                                                                                                | [PostV1WebhookSubscriptionRequestBody](../../models/operations/PostV1WebhookSubscriptionRequestBody.md)                                                                                                                      | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostV1WebhookSubscriptionResponse](../../models/operations/PostV1WebhookSubscriptionResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getSubscription

Returns the Webhook Subscription associated with the provided UUID.

📘 System Access Authentication

This endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)

scope: `webhook_subscriptions:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-webhook-subscription-uuid" method="get" path="/v1/webhook_subscriptions/{webhook_subscription_uuid}" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        GetV1WebhookSubscriptionUuidResponse res = sdk.webhooks().getSubscription()
                .security(GetV1WebhookSubscriptionUuidSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .webhookSubscriptionUuid("<id>")
                .xGustoAPIVersion(GetV1WebhookSubscriptionUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.webhookSubscription().isPresent()) {
            System.out.println(res.webhookSubscription().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `security`                                                                                                                                                                                                                   | [com.gusto.embedded_api.models.operations.GetV1WebhookSubscriptionUuidSecurity](../../models/operations/GetV1WebhookSubscriptionUuidSecurity.md)                                                                             | :heavy_check_mark:                                                                                                                                                                                                           | The security requirements to use for the request.                                                                                                                                                                            |
| `webhookSubscriptionUuid`                                                                                                                                                                                                    | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The webhook subscription UUID.                                                                                                                                                                                               |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1WebhookSubscriptionUuidHeaderXGustoAPIVersion>](../../models/operations/GetV1WebhookSubscriptionUuidHeaderXGustoAPIVersion.md)                                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1WebhookSubscriptionUuidResponse](../../models/operations/GetV1WebhookSubscriptionUuidResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## updateSubscription

Updates the Webhook Subscription associated with the provided UUID.

📘 System Access Authentication

This endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)

scope: `webhook_subscriptions:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-webhook-subscription-uuid" method="put" path="/v1/webhook_subscriptions/{webhook_subscription_uuid}" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        PutV1WebhookSubscriptionUuidResponse res = sdk.webhooks().updateSubscription()
                .security(PutV1WebhookSubscriptionUuidSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .webhookSubscriptionUuid("<id>")
                .xGustoAPIVersion(PutV1WebhookSubscriptionUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PutV1WebhookSubscriptionUuidRequestBody.builder()
                    .subscriptionTypes(List.of(
                        PutV1WebhookSubscriptionUuidSubscriptionTypes.PAYROLL))
                    .build())
                .call();

        if (res.webhookSubscription().isPresent()) {
            System.out.println(res.webhookSubscription().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-webhook-subscription-uuid" method="put" path="/v1/webhook_subscriptions/{webhook_subscription_uuid}" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        PutV1WebhookSubscriptionUuidResponse res = sdk.webhooks().updateSubscription()
                .security(PutV1WebhookSubscriptionUuidSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .webhookSubscriptionUuid("<id>")
                .xGustoAPIVersion(PutV1WebhookSubscriptionUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PutV1WebhookSubscriptionUuidRequestBody.builder()
                    .subscriptionTypes(List.of(
                        PutV1WebhookSubscriptionUuidSubscriptionTypes.COMPANY,
                        PutV1WebhookSubscriptionUuidSubscriptionTypes.EMPLOYEE))
                    .build())
                .call();

        if (res.webhookSubscription().isPresent()) {
            System.out.println(res.webhookSubscription().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-webhook-subscription-uuid" method="put" path="/v1/webhook_subscriptions/{webhook_subscription_uuid}" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        PutV1WebhookSubscriptionUuidResponse res = sdk.webhooks().updateSubscription()
                .security(PutV1WebhookSubscriptionUuidSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .webhookSubscriptionUuid("<id>")
                .xGustoAPIVersion(PutV1WebhookSubscriptionUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PutV1WebhookSubscriptionUuidRequestBody.builder()
                    .subscriptionTypes(List.of(
                        PutV1WebhookSubscriptionUuidSubscriptionTypes.PAYROLL))
                    .build())
                .call();

        if (res.webhookSubscription().isPresent()) {
            System.out.println(res.webhookSubscription().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-webhook-subscription-uuid" method="put" path="/v1/webhook_subscriptions/{webhook_subscription_uuid}" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        PutV1WebhookSubscriptionUuidResponse res = sdk.webhooks().updateSubscription()
                .security(PutV1WebhookSubscriptionUuidSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .webhookSubscriptionUuid("<id>")
                .xGustoAPIVersion(PutV1WebhookSubscriptionUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PutV1WebhookSubscriptionUuidRequestBody.builder()
                    .subscriptionTypes(List.of(
                        PutV1WebhookSubscriptionUuidSubscriptionTypes.PAYROLL))
                    .build())
                .call();

        if (res.webhookSubscription().isPresent()) {
            System.out.println(res.webhookSubscription().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `security`                                                                                                                                                                                                                   | [com.gusto.embedded_api.models.operations.PutV1WebhookSubscriptionUuidSecurity](../../models/operations/PutV1WebhookSubscriptionUuidSecurity.md)                                                                             | :heavy_check_mark:                                                                                                                                                                                                           | The security requirements to use for the request.                                                                                                                                                                            |
| `webhookSubscriptionUuid`                                                                                                                                                                                                    | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The webhook subscription UUID.                                                                                                                                                                                               |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1WebhookSubscriptionUuidHeaderXGustoAPIVersion>](../../models/operations/PutV1WebhookSubscriptionUuidHeaderXGustoAPIVersion.md)                                                                               | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `requestBody`                                                                                                                                                                                                                | [PutV1WebhookSubscriptionUuidRequestBody](../../models/operations/PutV1WebhookSubscriptionUuidRequestBody.md)                                                                                                                | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1WebhookSubscriptionUuidResponse](../../models/operations/PutV1WebhookSubscriptionUuidResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## deleteSubscription

Deletes the Webhook Subscription associated with the provided UUID.

📘 System Access Authentication

This endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)

scope: `webhook_subscriptions:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-webhook-subscription-uuid" method="delete" path="/v1/webhook_subscriptions/{webhook_subscription_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        DeleteV1WebhookSubscriptionUuidResponse res = sdk.webhooks().deleteSubscription()
                .security(DeleteV1WebhookSubscriptionUuidSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .webhookSubscriptionUuid("<id>")
                .xGustoAPIVersion(DeleteV1WebhookSubscriptionUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `security`                                                                                                                                                                                                                   | [com.gusto.embedded_api.models.operations.DeleteV1WebhookSubscriptionUuidSecurity](../../models/operations/DeleteV1WebhookSubscriptionUuidSecurity.md)                                                                       | :heavy_check_mark:                                                                                                                                                                                                           | The security requirements to use for the request.                                                                                                                                                                            |
| `webhookSubscriptionUuid`                                                                                                                                                                                                    | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The webhook subscription UUID.                                                                                                                                                                                               |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1WebhookSubscriptionUuidHeaderXGustoAPIVersion>](../../models/operations/DeleteV1WebhookSubscriptionUuidHeaderXGustoAPIVersion.md)                                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[DeleteV1WebhookSubscriptionUuidResponse](../../models/operations/DeleteV1WebhookSubscriptionUuidResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## verify

When a webhook subscription is created, a `verification_token` is POSTed to the registered webhook subscription URL. This `verify` endpoint needs to be called with `verification_token` before webhook events can be sent to the registered webhook URL.

Use the /v1/webhook_subscriptions/{webhook_subscription_uuid}/request_verification_token API to resend the `verification_token` to the Subscriber.

📘 System Access Authentication

This endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)

scope: `webhook_subscriptions:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-v1-verify-webhook-subscription-uuid" method="put" path="/v1/webhook_subscriptions/{webhook_subscription_uuid}/verify" example="Basic" -->
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
            .build();

        PutV1VerifyWebhookSubscriptionUuidResponse res = sdk.webhooks().verify()
                .security(PutV1VerifyWebhookSubscriptionUuidSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .webhookSubscriptionUuid("<id>")
                .xGustoAPIVersion(PutV1VerifyWebhookSubscriptionUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PutV1VerifyWebhookSubscriptionUuidRequestBody.builder()
                    .verificationToken("<value>")
                    .build())
                .call();

        if (res.webhookSubscription().isPresent()) {
            System.out.println(res.webhookSubscription().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-v1-verify-webhook-subscription-uuid" method="put" path="/v1/webhook_subscriptions/{webhook_subscription_uuid}/verify" example="Example" -->
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
            .build();

        PutV1VerifyWebhookSubscriptionUuidResponse res = sdk.webhooks().verify()
                .security(PutV1VerifyWebhookSubscriptionUuidSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .webhookSubscriptionUuid("<id>")
                .xGustoAPIVersion(PutV1VerifyWebhookSubscriptionUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PutV1VerifyWebhookSubscriptionUuidRequestBody.builder()
                    .verificationToken("asefasedfe23e234easd")
                    .build())
                .call();

        if (res.webhookSubscription().isPresent()) {
            System.out.println(res.webhookSubscription().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-v1-verify-webhook-subscription-uuid" method="put" path="/v1/webhook_subscriptions/{webhook_subscription_uuid}/verify" example="Nested" -->
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
            .build();

        PutV1VerifyWebhookSubscriptionUuidResponse res = sdk.webhooks().verify()
                .security(PutV1VerifyWebhookSubscriptionUuidSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .webhookSubscriptionUuid("<id>")
                .xGustoAPIVersion(PutV1VerifyWebhookSubscriptionUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PutV1VerifyWebhookSubscriptionUuidRequestBody.builder()
                    .verificationToken("<value>")
                    .build())
                .call();

        if (res.webhookSubscription().isPresent()) {
            System.out.println(res.webhookSubscription().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-v1-verify-webhook-subscription-uuid" method="put" path="/v1/webhook_subscriptions/{webhook_subscription_uuid}/verify" example="Resource" -->
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
            .build();

        PutV1VerifyWebhookSubscriptionUuidResponse res = sdk.webhooks().verify()
                .security(PutV1VerifyWebhookSubscriptionUuidSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .webhookSubscriptionUuid("<id>")
                .xGustoAPIVersion(PutV1VerifyWebhookSubscriptionUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .requestBody(PutV1VerifyWebhookSubscriptionUuidRequestBody.builder()
                    .verificationToken("<value>")
                    .build())
                .call();

        if (res.webhookSubscription().isPresent()) {
            System.out.println(res.webhookSubscription().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `security`                                                                                                                                                                                                                   | [com.gusto.embedded_api.models.operations.PutV1VerifyWebhookSubscriptionUuidSecurity](../../models/operations/PutV1VerifyWebhookSubscriptionUuidSecurity.md)                                                                 | :heavy_check_mark:                                                                                                                                                                                                           | The security requirements to use for the request.                                                                                                                                                                            |
| `webhookSubscriptionUuid`                                                                                                                                                                                                    | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The webhook subscription UUID.                                                                                                                                                                                               |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1VerifyWebhookSubscriptionUuidHeaderXGustoAPIVersion>](../../models/operations/PutV1VerifyWebhookSubscriptionUuidHeaderXGustoAPIVersion.md)                                                                   | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `requestBody`                                                                                                                                                                                                                | [PutV1VerifyWebhookSubscriptionUuidRequestBody](../../models/operations/PutV1VerifyWebhookSubscriptionUuidRequestBody.md)                                                                                                    | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1VerifyWebhookSubscriptionUuidResponse](../../models/operations/PutV1VerifyWebhookSubscriptionUuidResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## requestVerificationToken

Request that the webhook subscription `verification_token` be POSTed to the Subscription URL.

📘 System Access Authentication

This endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)

scope: `webhook_subscriptions:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-webhook-subscription-verification-token-uuid" method="get" path="/v1/webhook_subscriptions/{webhook_subscription_uuid}/request_verification_token" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        GetV1WebhookSubscriptionVerificationTokenUuidResponse res = sdk.webhooks().requestVerificationToken()
                .security(GetV1WebhookSubscriptionVerificationTokenUuidSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .webhookSubscriptionUuid("<id>")
                .xGustoAPIVersion(GetV1WebhookSubscriptionVerificationTokenUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.webhookVerificationTokenResponse().isPresent()) {
            System.out.println(res.webhookVerificationTokenResponse().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `security`                                                                                                                                                                                                                   | [com.gusto.embedded_api.models.operations.GetV1WebhookSubscriptionVerificationTokenUuidSecurity](../../models/operations/GetV1WebhookSubscriptionVerificationTokenUuidSecurity.md)                                           | :heavy_check_mark:                                                                                                                                                                                                           | The security requirements to use for the request.                                                                                                                                                                            |
| `webhookSubscriptionUuid`                                                                                                                                                                                                    | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The webhook subscription UUID.                                                                                                                                                                                               |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1WebhookSubscriptionVerificationTokenUuidHeaderXGustoAPIVersion>](../../models/operations/GetV1WebhookSubscriptionVerificationTokenUuidHeaderXGustoAPIVersion.md)                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1WebhookSubscriptionVerificationTokenUuidResponse](../../models/operations/GetV1WebhookSubscriptionVerificationTokenUuidResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## getV1WebhooksHealthCheck

Returns the health status (`healthy`, `unhealthy`, or `unknown`) of the webhooks system based on the last ten minutes of activity.

📘 System Access Authentication

This endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)

scope: `webhook_subscriptions:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-webhooks-health_check" method="get" path="/v1/webhooks/health_check" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        GetV1WebhooksHealthCheckResponse res = sdk.webhooks().getV1WebhooksHealthCheck()
                .security(GetV1WebhooksHealthCheckSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .xGustoAPIVersion(GetV1WebhooksHealthCheckHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.webhooksHealthCheckStatus().isPresent()) {
            System.out.println(res.webhooksHealthCheckStatus().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `security`                                                                                                                                                                                                                   | [com.gusto.embedded_api.models.operations.GetV1WebhooksHealthCheckSecurity](../../models/operations/GetV1WebhooksHealthCheckSecurity.md)                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The security requirements to use for the request.                                                                                                                                                                            |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1WebhooksHealthCheckHeaderXGustoAPIVersion>](../../models/operations/GetV1WebhooksHealthCheckHeaderXGustoAPIVersion.md)                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1WebhooksHealthCheckResponse](../../models/operations/GetV1WebhooksHealthCheckResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |