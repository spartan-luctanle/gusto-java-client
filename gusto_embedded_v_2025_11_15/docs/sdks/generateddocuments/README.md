# GeneratedDocuments

## Overview

### Available Operations

* [get](#get) - Get a generated document

## get

Get a document given the request_uuid. The response will include the generation request's status and urls to the document. A list of urls is returned as certain document types require several urls.

scope: `generated_documents:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-generated_documents-document_type-request_uuid" method="get" path="/v1/generated_documents/{document_type}/{request_uuid}" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.components.VersionHeader;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.DocumentType;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1GeneratedDocumentsDocumentTypeRequestUuidResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1GeneratedDocumentsDocumentTypeRequestUuidResponse res = sdk.generatedDocuments().get()
                .documentType(DocumentType.PRINTABLE_PAYROLL_CHECKS)
                .requestUuid("<id>")
                .xGustoAPIVersion(VersionHeader.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .call();

        if (res.generatedDocument().isPresent()) {
            System.out.println(res.generatedDocument().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `documentType`                                                                                                                                                                                                               | [DocumentType](../../models/operations/DocumentType.md)                                                                                                                                                                      | :heavy_check_mark:                                                                                                                                                                                                           | The type of document being generated                                                                                                                                                                                         |
| `requestUuid`                                                                                                                                                                                                                | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the request to generate a document. Generate document endpoints return request_uuids to be used with the GET generated document endpoint.                                                                        |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<VersionHeader>](../../models/components/VersionHeader.md)                                                                                                                                                         | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |

### Response

**[GetV1GeneratedDocumentsDocumentTypeRequestUuidResponse](../../models/operations/GetV1GeneratedDocumentsDocumentTypeRequestUuidResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |