# PayPeriod

The representation of a pay period.


## Fields

| Field                                                                      | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `startDate`                                                                | *Optional\<String>*                                                        | :heavy_minus_sign:                                                         | The start date, inclusive, of the pay period.                              |
| `endDate`                                                                  | *Optional\<String>*                                                        | :heavy_minus_sign:                                                         | The end date, inclusive, of the pay period.                                |
| `payScheduleUuid`                                                          | *Optional\<String>*                                                        | :heavy_minus_sign:                                                         | A unique identifier of the pay schedule to which the pay period belongs.   |
| `payroll`                                                                  | [Optional\<PayPeriodPayroll>](../../models/components/PayPeriodPayroll.md) | :heavy_minus_sign:                                                         | Information about the payroll for the pay period.                          |