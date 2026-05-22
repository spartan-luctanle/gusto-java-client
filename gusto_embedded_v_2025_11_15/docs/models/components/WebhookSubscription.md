# WebhookSubscription

The representation of webhook subscription.


## Fields

| Field                                                                                        | Type                                                                                         | Required                                                                                     | Description                                                                                  |
| -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| `uuid`                                                                                       | *String*                                                                                     | :heavy_check_mark:                                                                           | The UUID of the webhook subscription.                                                        |
| `url`                                                                                        | *Optional\<String>*                                                                          | :heavy_minus_sign:                                                                           | The webhook subscriber URL. Updates will be POSTed to this URL.                              |
| `status`                                                                                     | [Optional\<WebhookSubscriptionStatus>](../../models/components/WebhookSubscriptionStatus.md) | :heavy_minus_sign:                                                                           | The status of the webhook subscription.                                                      |
| `subscriptionTypes`                                                                          | List\<[SubscriptionTypes](../../models/components/SubscriptionTypes.md)>                     | :heavy_minus_sign:                                                                           | Receive updates for these types.                                                             |