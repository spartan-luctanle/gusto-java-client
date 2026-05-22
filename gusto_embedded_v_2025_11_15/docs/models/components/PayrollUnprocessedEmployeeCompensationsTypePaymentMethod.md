# PayrollUnprocessedEmployeeCompensationsTypePaymentMethod

The employee's compensation payment method. Is *only* `Historical` when retrieving external payrolls initially run outside of Gusto, then put into Gusto.

## Example Usage

```java
import com.gusto.embedded_api_v_2025_11_15.models.components.PayrollUnprocessedEmployeeCompensationsTypePaymentMethod;

PayrollUnprocessedEmployeeCompensationsTypePaymentMethod value = PayrollUnprocessedEmployeeCompensationsTypePaymentMethod.DIRECT_DEPOSIT;
```


## Values

| Name             | Value            |
| ---------------- | ---------------- |
| `DIRECT_DEPOSIT` | Direct Deposit   |
| `CHECK`          | Check            |
| `HISTORICAL`     | Historical       |