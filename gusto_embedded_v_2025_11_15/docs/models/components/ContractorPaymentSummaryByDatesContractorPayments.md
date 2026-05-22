# ContractorPaymentSummaryByDatesContractorPayments


## Fields

| Field                                                                    | Type                                                                     | Required                                                                 | Description                                                              |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| `contractorUuid`                                                         | *Optional\<String>*                                                      | :heavy_minus_sign:                                                       | The UUID of the contractor.                                              |
| `checkDate`                                                              | *Optional\<String>*                                                      | :heavy_minus_sign:                                                       | The payment check date.                                                  |
| `reimbursementTotal`                                                     | *Optional\<String>*                                                      | :heavy_minus_sign:                                                       | The total reimbursements for the contractor within a given time period.  |
| `wageTotal`                                                              | *Optional\<String>*                                                      | :heavy_minus_sign:                                                       | The total wages for the contractor within a given time period.           |
| `payments`                                                               | List\<[ContractorPayment](../../models/components/ContractorPayment.md)> | :heavy_minus_sign:                                                       | The contractor's payments within a given time period.                    |