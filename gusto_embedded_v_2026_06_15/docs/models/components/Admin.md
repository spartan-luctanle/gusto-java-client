# Admin

The representation of an admin user in Gusto.


## Fields

| Field                                      | Type                                       | Required                                   | Description                                |
| ------------------------------------------ | ------------------------------------------ | ------------------------------------------ | ------------------------------------------ |
| `uuid`                                     | *String*                                   | :heavy_check_mark:                         | The unique id of the admin.                |
| `email`                                    | *Optional\<String>*                        | :heavy_minus_sign:                         | The email of the admin for Gusto's system. |
| `firstName`                                | *Optional\<String>*                        | :heavy_minus_sign:                         | The first name of the admin.               |
| `lastName`                                 | *Optional\<String>*                        | :heavy_minus_sign:                         | The last name of the admin.                |
| `phone`                                    | *JsonNullable\<String>*                    | :heavy_minus_sign:                         | The phone number of the admin.             |