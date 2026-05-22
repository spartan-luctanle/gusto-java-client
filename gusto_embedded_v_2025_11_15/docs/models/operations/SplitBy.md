# SplitBy

How the payment will be split. If Percentage, split amounts must add up to exactly 100. If Amount, values are in cents and the last split amount must be null to capture the remainder.

## Example Usage

```java
import com.gusto.embedded_api_v_2025_11_15.models.operations.SplitBy;

SplitBy value = SplitBy.PERCENTAGE;
```


## Values

| Name         | Value        |
| ------------ | ------------ |
| `PERCENTAGE` | Percentage   |
| `AMOUNT`     | Amount       |