# PaidHoliday

A paid holiday derived from the company's holiday pay policy


## Fields

| Field                                               | Type                                                | Required                                            | Description                                         |
| --------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------- |
| `holidayKey`                                        | *JsonNullable\<String>*                             | :heavy_minus_sign:                                  | The holiday's identifier (null for custom holidays) |
| `holidayName`                                       | *Optional\<String>*                                 | :heavy_minus_sign:                                  | The holiday's official name                         |
| `startDate`                                         | *Optional\<String>*                                 | :heavy_minus_sign:                                  | The holiday's start date (YYYY-MM-DD)               |
| `endDate`                                           | *Optional\<String>*                                 | :heavy_minus_sign:                                  | The holiday's end date (YYYY-MM-DD)                 |