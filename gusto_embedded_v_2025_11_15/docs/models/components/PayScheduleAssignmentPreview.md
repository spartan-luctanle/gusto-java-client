# PayScheduleAssignmentPreview

The representation of a pay schedule assignment preview.


## Fields

| Field                                                                                                          | Type                                                                                                           | Required                                                                                                       | Description                                                                                                    |
| -------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `type`                                                                                                         | [JsonNullable\<PayScheduleAssignmentPreviewType>](../../models/components/PayScheduleAssignmentPreviewType.md) | :heavy_minus_sign:                                                                                             | The pay schedule assignment type.                                                                              |
| `employeeChanges`                                                                                              | List\<[PayScheduleAssignmentEmployeeChange](../../models/components/PayScheduleAssignmentEmployeeChange.md)>   | :heavy_minus_sign:                                                                                             | A list of pay schedule changes including pay period and transition pay period.                                 |