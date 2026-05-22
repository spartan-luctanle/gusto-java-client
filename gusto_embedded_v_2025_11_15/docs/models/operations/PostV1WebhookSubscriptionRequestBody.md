# PostV1WebhookSubscriptionRequestBody


## Fields

| Field                                                                    | Type                                                                     | Required                                                                 | Description                                                              |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| `url`                                                                    | *String*                                                                 | :heavy_check_mark:                                                       | The URL where webhook events will be POSTed.                             |
| `subscriptionTypes`                                                      | List\<[SubscriptionTypes](../../models/operations/SubscriptionTypes.md)> | :heavy_check_mark:                                                       | The types of events to subscribe to.                                     |