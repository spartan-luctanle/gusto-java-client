# EmployeeMemberPortalInvitationStatus

Member portal invitation status information. Only included when the include param has the portal_invitations value set.


## Fields

| Field                                                                                     | Type                                                                                      | Required                                                                                  | Description                                                                               |
| ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| `status`                                                                                  | [Optional\<EmployeeStatus>](../../models/components/EmployeeStatus.md)                    | :heavy_minus_sign:                                                                        | The current status of the member portal invitation.                                       |
| `tokenExpired`                                                                            | *JsonNullable\<Boolean>*                                                                  | :heavy_minus_sign:                                                                        | Whether the invitation token has expired.                                                 |
| `welcomeEmailSentAt`                                                                      | [OffsetDateTime](https://docs.oracle.com/javase/8/docs/api/java/time/OffsetDateTime.html) | :heavy_minus_sign:                                                                        | The date and time when the welcome email was sent.                                        |
| `lastPasswordResentAt`                                                                    | [OffsetDateTime](https://docs.oracle.com/javase/8/docs/api/java/time/OffsetDateTime.html) | :heavy_minus_sign:                                                                        | The date and time when the password reset was last resent.                                |