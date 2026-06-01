# PayrollCalculateAccruingTimeOffHoursRequest

Request body for calculating accruing time off hours


## Fields

| Field                                           | Type                                            | Required                                        | Description                                     |
| ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- |
| `regularHoursWorked`                            | *JsonNullable\<String>*                         | :heavy_minus_sign:                              | Regular hours worked in this pay period         |
| `overtimeHoursWorked`                           | *JsonNullable\<String>*                         | :heavy_minus_sign:                              | Overtime hours worked in this pay period        |
| `doubleOvertimeHoursWorked`                     | *JsonNullable\<String>*                         | :heavy_minus_sign:                              | Double overtime hours worked in this pay period |
| `ptoHoursUsed`                                  | *JsonNullable\<String>*                         | :heavy_minus_sign:                              | Paid time off hours used in this pay period     |
| `sickHoursUsed`                                 | *JsonNullable\<String>*                         | :heavy_minus_sign:                              | Sick hours used in this pay period              |