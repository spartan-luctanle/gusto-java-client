<!-- Start SDK Example Usage [usage] -->
```java
package hello.world;

import com.gusto.embedded_api_v_2026_06_15.GustoEmbedded;
import com.gusto.embedded_api_v_2026_06_15.models.errors.NotFoundErrorObject;
import com.gusto.embedded_api_v_2026_06_15.models.operations.GetAchTransactionsRequest;
import com.gusto.embedded_api_v_2026_06_15.models.operations.GetAchTransactionsResponse;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws NotFoundErrorObject, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetAchTransactionsRequest req = GetAchTransactionsRequest.builder()
                .companyUuid("<id>")
                .build();

        GetAchTransactionsResponse res = sdk.achTransactions().getAll()
                .request(req)
                .call();

        if (res.achTransactionList().isPresent()) {
            System.out.println(res.achTransactionList().get());
        }
    }
}
```
<!-- End SDK Example Usage [usage] -->