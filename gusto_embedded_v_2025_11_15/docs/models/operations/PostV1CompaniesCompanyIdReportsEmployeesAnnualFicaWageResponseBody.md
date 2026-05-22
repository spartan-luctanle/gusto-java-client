# PostV1CompaniesCompanyIdReportsEmployeesAnnualFicaWageResponseBody

accepted


## Fields

| Field                                                                   | Type                                                                    | Required                                                                | Description                                                             |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `requestUuid`                                                           | *String*                                                                | :heavy_check_mark:                                                      | The UUID of the report request. Use this to poll for report completion. |
| `companyUuid`                                                           | *String*                                                                | :heavy_check_mark:                                                      | The UUID of the company                                                 |
| `startYear`                                                             | *long*                                                                  | :heavy_check_mark:                                                      | The start year for the report                                           |
| `endYear`                                                               | *long*                                                                  | :heavy_check_mark:                                                      | The end year for the report                                             |