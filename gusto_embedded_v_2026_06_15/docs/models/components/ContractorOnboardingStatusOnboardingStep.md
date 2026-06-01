# ContractorOnboardingStatusOnboardingStep


## Fields

| Field                                                   | Type                                                    | Required                                                | Description                                             |
| ------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------- |
| `title`                                                 | *Optional\<String>*                                     | :heavy_minus_sign:                                      | User-friendly description of the onboarding step.       |
| `id`                                                    | *Optional\<String>*                                     | :heavy_minus_sign:                                      | String identifier for the onboarding step.              |
| `required`                                              | *Optional\<Boolean>*                                    | :heavy_minus_sign:                                      | When true, this step is required.                       |
| `completed`                                             | *Optional\<Boolean>*                                    | :heavy_minus_sign:                                      | When true, this step has been completed.                |
| `requirements`                                          | List\<*String*>                                         | :heavy_minus_sign:                                      | A list of onboarding steps required to begin this step. |