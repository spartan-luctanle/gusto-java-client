# SubmissionBlockers


## Fields

| Field                                                         | Type                                                          | Required                                                      | Description                                                   |
| ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- |
| `blockerType`                                                 | *Optional\<String>*                                           | :heavy_minus_sign:                                            | The type of blocker that is blocking the payment submission   |
| `selectedOption`                                              | *JsonNullable\<String>*                                       | :heavy_minus_sign:                                            | The unblock option selected to resolve the submission blocker |
| `message`                                                     | *Optional\<String>*                                           | :heavy_minus_sign:                                            | Optional message related to the blocker                       |
| `options`                                                     | List\<[Options](../../models/operations/Options.md)>          | :heavy_minus_sign:                                            | Optional array of additional options for the blocker          |