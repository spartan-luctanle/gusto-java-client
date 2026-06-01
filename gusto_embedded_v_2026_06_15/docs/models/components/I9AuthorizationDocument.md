# I9AuthorizationDocument

An employee's I-9 verification document


## Fields

| Field                                     | Type                                      | Required                                  | Description                               |
| ----------------------------------------- | ----------------------------------------- | ----------------------------------------- | ----------------------------------------- |
| `uuid`                                    | *String*                                  | :heavy_check_mark:                        | The UUID of the I-9 verification document |
| `documentType`                            | *String*                                  | :heavy_check_mark:                        | The document's document type              |
| `documentTitle`                           | *String*                                  | :heavy_check_mark:                        | The document's document title             |
| `expirationDate`                          | *JsonNullable\<String>*                   | :heavy_minus_sign:                        | The document's expiration date            |
| `issuingAuthority`                        | *String*                                  | :heavy_check_mark:                        | The document's issuing authority          |