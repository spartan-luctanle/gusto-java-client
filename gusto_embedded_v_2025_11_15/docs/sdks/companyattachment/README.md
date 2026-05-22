# CompanyAttachment

## Overview

### Available Operations

* [getDownloadUrl](#getdownloadurl) - Get a temporary url to download the Company Attachment file

## getDownloadUrl

Retrieve a temporary url to download an attachment file uploaded by the company.

### Related guides
- [Manage company attachments](doc:manage-company-attachments)

scope: `company_attachments:read`

### Example Usage

<!-- UsageSnippet language="java" operationID="get-v1-companies-attachment-url" method="get" path="/v1/companies/{company_id}/attachments/{company_attachment_uuid}/download_url" -->
```java
package hello.world;

import com.gusto.embedded_api_v_2025_11_15.GustoEmbedded;
import com.gusto.embedded_api_v_2025_11_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesAttachmentUrlHeaderXGustoAPIVersion;
import com.gusto.embedded_api_v_2025_11_15.models.operations.GetV1CompaniesAttachmentUrlResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1CompaniesAttachmentUrlResponse res = sdk.companyAttachment().getDownloadUrl()
                .xGustoAPIVersion(GetV1CompaniesAttachmentUrlHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS11_MINUS15)
                .companyId("<id>")
                .companyAttachmentUuid("<id>")
                .call();

        if (res.companyAttachmentDownloadUrl().isPresent()) {
            System.out.println(res.companyAttachmentDownloadUrl().get());
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xGustoAPIVersion`                                                                                                                                                                                                           | [Optional\<GetV1CompaniesAttachmentUrlHeaderXGustoAPIVersion>](../../models/operations/GetV1CompaniesAttachmentUrlHeaderXGustoAPIVersion.md)                                                                                 | :heavy_minus_sign:                                                                                                                                                                                                           | Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used. |
| `companyId`                                                                                                                                                                                                                  | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company                                                                                                                                                                                                      |
| `companyAttachmentUuid`                                                                                                                                                                                                      | *String*                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                           | The UUID of the company attachment                                                                                                                                                                                           |

### Response

**[GetV1CompaniesAttachmentUrlResponse](../../models/operations/GetV1CompaniesAttachmentUrlResponse.md)**

### Errors

| Error Type                        | Status Code                       | Content Type                      |
| --------------------------------- | --------------------------------- | --------------------------------- |
| models/errors/NotFoundErrorObject | 404                               | application/json                  |
| models/errors/APIException        | 4XX, 5XX                          | \*/\*                             |