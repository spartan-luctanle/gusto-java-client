# SetupStatus

The current status of the state tax setup.
- `not_started`: No requirements have been filled
- `in_progress`: Some requirements have been filled, or default rates are applied
- `complete`: All requirements have been filled without default rates


## Example Usage

```java
import com.gusto.embedded_api_v_2025_11_15.models.components.SetupStatus;

SetupStatus value = SetupStatus.NOT_STARTED;
```


## Values

| Name          | Value         |
| ------------- | ------------- |
| `NOT_STARTED` | not_started   |
| `IN_PROGRESS` | in_progress   |
| `COMPLETE`    | complete      |