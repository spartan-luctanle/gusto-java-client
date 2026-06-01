# Report


## Fields

| Field                                                                                 | Type                                                                                  | Required                                                                              | Description                                                                           |
| ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| `requestUuid`                                                                         | *Optional\<String>*                                                                   | :heavy_minus_sign:                                                                    | A unique identifier of the report request                                             |
| `status`                                                                              | *Optional\<String>*                                                                   | :heavy_minus_sign:                                                                    | Current status of the report, possible values are 'succeeded', 'pending', or 'failed' |
| `reportUrls`                                                                          | List\<*String*>                                                                       | :heavy_minus_sign:                                                                    | The array of urls to access the report                                                |