# CompanyBenefitWithEmployeeBenefitsSource

The source of the company benefit. This can be "internal", "external", or "partnered". Company benefits created via the API default to "external". Certain partners can create company benefits with a source of "partnered".

## Example Usage

```java
import com.gusto.embedded_api_v_2025_11_15.models.components.CompanyBenefitWithEmployeeBenefitsSource;

CompanyBenefitWithEmployeeBenefitsSource value = CompanyBenefitWithEmployeeBenefitsSource.INTERNAL;
```


## Values

| Name        | Value       |
| ----------- | ----------- |
| `INTERNAL`  | internal    |
| `EXTERNAL`  | external    |
| `PARTNERED` | partnered   |