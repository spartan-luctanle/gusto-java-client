# SortOrder

A string indicating whether to sort resulting events in ascending (asc) or descending (desc) chronological order. Events are sorted by their `timestamp`. Defaults to asc if left empty.

## Example Usage

```java
import com.gusto.embedded_api_v_2025_11_15.models.operations.SortOrder;

SortOrder value = SortOrder.ASC;
```


## Values

| Name   | Value  |
| ------ | ------ |
| `ASC`  | asc    |
| `DESC` | desc   |