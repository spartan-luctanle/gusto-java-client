# I9AuthorizationDocumentOption

An employee's I-9 verification document option based on the authorization status


## Fields

| Field                                                                             | Type                                                                              | Required                                                                          | Description                                                                       |
| --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| `section`                                                                         | [Section](../../models/components/Section.md)                                     | :heavy_check_mark:                                                                | The document option's section in the list of acceptable documents on the Form I-9 |
| `description`                                                                     | *String*                                                                          | :heavy_check_mark:                                                                | The document option's description                                                 |
| `documentType`                                                                    | *String*                                                                          | :heavy_check_mark:                                                                | The document option's document type                                               |
| `documentTitle`                                                                   | List\<*String*>                                                                   | :heavy_check_mark:                                                                | The document option's document titles                                             |
| `commonChoice`                                                                    | *boolean*                                                                         | :heavy_check_mark:                                                                | Whether the document is a common choice for I-9 verification                      |