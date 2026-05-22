# ExternalPayrollCreateRequest

The request body for creating an external payroll.


## Fields

| Field                                                                           | Type                                                                            | Required                                                                        | Description                                                                     | Example                                                                         |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| `checkDate`                                                                     | [LocalDate](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html) | :heavy_check_mark:                                                              | The check date of the external payroll.                                         | 2022-06-03                                                                      |
| `paymentPeriodStartDate`                                                        | [LocalDate](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html) | :heavy_check_mark:                                                              | The start date of the external payroll payment period.                          | 2022-05-15                                                                      |
| `paymentPeriodEndDate`                                                          | [LocalDate](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html) | :heavy_check_mark:                                                              | The end date of the external payroll payment period.                            | 2022-05-30                                                                      |