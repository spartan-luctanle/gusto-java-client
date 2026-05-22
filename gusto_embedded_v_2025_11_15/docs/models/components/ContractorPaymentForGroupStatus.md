# ContractorPaymentForGroupStatus

The status of the contractor payment.  Will transition to `Funded` during payments processing if the payment should be funded, i.e. has `Direct Deposit` for payment method. Contractors payments with `Check` payment method will remain `Unfunded`.

## Example Usage

```java
import com.gusto.embedded_api_v_2025_11_15.models.components.ContractorPaymentForGroupStatus;

ContractorPaymentForGroupStatus value = ContractorPaymentForGroupStatus.FUNDED;
```


## Values

| Name       | Value      |
| ---------- | ---------- |
| `FUNDED`   | Funded     |
| `UNFUNDED` | Unfunded   |