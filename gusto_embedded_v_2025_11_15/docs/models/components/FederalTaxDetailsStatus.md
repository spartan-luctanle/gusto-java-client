# FederalTaxDetailsStatus

The status of EIN verification:
- `pending`: The EIN verification process has not completed (or the company does not yet have an EIN).
- `verified`: The EIN has been successfully verified as a valid EIN with the IRS.
- `failed`: The company's EIN did not pass verification. Common issues are being entered incorrectly or not matching the company's legal name.

## Example Usage

```java
import com.gusto.embedded_api_v_2025_11_15.models.components.FederalTaxDetailsStatus;

FederalTaxDetailsStatus value = FederalTaxDetailsStatus.PENDING;
```


## Values

| Name       | Value      |
| ---------- | ---------- |
| `PENDING`  | pending    |
| `VERIFIED` | verified   |
| `FAILED`   | failed     |