# PutV1ContractorsContractorIdPaymentMethodType

The payment method type. If type is Direct Deposit, the contractor is required to have a bank account. See [Bank account endpoint](./post-v1-contractors-contractor_uuid-bank_accounts).

## Example Usage

```java
import com.gusto.embedded_api.models.operations.PutV1ContractorsContractorIdPaymentMethodType;

PutV1ContractorsContractorIdPaymentMethodType value = PutV1ContractorsContractorIdPaymentMethodType.DIRECT_DEPOSIT;
```


## Values

| Name             | Value            |
| ---------------- | ---------------- |
| `DIRECT_DEPOSIT` | Direct Deposit   |
| `CHECK`          | Check            |