# HistoricalEmployeeBodyHomeAddress

Residential address on file for tax withholding and compliance mail.


## Fields

| Field                                                   | Type                                                    | Required                                                | Description                                             | Example                                                 |
| ------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------- |
| `street1`                                               | *String*                                                | :heavy_check_mark:                                      | Street address line 1.                                  | 55 Mission St                                           |
| `street2`                                               | *JsonNullable\<String>*                                 | :heavy_minus_sign:                                      | Apartment, suite, unit, or building (optional).         | Floor 3                                                 |
| `city`                                                  | *String*                                                | :heavy_check_mark:                                      | City.                                                   | San Francisco                                           |
| `state`                                                 | *String*                                                | :heavy_check_mark:                                      | Two-letter U.S. state or territory postal abbreviation. | CA                                                      |
| `zip`                                                   | *String*                                                | :heavy_check_mark:                                      | ZIP or ZIP+4.                                           | 94105                                                   |