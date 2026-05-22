# PlaidProcessorTokenRequest

Request body for creating a verified company bank account from a Plaid processor token.


## Fields

| Field                                             | Type                                              | Required                                          | Description                                       |
| ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- |
| `ownerType`                                       | [OwnerType](../../models/components/OwnerType.md) | :heavy_check_mark:                                | The owner type of the bank account                |
| `ownerId`                                         | *String*                                          | :heavy_check_mark:                                | The owner UUID of the bank account                |
| `processorToken`                                  | *String*                                          | :heavy_check_mark:                                | The Plaid processor token                         |