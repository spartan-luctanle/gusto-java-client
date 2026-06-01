# WebhooksHealthCheckStatus

The representation of a webhooks health check response


## Fields

| Field                                                                                                    | Type                                                                                                     | Required                                                                                                 | Description                                                                                              |
| -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| `status`                                                                                                 | [Optional\<WebhooksHealthCheckStatusStatus>](../../models/components/WebhooksHealthCheckStatusStatus.md) | :heavy_minus_sign:                                                                                       | Latest health status of the webhooks system                                                              |
| `lastCheckedAt`                                                                                          | [OffsetDateTime](https://docs.oracle.com/javase/8/docs/api/java/time/OffsetDateTime.html)                | :heavy_minus_sign:                                                                                       | ISO8601 timestamp of the last successful health check with millisecond precision                         |