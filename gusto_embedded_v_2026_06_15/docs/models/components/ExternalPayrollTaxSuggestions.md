# ExternalPayrollTaxSuggestions

The representation of an external payroll with minimal information.


## Fields

| Field                                                              | Type                                                               | Required                                                           | Description                                                        |
| ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ |
| `employeeUuid`                                                     | *Optional\<String>*                                                | :heavy_minus_sign:                                                 | The UUID of the employee.                                          |
| `taxSuggestions`                                                   | List\<[TaxSuggestions](../../models/components/TaxSuggestions.md)> | :heavy_minus_sign:                                                 | Possible tax liabilities selections.                               |