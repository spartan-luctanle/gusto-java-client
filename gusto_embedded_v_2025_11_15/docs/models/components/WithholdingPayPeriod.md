# WithholdingPayPeriod

The payment schedule tax rate the payroll is based on. Only relevant for off-cycle payrolls.

## Example Usage

```java
import com.gusto.embedded_api_v_2025_11_15.models.components.WithholdingPayPeriod;

WithholdingPayPeriod value = WithholdingPayPeriod.EVERY_WEEK;
```


## Values

| Name               | Value              |
| ------------------ | ------------------ |
| `EVERY_WEEK`       | Every week         |
| `EVERY_OTHER_WEEK` | Every other week   |
| `TWICE_PER_MONTH`  | Twice per month    |
| `MONTHLY`          | Monthly            |
| `QUARTERLY`        | Quarterly          |
| `SEMIANNUALLY`     | Semiannually       |
| `ANNUALLY`         | Annually           |