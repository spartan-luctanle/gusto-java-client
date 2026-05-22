# PayrollReversal


## Fields

| Field                                                    | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `reversedPayrollUuid`                                    | *Optional\<String>*                                      | :heavy_minus_sign:                                       | The UUID for the payroll run being reversed.             |
| `reversalPayrollUuid`                                    | *JsonNullable\<String>*                                  | :heavy_minus_sign:                                       | The UUID of the payroll where the reversal was applied.  |
| `reason`                                                 | *Optional\<String>*                                      | :heavy_minus_sign:                                       | A reason provided by the admin who created the reversal. |
| `approvedAt`                                             | *JsonNullable\<String>*                                  | :heavy_minus_sign:                                       | Timestamp of when the reversal was approved.             |
| `category`                                               | *JsonNullable\<String>*                                  | :heavy_minus_sign:                                       | Category chosen by the admin who requested the reversal. |
| `reversedEmployeeUuids`                                  | List\<*String*>                                          | :heavy_minus_sign:                                       | Array of affected employee UUIDs.                        |