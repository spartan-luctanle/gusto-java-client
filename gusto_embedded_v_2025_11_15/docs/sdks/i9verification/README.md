# I9Verification

## Overview

### Available Operations

* [getAuthorization](#getauthorization) - Get an employee's I-9 authorization
* [update](#update) - Create or update an employee's I-9 authorization
* [getDocumentOptions](#getdocumentoptions) - Get an employee's I-9 verification document options
* [getDocuments](#getdocuments) - Get an employee's I-9 verification documents
* [createDocuments](#createdocuments) - Create an employee's I-9 authorization verification documents
* [deleteDocument](#deletedocument) - Delete an employee's I-9 verification document
* [employerSign](#employersign) - Employer sign an employee's Form I-9

## getAuthorization

An employee's I-9 authorization stores information about an employee's authorization status and I-9 signatures, information required to fill out the Form I-9 for employment eligibility verification.

**NOTE:** The `form_uuid` in responses from this endpoint can be used to retrieve the PDF version of the I-9. See the "get employee form PDF" request for more details.

### Related guides
- [I-9 employment verification](doc:i-9-employment-verification)

scope: `i9_authorizations:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees-employee_id-i9_authorization" method="get" path="/v1/employees/{employee_id}/i9_authorization" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1EmployeesEmployeeIdI9AuthorizationHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1EmployeesEmployeeIdI9AuthorizationResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesEmployeeIdI9AuthorizationResponse res = sdk.i9Verification().getAuthorization()
                .xGustoAPIVersion(GetV1EmployeesEmployeeIdI9AuthorizationHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .employeeId("<id>")
                .call();

        if (res.i9Authorization().isPresent()) {
            System.out.println(res.i9Authorization().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1EmployeesEmployeeIdI9AuthorizationHeaderXGustoAPIVersion>](../../models/operations/GetV1EmployeesEmployeeIdI9AuthorizationHeaderXGustoAPIVersion.md)                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |

### Response

**[GetV1EmployeesEmployeeIdI9AuthorizationResponse](../../models/operations/GetV1EmployeesEmployeeIdI9AuthorizationResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## update

An employee's I-9 authorization stores information about an employee's authorization status, as well as signatures and other information required to complete the Form I-9 for employment eligibility verification.

If the version is supplied and the employee I-9 authorization exists, this endpoint acts as an update. Otherwise, it will create an employee I-9 authorization.

Validations on this endpoint are conditional:
  * `document_type` may be required, depending on `authorization_status`.
  * Valid formats for `document_number` vary, depending on `document_type`.
  * `country` is only allowed with `document_type: 'foreign_passport'`.
  * `expiration_date` is only allowed with `authorization_status: 'alien'`.

> ℹ️ Unneeded information is automatically removed during updates.
>
> If an update causes some formerly-required fields to be unneeded, the now-unneeded data will be removed automatically.
>
> **Example:** Updating `authorization_status` from `alien` to `citizen` will cause any data in `document_type`, `document_number`, `country`, and `expiration_date` to be removed, since these fields are unused for `authorization_status:'citizen'`.

Detailed instructions for completing Form I-9 can be found at https://www.uscis.gov/sites/default/files/document/forms/i-9instr.pdf

### Related guides
- [I-9 employment verification](doc:i-9-employment-verification)

scope: `i9_authorizations:write`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-i9_authorization" method="put" path="/v1/employees/{employee_id}/i9_authorization" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.I9AuthorizationRequestBody;
import com.gusto.embedded_api_v_2025_11_15.models.components.I9AuthorizationRequestBodyAuthorizationStatus;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1EmployeesEmployeeIdI9AuthorizationHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1EmployeesEmployeeIdI9AuthorizationResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdI9AuthorizationResponse res = sdk.i9Verification().update()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdI9AuthorizationHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .employeeId("<id>")
                .i9AuthorizationRequestBody(I9AuthorizationRequestBody.builder()
                    .authorizationStatus(I9AuthorizationRequestBodyAuthorizationStatus.ALIEN)
                    .build())
                .call();

        if (res.i9Authorization().isPresent()) {
            System.out.println(res.i9Authorization().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1EmployeesEmployeeIdI9AuthorizationHeaderXGustoAPIVersion>](../../models/operations/PutV1EmployeesEmployeeIdI9AuthorizationHeaderXGustoAPIVersion.md)                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `i9AuthorizationRequestBody`                                                                                                                                                                                                 | [I9AuthorizationRequestBody](../../models/components/I9AuthorizationRequestBody.md)                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1EmployeesEmployeeIdI9AuthorizationResponse](../../models/operations/PutV1EmployeesEmployeeIdI9AuthorizationResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## getDocumentOptions

An employee's I-9 verification documents are the documents an employee has provided the employer to verify their identity and authorization to work in the United States. This endpoint returns the possible document options based on the employee's authorization status. These options can then be used to create the I-9 verification documents.

### Related guides
- [I-9 employment verification](doc:i-9-employment-verification)

scope: `i9_authorizations:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees-employee_id-i9_authorization-document_options" method="get" path="/v1/employees/{employee_id}/i9_authorization/document_options" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1EmployeesEmployeeIdI9AuthorizationDocumentOptionsHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1EmployeesEmployeeIdI9AuthorizationDocumentOptionsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesEmployeeIdI9AuthorizationDocumentOptionsResponse res = sdk.i9Verification().getDocumentOptions()
                .xGustoAPIVersion(GetV1EmployeesEmployeeIdI9AuthorizationDocumentOptionsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .employeeId("<id>")
                .call();

        if (res.i9AuthorizationDocumentOptions().isPresent()) {
            System.out.println(res.i9AuthorizationDocumentOptions().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1EmployeesEmployeeIdI9AuthorizationDocumentOptionsHeaderXGustoAPIVersion>](../../models/operations/GetV1EmployeesEmployeeIdI9AuthorizationDocumentOptionsHeaderXGustoAPIVersion.md)                           | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |

### Response

**[GetV1EmployeesEmployeeIdI9AuthorizationDocumentOptionsResponse](../../models/operations/GetV1EmployeesEmployeeIdI9AuthorizationDocumentOptionsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## getDocuments

An employee's I-9 verification documents are the documents an employee has provided the employer to verify their identity and authorization to work in the United States.

### Related guides
- [I-9 employment verification](doc:i-9-employment-verification)

scope: `i9_authorizations:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-employees-employee_id-i9_authorization-documents" method="get" path="/v1/employees/{employee_id}/i9_authorization/documents" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1EmployeesEmployeeIdI9AuthorizationDocumentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1EmployeesEmployeeIdI9AuthorizationDocumentsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1EmployeesEmployeeIdI9AuthorizationDocumentsResponse res = sdk.i9Verification().getDocuments()
                .xGustoAPIVersion(GetV1EmployeesEmployeeIdI9AuthorizationDocumentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .employeeId("<id>")
                .call();

        if (res.i9AuthorizationDocuments().isPresent()) {
            System.out.println(res.i9AuthorizationDocuments().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1EmployeesEmployeeIdI9AuthorizationDocumentsHeaderXGustoAPIVersion>](../../models/operations/GetV1EmployeesEmployeeIdI9AuthorizationDocumentsHeaderXGustoAPIVersion.md)                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |

### Response

**[GetV1EmployeesEmployeeIdI9AuthorizationDocumentsResponse](../../models/operations/GetV1EmployeesEmployeeIdI9AuthorizationDocumentsResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |

## createDocuments

An employee's I-9 verification documents are the documents an employee has provided the employer to verify their identity and authorization to work in the United States.

Use the [document options endpoint](ref:get-v1-employees-employee_id-i9_authorization-document_options) to get the possible document types and titles, which can vary depending on the employee's authorization status.

> 🚧 Every request must contain the complete list of documents for the Employee.
>
> Every request to this endpoint removes any previous verification document records for the employee.

### Related guides
- [I-9 employment verification](doc:i-9-employment-verification)

scope: `i9_authorizations:manage`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-i9_authorization-documents" method="put" path="/v1/employees/{employee_id}/i9_authorization/documents" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.I9AuthorizationDocumentsRequestBody;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1EmployeesEmployeeIdI9AuthorizationDocumentsHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1EmployeesEmployeeIdI9AuthorizationDocumentsResponse;
import java.lang.Exception;
import java.util.List;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdI9AuthorizationDocumentsResponse res = sdk.i9Verification().createDocuments()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdI9AuthorizationDocumentsHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .employeeId("<id>")
                .i9AuthorizationDocumentsRequestBody(I9AuthorizationDocumentsRequestBody.builder()
                    .documents(List.of())
                    .build())
                .call();

        if (res.i9AuthorizationDocuments().isPresent()) {
            System.out.println(res.i9AuthorizationDocuments().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1EmployeesEmployeeIdI9AuthorizationDocumentsHeaderXGustoAPIVersion>](../../models/operations/PutV1EmployeesEmployeeIdI9AuthorizationDocumentsHeaderXGustoAPIVersion.md)                                       | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `i9AuthorizationDocumentsRequestBody`                                                                                                                                                                                        | [I9AuthorizationDocumentsRequestBody](../../models/components/I9AuthorizationDocumentsRequestBody.md)                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1EmployeesEmployeeIdI9AuthorizationDocumentsResponse](../../models/operations/PutV1EmployeesEmployeeIdI9AuthorizationDocumentsResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## deleteDocument

An employee's I-9 verification documents are the documents an employee has provided the employer to verify their identity and authorization to work in the United States. This endpoint deletes a specific verification document.

### Related guides
- [I-9 employment verification](doc:i-9-employment-verification)

scope: `i9_authorizations:manage`

### Example Usage

<!-- UsageSnippet language="java" operationID="delete-v1-employees-employee_id-i9_authorization-documents-document_id" method="delete" path="/v1/employees/{employee_id}/i9_authorization/documents/{document_id}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.DeleteV1EmployeesEmployeeIdI9AuthorizationDocumentsDocumentIdHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.DeleteV1EmployeesEmployeeIdI9AuthorizationDocumentsDocumentIdResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        DeleteV1EmployeesEmployeeIdI9AuthorizationDocumentsDocumentIdResponse res = sdk.i9Verification().deleteDocument()
                .xGustoAPIVersion(DeleteV1EmployeesEmployeeIdI9AuthorizationDocumentsDocumentIdHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .employeeId("<id>")
                .documentId("<id>")
                .call();

        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<DeleteV1EmployeesEmployeeIdI9AuthorizationDocumentsDocumentIdHeaderXGustoAPIVersion>](../../models/operations/DeleteV1EmployeesEmployeeIdI9AuthorizationDocumentsDocumentIdHeaderXGustoAPIVersion.md)             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `documentId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the document                                                                                                                                                                                                     |

### Response

**[DeleteV1EmployeesEmployeeIdI9AuthorizationDocumentsDocumentIdResponse](../../models/operations/DeleteV1EmployeesEmployeeIdI9AuthorizationDocumentsDocumentIdResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |

## employerSign

Sign an employee's Form I-9 as an employer. Once the form is signed, the employee's I-9 authorization is considered complete and cannot be modified.

### Prerequisites
Before calling this endpoint:
1. The employee must have a completed [I-9 authorization](ref:put-v1-employees-employee_id-i9_authorization)
2. The employee must have signed the Form I-9
3. [I-9 verification documents](ref:put-v1-employees-employee_id-i9_authorization-documents) must be submitted

### Related guides
- [I-9 employment verification](doc:i-9-employment-verification)

scope: `i9_authorizations:manage`

### Example Usage

<!-- UsageSnippet language="java" operationID="put-v1-employees-employee_id-i9_authorization-employer_sign" method="put" path="/v1/employees/{employee_id}/i9_authorization/employer_sign" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.I9AuthorizationEmployerSignRequestBody;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1EmployeesEmployeeIdI9AuthorizationEmployerSignHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.PutV1EmployeesEmployeeIdI9AuthorizationEmployerSignResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        PutV1EmployeesEmployeeIdI9AuthorizationEmployerSignResponse res = sdk.i9Verification().employerSign()
                .xGustoAPIVersion(PutV1EmployeesEmployeeIdI9AuthorizationEmployerSignHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .employeeId("<id>")
                .i9AuthorizationEmployerSignRequestBody(I9AuthorizationEmployerSignRequestBody.builder()
                    .signatureText("<value>")
                    .signerTitle("<value>")
                    .agree(false)
                    .build())
                .call();

        if (res.i9Authorization().isPresent()) {
            System.out.println(res.i9Authorization().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<PutV1EmployeesEmployeeIdI9AuthorizationEmployerSignHeaderXGustoAPIVersion>](../../models/operations/PutV1EmployeesEmployeeIdI9AuthorizationEmployerSignHeaderXGustoAPIVersion.md)                                 | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `employeeId`                                                                                                                                                                                                                 | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the employee                                                                                                                                                                                                     |
| `xGustoClientIp`                                                                                                                                                                                                             | *Optional\<String>*                                                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                                                           | Optional header to supply the IP address. This can be used to supply the IP address for signature endpoints instead of the signed_by_ip_address parameter.                                                                   |
| `i9AuthorizationEmployerSignRequestBody`                                                                                                                                                                                     | [I9AuthorizationEmployerSignRequestBody](../../models/components/I9AuthorizationEmployerSignRequestBody.md)                                                                                                                  | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |

### Response

**[PutV1EmployeesEmployeeIdI9AuthorizationEmployerSignResponse](../../models/operations/PutV1EmployeesEmployeeIdI9AuthorizationEmployerSignResponse.md)**

### Errors

| Error Type                             | Status Code                            | Content Type                           |
| -------------------------------------- | -------------------------------------- | -------------------------------------- |
| models/errors/NotFoundErrorObject      | 404                                    | application/json                       |
| models/errors/UnprocessableEntityError | 422                                    | application/json                       |
| models/errors/APIException             | 4XX, 5XX                               | \*/\*                                  |