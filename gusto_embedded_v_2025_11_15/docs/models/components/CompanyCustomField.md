# CompanyCustomField

A custom field on a company


## Fields

| Field                                                          | Type                                                           | Required                                                       | Description                                                    |
| -------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------- |
| `uuid`                                                         | *String*                                                       | :heavy_check_mark:                                             | UUID of the company custom field                               |
| `name`                                                         | *String*                                                       | :heavy_check_mark:                                             | Name of the company custom field                               |
| `type`                                                         | [CustomFieldType](../../models/components/CustomFieldType.md)  | :heavy_check_mark:                                             | Input type for the custom field.                               |
| `description`                                                  | *JsonNullable\<String>*                                        | :heavy_minus_sign:                                             | Description of the company custom field                        |
| `selectionOptions`                                             | List\<*String*>                                                | :heavy_minus_sign:                                             | An array of options for fields of type radio. Otherwise, null. |