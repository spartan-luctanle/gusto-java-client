# PostV1CompaniesCompanyIdPeopleBatchesRequestBody


## Fields

| Field                                                          | Type                                                           | Required                                                       | Description                                                    | Example                                                        |
| -------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------- |
| `idempotencyKey`                                               | *String*                                                       | :heavy_check_mark:                                             | A unique identifier to ensure idempotency of the batch request | 550e8400-e29b-41d4-a716-446655440000                           |
| `batchAction`                                                  | [BatchAction](../../models/operations/BatchAction.md)          | :heavy_check_mark:                                             | The action to perform on the batch                             | create                                                         |
| `batch`                                                        | List\<[Batch](../../models/operations/Batch.md)>               | :heavy_check_mark:                                             | Array of people to create                                      |                                                                |