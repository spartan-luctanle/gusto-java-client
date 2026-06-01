# PostV1EmployeesEmployeeIdSalaryEstimatesRequestBody


## Fields

| Field                                                           | Type                                                            | Required                                                        | Description                                                     | Example                                                         |
| --------------------------------------------------------------- | --------------------------------------------------------------- | --------------------------------------------------------------- | --------------------------------------------------------------- | --------------------------------------------------------------- |
| `annualNetRevenue`                                              | *JsonNullable\<Double>*                                         | :heavy_minus_sign:                                              | The annual net revenue of the business (must be greater than 0) | 500000                                                          |
| `zipCode`                                                       | *String*                                                        | :heavy_check_mark:                                              | The ZIP code for location-based salary calculations             | 94107                                                           |
| `occupations`                                                   | List\<[Occupations](../../models/operations/Occupations.md)>    | :heavy_check_mark:                                              | Array of occupations. Time percentages must sum to 100%.        |                                                                 |