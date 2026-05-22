# PayrollPayrollStatusMetaType

Information about the payroll's status and expected dates


## Fields

| Field                                                                            | Type                                                                             | Required                                                                         | Description                                                                      |
| -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `cancellable`                                                                    | *Optional\<Boolean>*                                                             | :heavy_minus_sign:                                                               | true if the payroll may be cancelled.                                            |
| `expectedCheckDate`                                                              | *Optional\<String>*                                                              | :heavy_minus_sign:                                                               | The date an employee will be paid if the payroll is submitted now.               |
| `initialCheckDate`                                                               | *Optional\<String>*                                                              | :heavy_minus_sign:                                                               | The normal check date for the associated pay period.                             |
| `expectedDebitTime`                                                              | *Optional\<String>*                                                              | :heavy_minus_sign:                                                               | The time the employer's account will be debited if the payroll is submitted now. |
| `payrollLate`                                                                    | *Optional\<Boolean>*                                                             | :heavy_minus_sign:                                                               | expected_check_date > initial_check_date.                                        |
| `initialDebitCutoffTime`                                                         | *Optional\<String>*                                                              | :heavy_minus_sign:                                                               | Payroll must be submitted at or before this time to avoid late payroll.          |