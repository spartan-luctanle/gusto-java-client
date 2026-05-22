# TaxLiabilitiesSelections

The representation of tax liabilities selections.


## Fields

| Field                                                                        | Type                                                                         | Required                                                                     | Description                                                                  |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `taxId`                                                                      | *Optional\<Long>*                                                            | :heavy_minus_sign:                                                           | The ID of the tax.                                                           |
| `taxName`                                                                    | *Optional\<String>*                                                          | :heavy_minus_sign:                                                           | The name of the tax.                                                         |
| `description`                                                                | *JsonNullable\<String>*                                                      | :heavy_minus_sign:                                                           | A description of the tax, providing additional detail about the tax type.    |
| `lastUnpaidExternalPayrollUuid`                                              | *JsonNullable\<String>*                                                      | :heavy_minus_sign:                                                           | The UUID of last unpaid external payroll.                                    |
| `possibleLiabilities`                                                        | List\<[PossibleLiabilities](../../models/components/PossibleLiabilities.md)> | :heavy_minus_sign:                                                           | Possible tax liabilities selections.                                         |