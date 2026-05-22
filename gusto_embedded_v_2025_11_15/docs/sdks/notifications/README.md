# Notifications

## Overview

### Available Operations

* [getDetails](#getdetails) - Get a notification's details
* [getCompanyNotifications](#getcompanynotifications) - Get notifications for company

## getDetails

Upon receiving a notification webhook event, use this endpoint to fetch the notification's details. The notification details include basic suggested content that can help you build notifications in your platform.

Note: partners are responsible for the delivery and any custom state management of notifications in their application. Refer to our [partner notification guide](https://docs.gusto.com/embedded-payroll/docs/partner-notifications) for more details.

If the notification UUID is not found, the response will be 404 Not Found. If the notification's supporting data is no longer valid, the response will be 422 Unprocessable Entity.

scope: `notifications:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-notifications-notification_uuid" method="get" path="/v1/notifications/{notification_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetNotificationsNotificationUuidHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetNotificationsNotificationUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetNotificationsNotificationUuidResponse res = sdk.notifications().getDetails()
                .notificationUuid("<id>")
                .xGustoAPIVersion(GetNotificationsNotificationUuidHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .call();

        if (res.notification().isPresent()) {
            System.out.println(res.notification().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `notificationUuid`                                                                                                                                                                                                           | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The notification entity_uuid                                                                                                                                                                                                 |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetNotificationsNotificationUuidHeaderXGustoAPIVersion>](../../models/operations/GetNotificationsNotificationUuidHeaderXGustoAPIVersion.md)                                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetNotificationsNotificationUuidResponse](../../models/operations/GetNotificationsNotificationUuidResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getCompanyNotifications

Returns all notifications relevant for the given company.

scope: `notifications:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-company-notifications" method="get" path="/v1/companies/{company_uuid}/notifications" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetCompanyNotificationsRequest;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetCompanyNotificationsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetCompanyNotificationsRequest req = GetCompanyNotificationsRequest.builder()
                .companyUuid("<id>")
                .build();

        GetCompanyNotificationsResponse res = sdk.notifications().getCompanyNotifications()
                .request(req)
                .call();

        if (res.notificationsList().isPresent()) {
            System.out.println(res.notificationsList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                   | Type                                                                                        | Required                                                                                    | Description                                                                                 |
| ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| `request`                                                                                   | [GetCompanyNotificationsRequest](../../models/operations/GetCompanyNotificationsRequest.md) | :heavy_check_mark:                                                                          | The request object to use for the request.                                                  |

### Response

**[GetCompanyNotificationsResponse](../../models/operations/GetCompanyNotificationsResponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| models/errors/APIException | 4XX, 5XX                   | \*/\*                      |