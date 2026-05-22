# Departments

## Overview

### Available Operations

* [getAll](#getall) - Get all departments of a company
* [create](#create) - Create a department
* [get](#get) - Get a department
* [update](#update) - Update a department
* [delete](#delete) - Delete a department
* [addPeople](#addpeople) - Add people to a department
* [removePeople](#removepeople) - Remove people from a department

## getAll

Get all of the departments for a given company with the employees and contractors assigned to that department.

scope: `departments:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-companies-departments" method="get" path="/v1/companies/{company_uuid}/departments" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetCompaniesDepartmentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetCompaniesDepartmentsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetCompaniesDepartmentsResponse res = sdk.departments().getAll()
                .companyUuid("<id>")
                .xGustoAPIVersion(GetCompaniesDepartmentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.departmentList().isPresent()) {
            System.out.println(res.departmentList().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetCompaniesDepartmentsHeaderXGustoAPIVersion>](../../models/operations/GetCompaniesDepartmentsHeaderXGustoAPIVersion.md)                                                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetCompaniesDepartmentsResponse](../../models/operations/GetCompaniesDepartmentsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## create

Create a department

scope: `departments:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="post-departments" method="post" path="/v1/companies/{company_uuid}/departments" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.DepartmentCreateRequestBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostDepartmentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostDepartmentsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostDepartmentsResponse res = sdk.departments().create()
                .companyUuid("<id>")
                .xGustoAPIVersion(PostDepartmentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .departmentCreateRequestBody(DepartmentCreateRequestBody.builder()
                    .title("Stage Hand")
                    .build())
                .call();

        if (res.department().isPresent()) {
            System.out.println(res.department().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="post-departments" method="post" path="/v1/companies/{company_uuid}/departments" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.DepartmentCreateRequestBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostDepartmentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostDepartmentsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostDepartmentsResponse res = sdk.departments().create()
                .companyUuid("<id>")
                .xGustoAPIVersion(PostDepartmentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .departmentCreateRequestBody(DepartmentCreateRequestBody.builder()
                    .title("Stage Hand")
                    .build())
                .call();

        if (res.department().isPresent()) {
            System.out.println(res.department().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="post-departments" method="post" path="/v1/companies/{company_uuid}/departments" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.DepartmentCreateRequestBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostDepartmentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostDepartmentsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostDepartmentsResponse res = sdk.departments().create()
                .companyUuid("<id>")
                .xGustoAPIVersion(PostDepartmentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .departmentCreateRequestBody(DepartmentCreateRequestBody.builder()
                    .title("Stage Hand")
                    .build())
                .call();

        if (res.department().isPresent()) {
            System.out.println(res.department().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="post-departments" method="post" path="/v1/companies/{company_uuid}/departments" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.DepartmentCreateRequestBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PostDepartmentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PostDepartmentsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PostDepartmentsResponse res = sdk.departments().create()
                .companyUuid("<id>")
                .xGustoAPIVersion(PostDepartmentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .departmentCreateRequestBody(DepartmentCreateRequestBody.builder()
                    .title("Stage Hand")
                    .build())
                .call();

        if (res.department().isPresent()) {
            System.out.println(res.department().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `companyUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PostDepartmentsHeaderXGustoAPIVersion>](../../models/operations/PostDepartmentsHeaderXGustoAPIVersion.md)                                                                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `departmentCreateRequestBody`                                                                                                                                                                                                | [DepartmentCreateRequestBody](../../models/components/DepartmentCreateRequestBody.md)                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PostDepartmentsResponse](../../models/operations/PostDepartmentsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## get

Get a department given the UUID

scope: `departments:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-department" method="get" path="/v1/departments/{department_uuid}" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.operations.GetDepartmentHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.GetDepartmentResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetDepartmentResponse res = sdk.departments().get()
                .departmentUuid("<id>")
                .xGustoAPIVersion(GetDepartmentHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.department().isPresent()) {
            System.out.println(res.department().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `departmentUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the department                                                                                                                                                                                                   |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetDepartmentHeaderXGustoAPIVersion>](../../models/operations/GetDepartmentHeaderXGustoAPIVersion.md)                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetDepartmentResponse](../../models/operations/GetDepartmentResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## update

Update a department

scope: `departments:write`

### Example Usage: Basic

<!-- UsageSnippet language="java" operationID="put-departments" method="put" path="/v1/departments/{department_uuid}" example="Basic" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.DepartmentUpdateRequestBody;
import com.gusto.embedded_api.models.errors.*;
import com.gusto.embedded_api.models.operations.PutDepartmentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutDepartmentsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, ConflictErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutDepartmentsResponse res = sdk.departments().update()
                .departmentUuid("<id>")
                .xGustoAPIVersion(PutDepartmentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .departmentUpdateRequestBody(DepartmentUpdateRequestBody.builder()
                    .version("<value>")
                    .title("Stage Hand")
                    .build())
                .call();

        if (res.department().isPresent()) {
            System.out.println(res.department().get());
        }
    }
}
```
### Example Usage: Example

<!-- UsageSnippet language="java" operationID="put-departments" method="put" path="/v1/departments/{department_uuid}" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.DepartmentUpdateRequestBody;
import com.gusto.embedded_api.models.errors.*;
import com.gusto.embedded_api.models.operations.PutDepartmentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutDepartmentsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, ConflictErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutDepartmentsResponse res = sdk.departments().update()
                .departmentUuid("<id>")
                .xGustoAPIVersion(PutDepartmentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .departmentUpdateRequestBody(DepartmentUpdateRequestBody.builder()
                    .version("db0edd04aaac4506f7edab03ac855d56")
                    .title("Backup Dancer")
                    .build())
                .call();

        if (res.department().isPresent()) {
            System.out.println(res.department().get());
        }
    }
}
```
### Example Usage: Nested

<!-- UsageSnippet language="java" operationID="put-departments" method="put" path="/v1/departments/{department_uuid}" example="Nested" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.DepartmentUpdateRequestBody;
import com.gusto.embedded_api.models.errors.*;
import com.gusto.embedded_api.models.operations.PutDepartmentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutDepartmentsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, ConflictErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutDepartmentsResponse res = sdk.departments().update()
                .departmentUuid("<id>")
                .xGustoAPIVersion(PutDepartmentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .departmentUpdateRequestBody(DepartmentUpdateRequestBody.builder()
                    .version("<value>")
                    .title("Stage Hand")
                    .build())
                .call();

        if (res.department().isPresent()) {
            System.out.println(res.department().get());
        }
    }
}
```
### Example Usage: Resource

<!-- UsageSnippet language="java" operationID="put-departments" method="put" path="/v1/departments/{department_uuid}" example="Resource" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.DepartmentUpdateRequestBody;
import com.gusto.embedded_api.models.errors.*;
import com.gusto.embedded_api.models.operations.PutDepartmentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutDepartmentsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, ConflictErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutDepartmentsResponse res = sdk.departments().update()
                .departmentUuid("<id>")
                .xGustoAPIVersion(PutDepartmentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .departmentUpdateRequestBody(DepartmentUpdateRequestBody.builder()
                    .version("<value>")
                    .title("Stage Hand")
                    .build())
                .call();

        if (res.department().isPresent()) {
            System.out.println(res.department().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `departmentUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the department                                                                                                                                                                                                   |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutDepartmentsHeaderXGustoAPIVersion>](../../models/operations/PutDepartmentsHeaderXGustoAPIVersion.md)                                                                                                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `departmentUpdateRequestBody`                                                                                                                                                                                                | [DepartmentUpdateRequestBody](../../models/components/DepartmentUpdateRequestBody.md)                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutDepartmentsResponse](../../models/operations/PutDepartmentsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/ConflictErrorObject      | 409                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## delete

Delete a department. You cannot delete a department until all employees and contractors have been removed.

scope: `departments:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-department" method="delete" path="/v1/departments/{department_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.DeleteDepartmentHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.DeleteDepartmentResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteDepartmentResponse res = sdk.departments().delete()
                .departmentUuid("<id>")
                .xGustoAPIVersion(DeleteDepartmentHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `departmentUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the department                                                                                                                                                                                                   |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteDepartmentHeaderXGustoAPIVersion>](../../models/operations/DeleteDepartmentHeaderXGustoAPIVersion.md)                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[DeleteDepartmentResponse](../../models/operations/DeleteDepartmentResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## addPeople

Add employees and contractors to a department

scope: `departments:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-add-people-to-department" method="put" path="/v1/departments/{department_uuid}/add" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.DepartmentPeopleRequestBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutAddPeopleToDepartmentHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutAddPeopleToDepartmentResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutAddPeopleToDepartmentResponse res = sdk.departments().addPeople()
                .departmentUuid("<id>")
                .xGustoAPIVersion(PutAddPeopleToDepartmentHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .departmentPeopleRequestBody(DepartmentPeopleRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .build())
                .call();

        if (res.department().isPresent()) {
            System.out.println(res.department().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `departmentUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the department                                                                                                                                                                                                   |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutAddPeopleToDepartmentHeaderXGustoAPIVersion>](../../models/operations/PutAddPeopleToDepartmentHeaderXGustoAPIVersion.md)                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `departmentPeopleRequestBody`                                                                                                                                                                                                | [DepartmentPeopleRequestBody](../../models/components/DepartmentPeopleRequestBody.md)                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutAddPeopleToDepartmentResponse](../../models/operations/PutAddPeopleToDepartmentResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## removePeople

Remove employees and contractors from a department

scope: `departments:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-remove-people-from-department" method="put" path="/v1/departments/{department_uuid}/remove" example="Example" -->
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.DepartmentPeopleRequestBody;
import com.gusto.embedded_api.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.PutRemovePeopleFromDepartmentHeaderXGustoAPIVersion;
import com.gusto.embedded_api.models.operations.PutRemovePeopleFromDepartmentResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutRemovePeopleFromDepartmentResponse res = sdk.departments().removePeople()
                .departmentUuid("<id>")
                .xGustoAPIVersion(PutRemovePeopleFromDepartmentHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .departmentPeopleRequestBody(DepartmentPeopleRequestBody.builder()
                    .version("56d00c178bc7393b2a206ed6a86afcb4")
                    .build())
                .call();

        if (res.department().isPresent()) {
            System.out.println(res.department().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `departmentUuid`                                                                                                                                                                                                             | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the department                                                                                                                                                                                                   |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutRemovePeopleFromDepartmentHeaderXGustoAPIVersion>](../../models/operations/PutRemovePeopleFromDepartmentHeaderXGustoAPIVersion.md)                                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `departmentPeopleRequestBody`                                                                                                                                                                                                | [DepartmentPeopleRequestBody](../../models/components/DepartmentPeopleRequestBody.md)                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutRemovePeopleFromDepartmentResponse](../../models/operations/PutRemovePeopleFromDepartmentResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |