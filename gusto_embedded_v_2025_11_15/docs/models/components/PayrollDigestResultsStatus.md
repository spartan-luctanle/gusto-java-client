# PayrollDigestResultsStatus

The lifecycle status of the batch request itself. Terminal values are `completed` (processing finished — inspect `results` and `exclusions` for per-company outcomes) and `failed` (request failed; can be retried). This is distinct from the per-company `status` returned inside `results[]` and `exclusions[]`.

## Example Usage

```java
import com.gusto.embedded_api_v_2025_11_15.models.components.PayrollDigestResultsStatus;

PayrollDigestResultsStatus value = PayrollDigestResultsStatus.PENDING;
```


## Values

| Name         | Value        |
| ------------ | ------------ |
| `PENDING`    | pending      |
| `PROCESSING` | processing   |
| `COMPLETED`  | completed    |
| `FAILED`     | failed       |