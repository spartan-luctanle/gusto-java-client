# Status

Represents the notification's status as managed by our system. It is updated based on observable system events and internal business logic, and does not reflect resolution steps taken outside our system. This field is read-only and cannot be modified via the API.

## Example Usage

```java
import com.gusto.embedded_api_v_2026_06_15.models.components.Status;

Status value = Status.OPEN;
```


## Values

| Name       | Value      |
| ---------- | ---------- |
| `OPEN`     | open       |
| `RESOLVED` | resolved   |
| `EXPIRED`  | expired    |