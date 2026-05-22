# PeopleBatch

A batch for bulk people creation.


## Fields

| Field                                                             | Type                                                              | Required                                                          | Description                                                       |
| ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- |
| `uuid`                                                            | *String*                                                          | :heavy_check_mark:                                                | The unique identifier of the people batch.                        |
| `idempotencyKey`                                                  | *String*                                                          | :heavy_check_mark:                                                | The idempotency key provided when creating the batch.             |
| `status`                                                          | [PeopleBatchStatus](../../models/components/PeopleBatchStatus.md) | :heavy_check_mark:                                                | The current status of the batch processing.                       |
| `batchAction`                                                     | *String*                                                          | :heavy_check_mark:                                                | The action being performed on the batch.                          |