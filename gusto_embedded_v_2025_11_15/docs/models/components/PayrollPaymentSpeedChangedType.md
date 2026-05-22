# PayrollPaymentSpeedChangedType

Only applicable when a payroll is moved to four day processing instead of fast ach.


## Fields

| Field                                            | Type                                             | Required                                         | Description                                      |
| ------------------------------------------------ | ------------------------------------------------ | ------------------------------------------------ | ------------------------------------------------ |
| `originalCheckDate`                              | *Optional\<String>*                              | :heavy_minus_sign:                               | Original check date when fast ach applies.       |
| `currentCheckDate`                               | *Optional\<String>*                              | :heavy_minus_sign:                               | Current check date.                              |
| `originalDebitDate`                              | *Optional\<String>*                              | :heavy_minus_sign:                               | Original debit date when fast ach applies.       |
| `currentDebitDate`                               | *Optional\<String>*                              | :heavy_minus_sign:                               | Current debit date.                              |
| `reason`                                         | *Optional\<String>*                              | :heavy_minus_sign:                               | The reason why the payroll is moved to four day. |