# Occupations


## Fields

| Field                                                                 | Type                                                                  | Required                                                              | Description                                                           |
| --------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- |
| `code`                                                                | *String*                                                              | :heavy_check_mark:                                                    | Bureau of Labor Statistics (BLS) occupation code.                     |
| `name`                                                                | *Optional\<String>*                                                   | :heavy_minus_sign:                                                    | Occupation name.                                                      |
| `description`                                                         | *Optional\<String>*                                                   | :heavy_minus_sign:                                                    | Occupation description.                                               |
| `experienceLevel`                                                     | [ExperienceLevel](../../models/components/ExperienceLevel.md)         | :heavy_check_mark:                                                    | Experience level for this occupation.                                 |
| `timePercentage`                                                      | *String*                                                              | :heavy_check_mark:                                                    | Percentage of time spent in this occupation (as decimal string, 0-1). |
| `primary`                                                             | *Optional\<Boolean>*                                                  | :heavy_minus_sign:                                                    | Whether this is the primary occupation.                               |