# CompanyOnboardingStatus

The representation of a company's onboarding status


## Fields

| Field                                                              | Type                                                               | Required                                                           | Description                                                        |
| ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ |
| `uuid`                                                             | *String*                                                           | :heavy_check_mark:                                                 | the UUID of the company                                            |
| `onboardingCompleted`                                              | *Optional\<Boolean>*                                               | :heavy_minus_sign:                                                 | a boolean flag for the company's onboarding status                 |
| `onboardingSteps`                                                  | List\<[OnboardingStep](../../models/components/OnboardingStep.md)> | :heavy_minus_sign:                                                 | a list of company onboarding steps                                 |