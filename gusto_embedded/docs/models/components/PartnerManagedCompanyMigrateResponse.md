# PartnerManagedCompanyMigrateResponse


## Fields

| Field                                                                      | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `companyUuid`                                                              | *Optional\<String>*                                                        | :heavy_minus_sign:                                                         | The company UUID                                                           |
| `migrationStatus`                                                          | [Optional\<MigrationStatus>](../../models/components/MigrationStatus.md)   | :heavy_minus_sign:                                                         | The migration status. Always returns `success` for a successful migration. |