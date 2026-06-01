# EmployeesAnnualFicaWageReportAcceptance

Acceptance acknowledgement for an asynchronous employees annual FICA wage report. Returned with HTTP 202; poll the report status endpoint using `request_uuid`.


## Fields

| Field                                                                   | Type                                                                    | Required                                                                | Description                                                             |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `requestUuid`                                                           | *String*                                                                | :heavy_check_mark:                                                      | The UUID of the report request. Use this to poll for report completion. |
| `companyUuid`                                                           | *String*                                                                | :heavy_check_mark:                                                      | The UUID of the company.                                                |
| `startYear`                                                             | *long*                                                                  | :heavy_check_mark:                                                      | The start year for the report.                                          |
| `endYear`                                                               | *long*                                                                  | :heavy_check_mark:                                                      | The end year for the report.                                            |