# openapi

Developer-friendly & type-safe Java SDK specifically catered to leverage *openapi* API.

<div align="left">
    <a href="https://www.speakeasy.com/?utm_source=openapi&utm_campaign=java"><img src="https://custom-icon-badges.demolab.com/badge/-Built%20By%20Speakeasy-212015?style=for-the-badge&logoColor=FBE331&logo=speakeasy&labelColor=545454" /></a>
    <a href="https://mit-license.org/">
        <img src="https://img.shields.io/badge/License-MIT-blue.svg" style="width: 100px; height: 28px;" />
    </a>
</div>


<br /><br />
> [!IMPORTANT]
> This SDK is not yet ready for production use. To complete setup please follow the steps outlined in your [workspace](https://app.speakeasy.com/org/gusto/ruby-sdk). Delete this section before > publishing to a package manager.

<!-- Start Summary [summary] -->
## Summary

Gusto API: Welcome to Gusto's Embedded Payroll API documentation!
<!-- End Summary [summary] -->

<!-- Start Table of Contents [toc] -->
## Table of Contents
<!-- $toc-max-depth=2 -->
* [openapi](#openapi)
  * [SDK Installation](#sdk-installation)
  * [SDK Example Usage](#sdk-example-usage)
  * [Asynchronous Support](#asynchronous-support)
  * [Authentication](#authentication)
  * [Available Resources and Operations](#available-resources-and-operations)
  * [Error Handling](#error-handling)
  * [Server Selection](#server-selection)
  * [Custom HTTP Client](#custom-http-client)
  * [Debugging](#debugging)
  * [Jackson Configuration](#jackson-configuration)
* [Development](#development)
  * [Maturity](#maturity)
  * [Contributions](#contributions)

<!-- End Table of Contents [toc] -->

<!-- Start SDK Installation [installation] -->
## SDK Installation

### Getting started

JDK 11 or later is required.

The samples below show how a published SDK artifact is used:

Gradle:
```groovy
implementation 'com.gusto:embedded-api:0.3.3'
```

Maven:
```xml
<dependency>
    <groupId>com.gusto</groupId>
    <artifactId>embedded-api</artifactId>
    <version>0.3.3</version>
</dependency>
```

### How to build
After cloning the git repository to your file system you can build the SDK artifact from source to the `build` directory by running `./gradlew build` on *nix systems or `gradlew.bat` on Windows systems.

If you wish to build from source and publish the SDK artifact to your local Maven repository (on your filesystem) then use the following command (after cloning the git repo locally):

On *nix:
```bash
./gradlew publishToMavenLocal -Pskip.signing
```
On Windows:
```bash
gradlew.bat publishToMavenLocal -Pskip.signing
```
<!-- End SDK Installation [installation] -->

<!-- Start SDK Example Usage [usage] -->
## SDK Example Usage

### Example

```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.operations.GetV1TokenInfoResponse;
import com.gusto.embedded_api.models.operations.XGustoAPIVersion;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1TokenInfoResponse res = sdk.introspection().getInfo()
                .xGustoAPIVersion(XGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.tokenInfo().isPresent()) {
            System.out.println(res.tokenInfo().get());
        }
    }
}
```
#### Asynchronous Call
An asynchronous SDK client is also available that returns a [`CompletableFuture<T>`][comp-fut]. See [Asynchronous Support](#asynchronous-support) for more details on async benefits and reactive library integration.
```java
package hello.world;

import com.gusto.embedded_api.AsyncGustoEmbedded;
import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.operations.XGustoAPIVersion;
import com.gusto.embedded_api.models.operations.async.GetV1TokenInfoResponse;
import java.util.concurrent.CompletableFuture;

public class Application {

    public static void main(String[] args) {

        AsyncGustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build()
            .async();

        CompletableFuture<GetV1TokenInfoResponse> resFut = sdk.introspection().getInfo()
                .xGustoAPIVersion(XGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        resFut.thenAccept(res -> {
            if (res.tokenInfo().isPresent()) {
                System.out.println(res.tokenInfo().get());
            }
        });
    }
}
```

[comp-fut]: https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletableFuture.html

#### Union Consumption Patterns

When a response field is a union model:

- Discriminated unions: branch on the discriminator (`switch`) and then narrow to the concrete type.
- Non-discriminated unions: use generated accessors (for example `string()`, `asLong()`, `simpleObject()`) to determine the active variant.

For full model-specific examples (including Java 11/16/21 variants), see each union model's **Supported Types** section in the generated model docs.
<!-- End SDK Example Usage [usage] -->

<!-- Start Asynchronous Support [async-support] -->
## Asynchronous Support

The SDK provides comprehensive asynchronous support using Java's [`CompletableFuture<T>`][comp-fut] and [Reactive Streams `Publisher<T>`][reactive-streams] APIs. This design makes no assumptions about your choice of reactive toolkit, allowing seamless integration with any reactive library.

<details>
<summary>Why Use Async?</summary>

Asynchronous operations provide several key benefits:

- **Non-blocking I/O**: Your threads stay free for other work while operations are in flight
- **Better resource utilization**: Handle more concurrent operations with fewer threads
- **Improved scalability**: Build highly responsive applications that can handle thousands of concurrent requests
- **Reactive integration**: Works seamlessly with reactive streams and backpressure handling

</details>

<details>
<summary>Reactive Library Integration</summary>

The SDK returns [Reactive Streams `Publisher<T>`][reactive-streams] instances for operations dealing with streams involving multiple I/O interactions. We use Reactive Streams instead of JDK Flow API to provide broader compatibility with the reactive ecosystem, as most reactive libraries natively support Reactive Streams.

**Why Reactive Streams over JDK Flow?**
- **Broader ecosystem compatibility**: Most reactive libraries (Project Reactor, RxJava, Akka Streams, etc.) natively support Reactive Streams
- **Industry standard**: Reactive Streams is the de facto standard for reactive programming in Java
- **Better interoperability**: Seamless integration without additional adapters for most use cases

**Integration with Popular Libraries:**
- **Project Reactor**: Use `Flux.from(publisher)` to convert to Reactor types
- **RxJava**: Use `Flowable.fromPublisher(publisher)` for RxJava integration
- **Akka Streams**: Use `Source.fromPublisher(publisher)` for Akka Streams integration
- **Vert.x**: Use `ReadStream.fromPublisher(vertx, publisher)` for Vert.x reactive streams
- **Mutiny**: Use `Multi.createFrom().publisher(publisher)` for Quarkus Mutiny integration

**For JDK Flow API Integration:**
If you need JDK Flow API compatibility (e.g., for Quarkus/Mutiny 2), you can use adapters:
```java
// Convert Reactive Streams Publisher to Flow Publisher
Flow.Publisher<T> flowPublisher = FlowAdapters.toFlowPublisher(reactiveStreamsPublisher);

// Convert Flow Publisher to Reactive Streams Publisher
Publisher<T> reactiveStreamsPublisher = FlowAdapters.toPublisher(flowPublisher);
```

For standard single-response operations, the SDK returns `CompletableFuture<T>` for straightforward async execution.

</details>

<details>
<summary>Supported Operations</summary>

Async support is available for:

- **[Server-sent Events](#server-sent-event-streaming)**: Stream real-time events with Reactive Streams `Publisher<T>`
- **[JSONL Streaming](#jsonl-streaming)**: Process streaming JSON lines asynchronously
- **[Pagination](#pagination)**: Iterate through paginated results using `callAsPublisher()` and `callAsPublisherUnwrapped()`
- **[File Uploads](#file-uploads)**: Upload files asynchronously with progress tracking
- **[File Downloads](#file-downloads)**: Download files asynchronously with streaming support
- **[Standard Operations](#example)**: All regular API calls return `CompletableFuture<T>` for async execution

</details>

[comp-fut]: https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletableFuture.html
[reactive-streams]: https://www.reactive-streams.org/
<!-- End Asynchronous Support [async-support] -->

<!-- Start Authentication [security] -->
## Authentication

### Per-Client Security Schemes

This SDK supports the following security scheme globally:

| Name                | Type | Scheme      |
| ------------------- | ---- | ----------- |
| `companyAccessAuth` | http | HTTP Bearer |

To authenticate with the API the `companyAccessAuth` parameter must be set when initializing the SDK client instance. For example:
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.operations.GetV1TokenInfoResponse;
import com.gusto.embedded_api.models.operations.XGustoAPIVersion;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1TokenInfoResponse res = sdk.introspection().getInfo()
                .xGustoAPIVersion(XGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.tokenInfo().isPresent()) {
            System.out.println(res.tokenInfo().get());
        }
    }
}
```

### Per-Operation Security Schemes

Some operations in this SDK require the security scheme to be specified at the request level. For example:
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.*;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();

        PostV1PartnerManagedCompaniesResponse res = sdk.companies().createPartnerManaged()
                .security(PostV1PartnerManagedCompaniesSecurity.builder()
                    .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                    .build())
                .xGustoAPIVersion(PostV1PartnerManagedCompaniesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .partnerManagedCompanyCreateRequest(PartnerManagedCompanyCreateRequest.builder()
                    .user(User.builder()
                        .firstName("Frank")
                        .lastName("Ocean")
                        .email("frank@example.com")
                        .phone("2345558899")
                        .build())
                    .company(PartnerManagedCompanyCreateRequestCompany.builder()
                        .name("Frank's Ocean, LLC")
                        .tradeName("Frank’s Ocean")
                        .ein("123456789")
                        .contractorOnly(false)
                        .build())
                    .build())
                .call();

        if (res.partnerManagedCompany().isPresent()) {
            System.out.println(res.partnerManagedCompany().get());
        }
    }
}
```
<!-- End Authentication [security] -->

<!-- Start Available Resources and Operations [operations] -->
## Available Resources and Operations

<details open>
<summary>Available methods</summary>

### [AchTransactions](docs/sdks/achtransactions/README.md)

* [getAll](docs/sdks/achtransactions/README.md#getall) - Get all ACH transactions for a company

### [BankAccounts](docs/sdks/bankaccounts/README.md)

* [get](docs/sdks/bankaccounts/README.md#get) - Get all company bank accounts
* [create](docs/sdks/bankaccounts/README.md#create) - Create a company bank account
* [verify](docs/sdks/bankaccounts/README.md#verify) - Verify a company bank account
* [createFromPlaidToken](docs/sdks/bankaccounts/README.md#createfromplaidtoken) - Create a bank account from a plaid processor token
* [deleteV1CompaniesCompanyIdBankAccountsBankAccountId](docs/sdks/bankaccounts/README.md#deletev1companiescompanyidbankaccountsbankaccountid) - Delete a company bank account

### [Companies](docs/sdks/companies/README.md)

* [createPartnerManaged](docs/sdks/companies/README.md#createpartnermanaged) - Create a partner managed company
* [get](docs/sdks/companies/README.md#get) - Get a company
* [update](docs/sdks/companies/README.md#update) - Update a company
* [migrate](docs/sdks/companies/README.md#migrate) - Migrate company to embedded payroll
* [getV1PartnerManagedCompaniesCompanyUuidMigrationReadiness](docs/sdks/companies/README.md#getv1partnermanagedcompaniescompanyuuidmigrationreadiness) - Check company migration readiness
* [acceptTermsOfService](docs/sdks/companies/README.md#accepttermsofservice) - Accept terms of service for a company user
* [retrieveTermsOfService](docs/sdks/companies/README.md#retrievetermsofservice) - Retrieve terms of service status for a company user
* [listAdmins](docs/sdks/companies/README.md#listadmins) - Get all the admins at a company
* [createAdmin](docs/sdks/companies/README.md#createadmin) - Create an admin for the company
* [getOnboardingStatus](docs/sdks/companies/README.md#getonboardingstatus) - Get company onboarding status
* [finishOnboarding](docs/sdks/companies/README.md#finishonboarding) - Finish company onboarding
* [getCustomFields](docs/sdks/companies/README.md#getcustomfields) - Get the custom fields of a company

### [Companies.Suspensions](docs/sdks/suspensions/README.md)

* [get](docs/sdks/suspensions/README.md#get) - Get suspensions for this company
* [suspend](docs/sdks/suspensions/README.md#suspend) - Suspend a company's account

### [CompanyAttachment](docs/sdks/companyattachment/README.md)

* [getDownloadUrl](docs/sdks/companyattachment/README.md#getdownloadurl) - Get a temporary url to download the Company Attachment file

### [CompanyAttachments](docs/sdks/companyattachments/README.md)

* [getDetails](docs/sdks/companyattachments/README.md#getdetails) - Get Company Attachment Details
* [getList](docs/sdks/companyattachments/README.md#getlist) - Get List of Company Attachments
* [create](docs/sdks/companyattachments/README.md#create) - Create Company Attachment and Upload File

### [CompanyBenefits](docs/sdks/companybenefits/README.md)

* [list](docs/sdks/companybenefits/README.md#list) - Get benefits for a company
* [create](docs/sdks/companybenefits/README.md#create) - Create a company benefit
* [get](docs/sdks/companybenefits/README.md#get) - Get a company benefit
* [update](docs/sdks/companybenefits/README.md#update) - Update a company benefit
* [delete](docs/sdks/companybenefits/README.md#delete) - Delete a company benefit
* [getAll](docs/sdks/companybenefits/README.md#getall) - Get all supported benefits
* [getSupported](docs/sdks/companybenefits/README.md#getsupported) - Get a supported benefit
* [getSummary](docs/sdks/companybenefits/README.md#getsummary) - Get company benefit summary by company benefit id.
* [getEmployeeBenefits](docs/sdks/companybenefits/README.md#getemployeebenefits) - Get all employee benefits for a company benefit
* [updateEmployeeBenefits](docs/sdks/companybenefits/README.md#updateemployeebenefits) - Bulk update employee benefits for a company benefit
* [getRequirements](docs/sdks/companybenefits/README.md#getrequirements) - Get benefit fields requirements by benefit type
* [getV1CompanyBenefitsCompanyBenefitIdContributionExclusions](docs/sdks/companybenefits/README.md#getv1companybenefitscompanybenefitidcontributionexclusions) - Get contribution exclusions for a company benefit
* [putV1CompanyBenefitsCompanyBenefitIdContributionExclusions](docs/sdks/companybenefits/README.md#putv1companybenefitscompanybenefitidcontributionexclusions) - Update contribution exclusions for a company benefit

### [CompanyForms](docs/sdks/companyforms/README.md)

* [getAll](docs/sdks/companyforms/README.md#getall) - Get all company forms
* [get](docs/sdks/companyforms/README.md#get) - Get a company form
* [getPdf](docs/sdks/companyforms/README.md#getpdf) - Get a company form pdf
* [sign](docs/sdks/companyforms/README.md#sign) - Sign a company form

### [ContractorDocuments](docs/sdks/contractordocuments/README.md)

* [getAll](docs/sdks/contractordocuments/README.md#getall) - Get all contractor documents
* [get](docs/sdks/contractordocuments/README.md#get) - Get a contractor document
* [getPdf](docs/sdks/contractordocuments/README.md#getpdf) - Get the contractor document pdf
* [sign](docs/sdks/contractordocuments/README.md#sign) - Sign a contractor document

### [ContractorForms](docs/sdks/contractorforms/README.md)

* [list](docs/sdks/contractorforms/README.md#list) - Get all contractor forms
* [get](docs/sdks/contractorforms/README.md#get) - Get a contractor form
* [getPdf](docs/sdks/contractorforms/README.md#getpdf) - Get the contractor form pdf
* [generate1099](docs/sdks/contractorforms/README.md#generate1099) - Generate a 1099 form [DEMO]

### [ContractorPaymentGroups](docs/sdks/contractorpaymentgroups/README.md)

* [getList](docs/sdks/contractorpaymentgroups/README.md#getlist) - Get contractor payment groups for a company
* [create](docs/sdks/contractorpaymentgroups/README.md#create) - Create a contractor payment group
* [preview](docs/sdks/contractorpaymentgroups/README.md#preview) - Preview a contractor payment group
* [get](docs/sdks/contractorpaymentgroups/README.md#get) - Get a contractor payment group
* [delete](docs/sdks/contractorpaymentgroups/README.md#delete) - Cancel a contractor payment group
* [fund](docs/sdks/contractorpaymentgroups/README.md#fund) - Fund a contractor payment group [DEMO]
* [getV1ContractorPaymentGroupsIdPartnerDisbursements](docs/sdks/contractorpaymentgroups/README.md#getv1contractorpaymentgroupsidpartnerdisbursements) - Get partner disbursements for a contractor payment group
* [patchV1ContractorPaymentGroupsIdPartnerDisbursements](docs/sdks/contractorpaymentgroups/README.md#patchv1contractorpaymentgroupsidpartnerdisbursements) - Update partner disbursements for a contractor payment group

### [ContractorPaymentMethod](docs/sdks/contractorpaymentmethod/README.md)

* [getBankAccounts](docs/sdks/contractorpaymentmethod/README.md#getbankaccounts) - Get all contractor bank accounts
* [get](docs/sdks/contractorpaymentmethod/README.md#get) - Get a contractor's payment method
* [update](docs/sdks/contractorpaymentmethod/README.md#update) - Update a contractor's payment method

### [ContractorPaymentMethods](docs/sdks/contractorpaymentmethods/README.md)

* [createBankAccount](docs/sdks/contractorpaymentmethods/README.md#createbankaccount) - Create a contractor bank account

### [ContractorPayments](docs/sdks/contractorpayments/README.md)

* [getReceipt](docs/sdks/contractorpayments/README.md#getreceipt) - Get a single contractor payment receipt
* [fund](docs/sdks/contractorpayments/README.md#fund) - Fund a contractor payment [DEMO]
* [list](docs/sdks/contractorpayments/README.md#list) - Get contractor payments for a company
* [create](docs/sdks/contractorpayments/README.md#create) - Create a contractor payment
* [get](docs/sdks/contractorpayments/README.md#get) - Get a single contractor payment
* [delete](docs/sdks/contractorpayments/README.md#delete) - Cancel a contractor payment
* [preview](docs/sdks/contractorpayments/README.md#preview) - Preview contractor payment debit date
* [getV1ContractorPaymentsContractorPaymentIdPdf](docs/sdks/contractorpayments/README.md#getv1contractorpaymentscontractorpaymentidpdf) - Get a contractor payment PDF

### [Contractors](docs/sdks/contractors/README.md)

* [list](docs/sdks/contractors/README.md#list) - Get contractors of a company
* [create](docs/sdks/contractors/README.md#create) - Create a contractor
* [get](docs/sdks/contractors/README.md#get) - Get a contractor
* [update](docs/sdks/contractors/README.md#update) - Update a contractor
* [delete](docs/sdks/contractors/README.md#delete) - Delete a contractor
* [getOnboardingStatus](docs/sdks/contractors/README.md#getonboardingstatus) - Get the contractor's onboarding status
* [updateOnboardingStatus](docs/sdks/contractors/README.md#updateonboardingstatus) - Change the contractor's onboarding status
* [getAddress](docs/sdks/contractors/README.md#getaddress) - Get a contractor address
* [updateAddress](docs/sdks/contractors/README.md#updateaddress) - Create or update a contractor's address
* [getV1CompaniesCompanyIdContractorsPaymentDetails](docs/sdks/contractors/README.md#getv1companiescompanyidcontractorspaymentdetails) - List contractor payment details
* [postV1ContractorsContractorUuidRehire](docs/sdks/contractors/README.md#postv1contractorscontractoruuidrehire) - Schedule a contractor rehire
* [deleteV1ContractorsContractorUuidRehire](docs/sdks/contractors/README.md#deletev1contractorscontractoruuidrehire) - Cancel a pending contractor rehire
* [postV1ContractorsContractorUuidTermination](docs/sdks/contractors/README.md#postv1contractorscontractoruuidtermination) - Schedule a contractor termination
* [deleteV1ContractorsContractorUuidTermination](docs/sdks/contractors/README.md#deletev1contractorscontractoruuidtermination) - Cancel a pending contractor termination

### [Departments](docs/sdks/departments/README.md)

* [getAll](docs/sdks/departments/README.md#getall) - Get all departments of a company
* [create](docs/sdks/departments/README.md#create) - Create a department
* [get](docs/sdks/departments/README.md#get) - Get a department
* [update](docs/sdks/departments/README.md#update) - Update a department
* [delete](docs/sdks/departments/README.md#delete) - Delete a department
* [addPeople](docs/sdks/departments/README.md#addpeople) - Add people to a department
* [removePeople](docs/sdks/departments/README.md#removepeople) - Remove people from a department

### [EarningTypes](docs/sdks/earningtypes/README.md)

* [list](docs/sdks/earningtypes/README.md#list) - Get all earning types for a company
* [create](docs/sdks/earningtypes/README.md#create) - Create a custom earning type
* [update](docs/sdks/earningtypes/README.md#update) - Update an earning type
* [delete](docs/sdks/earningtypes/README.md#delete) - Deactivate an earning type

### [EmployeeAddresses](docs/sdks/employeeaddresses/README.md)

* [get](docs/sdks/employeeaddresses/README.md#get) - Get an employee's home addresses
* [create](docs/sdks/employeeaddresses/README.md#create) - Create an employee's home address
* [retrieveHomeAddress](docs/sdks/employeeaddresses/README.md#retrievehomeaddress) - Get an employee's home address
* [update](docs/sdks/employeeaddresses/README.md#update) - Update an employee's home address
* [delete](docs/sdks/employeeaddresses/README.md#delete) - Delete an employee's home address
* [getWorkAddresses](docs/sdks/employeeaddresses/README.md#getworkaddresses) - Get an employee's work addresses
* [createWorkAddress](docs/sdks/employeeaddresses/README.md#createworkaddress) - Create an employee work address
* [retrieveWorkAddress](docs/sdks/employeeaddresses/README.md#retrieveworkaddress) - Get an employee work address
* [updateWorkAddress](docs/sdks/employeeaddresses/README.md#updateworkaddress) - Update an employee work address
* [deleteWorkAddress](docs/sdks/employeeaddresses/README.md#deleteworkaddress) - Delete an employee's work address

### [EmployeeBenefits](docs/sdks/employeebenefits/README.md)

* [get](docs/sdks/employeebenefits/README.md#get) - Get all benefits for an employee
* [create](docs/sdks/employeebenefits/README.md#create) - Create an employee benefit
* [retrieve](docs/sdks/employeebenefits/README.md#retrieve) - Get an employee benefit
* [update](docs/sdks/employeebenefits/README.md#update) - Update an employee benefit
* [delete](docs/sdks/employeebenefits/README.md#delete) - Delete an employee benefit
* [getYtdBenefitAmountsFromDifferentCompany](docs/sdks/employeebenefits/README.md#getytdbenefitamountsfromdifferentcompany) - Get year-to-date benefit amounts from a different company
* [createYtdBenefitAmountsFromDifferentCompany](docs/sdks/employeebenefits/README.md#createytdbenefitamountsfromdifferentcompany) - Create year-to-date benefit amounts from a different company
* [getV1EmployeesEmployeeUuidSection603HighEarnerStatuses](docs/sdks/employeebenefits/README.md#getv1employeesemployeeuuidsection603highearnerstatuses) - Get all Section 603 high earner statuses for an employee
* [postV1EmployeesEmployeeUuidSection603HighEarnerStatuses](docs/sdks/employeebenefits/README.md#postv1employeesemployeeuuidsection603highearnerstatuses) - Create a Section 603 high earner status
* [getV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYear](docs/sdks/employeebenefits/README.md#getv1employeesemployeeuuidsection603highearnerstatuseseffectiveyear) - Get a Section 603 high earner status for a specific year
* [patchV1EmployeesEmployeeUuidSection603HighEarnerStatusesEffectiveYear](docs/sdks/employeebenefits/README.md#patchv1employeesemployeeuuidsection603highearnerstatuseseffectiveyear) - Update a Section 603 high earner status

### [EmployeeEmployments](docs/sdks/employeeemployments/README.md)

* [getTerminations](docs/sdks/employeeemployments/README.md#getterminations) - Get terminations for an employee
* [createTermination](docs/sdks/employeeemployments/README.md#createtermination) - Create an employee termination
* [deleteTermination](docs/sdks/employeeemployments/README.md#deletetermination) - Delete an employee termination
* [updateTermination](docs/sdks/employeeemployments/README.md#updatetermination) - Update an employee termination
* [getRehire](docs/sdks/employeeemployments/README.md#getrehire) - Get an employee rehire
* [createRehire](docs/sdks/employeeemployments/README.md#createrehire) - Create an employee rehire
* [rehire](docs/sdks/employeeemployments/README.md#rehire) - Update an employee rehire
* [deleteRehire](docs/sdks/employeeemployments/README.md#deleterehire) - Delete an employee rehire
* [getHistory](docs/sdks/employeeemployments/README.md#gethistory) - Get employment history for an employee
* [getV1TerminationsEmployeeId](docs/sdks/employeeemployments/README.md#getv1terminationsemployeeid) - Get an employee termination

### [EmployeeForms](docs/sdks/employeeforms/README.md)

* [generateW2](docs/sdks/employeeforms/README.md#generatew2) - Generate a W2 form [DEMO]
* [list](docs/sdks/employeeforms/README.md#list) - Get all employee forms
* [get](docs/sdks/employeeforms/README.md#get) - Get an employee form
* [getPdf](docs/sdks/employeeforms/README.md#getpdf) - Get the employee form pdf
* [sign](docs/sdks/employeeforms/README.md#sign) - Sign an employee form

### [EmployeePaymentMethod](docs/sdks/employeepaymentmethod/README.md)

* [create](docs/sdks/employeepaymentmethod/README.md#create) - Create an employee bank account
* [updateBankAccount](docs/sdks/employeepaymentmethod/README.md#updatebankaccount) - Update an employee bank account
* [deleteBankAccount](docs/sdks/employeepaymentmethod/README.md#deletebankaccount) - Delete an employee bank account
* [get](docs/sdks/employeepaymentmethod/README.md#get) - Get payment method for an employee
* [update](docs/sdks/employeepaymentmethod/README.md#update) - Update payment method for an employee

### [EmployeePaymentMethods](docs/sdks/employeepaymentmethods/README.md)

* [getBankAccounts](docs/sdks/employeepaymentmethods/README.md#getbankaccounts) - List employee bank accounts

### [Employees](docs/sdks/employees/README.md)

* [list](docs/sdks/employees/README.md#list) - Get employees of a company
* [create](docs/sdks/employees/README.md#create) - Create an employee
* [getV1CompaniesCompanyIdEmployeesPaymentDetails](docs/sdks/employees/README.md#getv1companiescompanyidemployeespaymentdetails) - Get employee payment details for a company
* [createHistorical](docs/sdks/employees/README.md#createhistorical) - Create a historical employee
* [get](docs/sdks/employees/README.md#get) - Get an employee
* [update](docs/sdks/employees/README.md#update) - Update an employee.
* [delete](docs/sdks/employees/README.md#delete) - Delete an onboarding employee
* [getCustomFields](docs/sdks/employees/README.md#getcustomfields) - Get an employee's custom fields
* [updateOnboardingDocumentsConfig](docs/sdks/employees/README.md#updateonboardingdocumentsconfig) - Update employee onboarding documents config
* [getOnboardingStatus](docs/sdks/employees/README.md#getonboardingstatus) - Get the employee's onboarding status
* [updateOnboardingStatus](docs/sdks/employees/README.md#updateonboardingstatus) - Update the employee's onboarding status
* [getTimeOffActivities](docs/sdks/employees/README.md#gettimeoffactivities) - Get employee time off activities

### [EmployeeTaxSetup](docs/sdks/employeetaxsetup/README.md)

* [getFederalTaxes](docs/sdks/employeetaxsetup/README.md#getfederaltaxes) - Get federal taxes for an employee
* [updateFederalTaxes](docs/sdks/employeetaxsetup/README.md#updatefederaltaxes) - Update federal taxes for an employee
* [getStateTaxes](docs/sdks/employeetaxsetup/README.md#getstatetaxes) - Get an employee's state taxes
* [updateStateTaxes](docs/sdks/employeetaxsetup/README.md#updatestatetaxes) - Update an employee's state taxes

### [Events](docs/sdks/events/README.md)

* [get](docs/sdks/events/README.md#get) - Get all events

### [ExternalPayrolls](docs/sdks/externalpayrolls/README.md)

* [get](docs/sdks/externalpayrolls/README.md#get) - Get external payrolls for a company
* [create](docs/sdks/externalpayrolls/README.md#create) - Create an external payroll for a company
* [retrieve](docs/sdks/externalpayrolls/README.md#retrieve) - Get an external payroll
* [update](docs/sdks/externalpayrolls/README.md#update) - Update an external payroll
* [delete](docs/sdks/externalpayrolls/README.md#delete) - Delete an external payroll
* [calculateTaxes](docs/sdks/externalpayrolls/README.md#calculatetaxes) - Get tax suggestions for an external payroll
* [listTaxLiabilities](docs/sdks/externalpayrolls/README.md#listtaxliabilities) - Get tax liabilities
* [updateTaxLiabilities](docs/sdks/externalpayrolls/README.md#updatetaxliabilities) - Update tax liabilities
* [finalizeTaxLiabilities](docs/sdks/externalpayrolls/README.md#finalizetaxliabilities) - Finalize tax liabilities options and convert into processed payrolls

### [FederalTaxDetails](docs/sdks/federaltaxdetails/README.md)

* [get](docs/sdks/federaltaxdetails/README.md#get) - Get a company's federal tax details
* [update](docs/sdks/federaltaxdetails/README.md#update) - Update a company's federal tax details

### [Flows](docs/sdks/flows/README.md)

* [create](docs/sdks/flows/README.md#create) - Create a flow

### [Garnishments](docs/sdks/garnishments/README.md)

* [list](docs/sdks/garnishments/README.md#list) - Get garnishments for an employee
* [create](docs/sdks/garnishments/README.md#create) - Create a garnishment
* [get](docs/sdks/garnishments/README.md#get) - Get a garnishment
* [update](docs/sdks/garnishments/README.md#update) - Update a garnishment
* [getChildSupportData](docs/sdks/garnishments/README.md#getchildsupportdata) - Get child support garnishment data

### [GeneratedDocuments](docs/sdks/generateddocuments/README.md)

* [get](docs/sdks/generateddocuments/README.md#get) - Get a generated document

### [HistoricalEmployees](docs/sdks/historicalemployees/README.md)

* [update](docs/sdks/historicalemployees/README.md#update) - Update a historical employee

### [HolidayPayPolicies](docs/sdks/holidaypaypolicies/README.md)

* [get](docs/sdks/holidaypaypolicies/README.md#get) - Get a company's holiday pay policy
* [create](docs/sdks/holidaypaypolicies/README.md#create) - Create a holiday pay policy for a company
* [update](docs/sdks/holidaypaypolicies/README.md#update) - Update a company's holiday pay policy
* [delete](docs/sdks/holidaypaypolicies/README.md#delete) - Delete a company's holiday pay policy
* [addEmployees](docs/sdks/holidaypaypolicies/README.md#addemployees) - Add employees to a company's holiday pay policy
* [removeEmployees](docs/sdks/holidaypaypolicies/README.md#removeemployees) - Remove employees from a company's holiday pay policy
* [previewPaidHolidays](docs/sdks/holidaypaypolicies/README.md#previewpaidholidays) - Preview a company's paid holidays

### [I9Verification](docs/sdks/i9verification/README.md)

* [getAuthorization](docs/sdks/i9verification/README.md#getauthorization) - Get an employee's I-9 authorization
* [update](docs/sdks/i9verification/README.md#update) - Create or update an employee's I-9 authorization
* [getDocumentOptions](docs/sdks/i9verification/README.md#getdocumentoptions) - Get an employee's I-9 verification document options
* [getDocuments](docs/sdks/i9verification/README.md#getdocuments) - Get an employee's I-9 verification documents
* [createDocuments](docs/sdks/i9verification/README.md#createdocuments) - Create an employee's I-9 authorization verification documents
* [deleteDocument](docs/sdks/i9verification/README.md#deletedocument) - Delete an employee's I-9 verification document
* [employerSign](docs/sdks/i9verification/README.md#employersign) - Employer sign an employee's Form I-9

### [IndustrySelection](docs/sdks/industryselection/README.md)

* [get](docs/sdks/industryselection/README.md#get) - Get a company industry selection
* [update](docs/sdks/industryselection/README.md#update) - Update a company industry selection

### [InformationRequests](docs/sdks/informationrequests/README.md)

* [getInformationRequests](docs/sdks/informationrequests/README.md#getinformationrequests) - Get all information requests for a company
* [submit](docs/sdks/informationrequests/README.md#submit) - Submit information request responses

### [Introspection](docs/sdks/introspection/README.md)

* [getInfo](docs/sdks/introspection/README.md#getinfo) - Get info about the current access token
* [oauthAccessToken](docs/sdks/introspection/README.md#oauthaccesstoken) - Create a System Access Token or Refresh an Access Token

### [Invoices](docs/sdks/invoices/README.md)

* [get](docs/sdks/invoices/README.md#get) - Retrieve invoicing data for companies

### [JobsAndCompensations](docs/sdks/jobsandcompensations/README.md)

* [getJobs](docs/sdks/jobsandcompensations/README.md#getjobs) - Get jobs for an employee
* [createJob](docs/sdks/jobsandcompensations/README.md#createjob) - Create a job
* [getJob](docs/sdks/jobsandcompensations/README.md#getjob) - Get a job
* [update](docs/sdks/jobsandcompensations/README.md#update) - Update a job
* [delete](docs/sdks/jobsandcompensations/README.md#delete) - Delete an individual job
* [getCompensations](docs/sdks/jobsandcompensations/README.md#getcompensations) - Get compensations for a job
* [createCompensation](docs/sdks/jobsandcompensations/README.md#createcompensation) - Create a compensation
* [getCompensation](docs/sdks/jobsandcompensations/README.md#getcompensation) - Get a compensation
* [updateCompensation](docs/sdks/jobsandcompensations/README.md#updatecompensation) - Update a compensation
* [deleteCompensation](docs/sdks/jobsandcompensations/README.md#deletecompensation) - Delete a compensation

### [Locations](docs/sdks/locations/README.md)

* [get](docs/sdks/locations/README.md#get) - Get all company locations
* [create](docs/sdks/locations/README.md#create) - Create a company location
* [retrieve](docs/sdks/locations/README.md#retrieve) - Get a location
* [update](docs/sdks/locations/README.md#update) - Update a location
* [getMinimumWages](docs/sdks/locations/README.md#getminimumwages) - Get minimum wages for a location

### [Notifications](docs/sdks/notifications/README.md)

* [getDetails](docs/sdks/notifications/README.md#getdetails) - Get a notification's details
* [getCompanyNotifications](docs/sdks/notifications/README.md#getcompanynotifications) - Get notifications for company

### [PaymentConfigs](docs/sdks/paymentconfigs/README.md)

* [get](docs/sdks/paymentconfigs/README.md#get) - Get a company's payment configs
* [update](docs/sdks/paymentconfigs/README.md#update) - Update a company's payment configs

### [Payrolls](docs/sdks/payrolls/README.md)

* [list](docs/sdks/payrolls/README.md#list) - Get all payrolls for a company
* [createOffCycle](docs/sdks/payrolls/README.md#createoffcycle) - Create an off-cycle payroll
* [getApprovedReversals](docs/sdks/payrolls/README.md#getapprovedreversals) - Get approved payroll reversals
* [get](docs/sdks/payrolls/README.md#get) - Get a single payroll
* [update](docs/sdks/payrolls/README.md#update) - Update a payroll by ID
* [delete](docs/sdks/payrolls/README.md#delete) - Delete a payroll
* [prepare](docs/sdks/payrolls/README.md#prepare) - Prepare a payroll for update
* [getReceipt](docs/sdks/payrolls/README.md#getreceipt) - Get a single payroll receipt
* [getBlockers](docs/sdks/payrolls/README.md#getblockers) - Get all payroll blockers for a company
* [skip](docs/sdks/payrolls/README.md#skip) - Skip a payroll
* [calculateGrossUp](docs/sdks/payrolls/README.md#calculategrossup) - Calculate gross up for a payroll
* [calculate](docs/sdks/payrolls/README.md#calculate) - Calculate a payroll
* [submit](docs/sdks/payrolls/README.md#submit) - Submit payroll
* [cancel](docs/sdks/payrolls/README.md#cancel) - Cancel a payroll
* [getPayStub](docs/sdks/payrolls/README.md#getpaystub) - Get an employee pay stub (pdf)
* [getPayStubs](docs/sdks/payrolls/README.md#getpaystubs) - Get an employee's pay stubs
* [generatePrintableChecks](docs/sdks/payrolls/README.md#generateprintablechecks) - Generate printable payroll checks (pdf)
* [getV1CompaniesCompanyIdPayrollsIdPartnerDisbursements](docs/sdks/payrolls/README.md#getv1companiescompanyidpayrollsidpartnerdisbursements) - Get partner disbursements for a payroll
* [patchV1CompaniesCompanyIdPayrollsIdPartnerDisbursements](docs/sdks/payrolls/README.md#patchv1companiescompanyidpayrollsidpartnerdisbursements) - Update partner disbursements for a payroll

### [PaySchedules](docs/sdks/payschedules/README.md)

* [getAll](docs/sdks/payschedules/README.md#getall) - Get the pay schedules for a company
* [create](docs/sdks/payschedules/README.md#create) - Create a new pay schedule
* [getPreview](docs/sdks/payschedules/README.md#getpreview) - Preview pay schedule dates
* [get](docs/sdks/payschedules/README.md#get) - Get a pay schedule
* [update](docs/sdks/payschedules/README.md#update) - Update a pay schedule
* [getPayPeriods](docs/sdks/payschedules/README.md#getpayperiods) - Get pay periods for a company
* [getUnprocessedTerminationPeriods](docs/sdks/payschedules/README.md#getunprocessedterminationperiods) - Get termination pay periods for a company
* [getAssignments](docs/sdks/payschedules/README.md#getassignments) - Get pay schedule assignments for a company
* [previewAssignment](docs/sdks/payschedules/README.md#previewassignment) - Preview pay schedule assignments for a company
* [assign](docs/sdks/payschedules/README.md#assign) - Assign pay schedules for a company

### [PeopleBatches](docs/sdks/peoplebatches/README.md)

* [postV1CompaniesCompanyIdPeopleBatches](docs/sdks/peoplebatches/README.md#postv1companiescompanyidpeoplebatches) - Create a people batch
* [getV1PeopleBatchesPeopleBatchUuid](docs/sdks/peoplebatches/README.md#getv1peoplebatchespeoplebatchuuid) - Get a people batch

### [RecoveryCases](docs/sdks/recoverycases/README.md)

* [get](docs/sdks/recoverycases/README.md#get) - Get all recovery cases for a company
* [redebit](docs/sdks/recoverycases/README.md#redebit) - Initiate a redebit for a recovery case

### [Reimbursements](docs/sdks/reimbursements/README.md)

* [getV1EmployeesEmployeeIdRecurringReimbursements](docs/sdks/reimbursements/README.md#getv1employeesemployeeidrecurringreimbursements) - Get recurring reimbursements for an employee
* [postV1EmployeesEmployeeIdRecurringReimbursements](docs/sdks/reimbursements/README.md#postv1employeesemployeeidrecurringreimbursements) - Create a recurring reimbursement
* [getV1RecurringReimbursements](docs/sdks/reimbursements/README.md#getv1recurringreimbursements) - Get a recurring reimbursement
* [putV1RecurringReimbursements](docs/sdks/reimbursements/README.md#putv1recurringreimbursements) - Update a recurring reimbursement
* [deleteV1RecurringReimbursements](docs/sdks/reimbursements/README.md#deletev1recurringreimbursements) - Delete a recurring reimbursement

### [Reports](docs/sdks/reports/README.md)

* [createCustom](docs/sdks/reports/README.md#createcustom) - Create a custom report
* [postPayrollsPayrollUuidReportsGeneralLedger](docs/sdks/reports/README.md#postpayrollspayrolluuidreportsgeneralledger) - Create a general ledger report
* [getReportsRequestUuid](docs/sdks/reports/README.md#getreportsrequestuuid) - Get a report
* [getTemplate](docs/sdks/reports/README.md#gettemplate) - Get a report template
* [postV1CompaniesCompanyIdReportsEmployeesAnnualFicaWage](docs/sdks/reports/README.md#postv1companiescompanyidreportsemployeesannualficawage) - Create an employees annual FICA wage report

### [SalaryEstimates](docs/sdks/salaryestimates/README.md)

* [postV1EmployeesEmployeeIdSalaryEstimates](docs/sdks/salaryestimates/README.md#postv1employeesemployeeidsalaryestimates) - Create a salary estimate for an employee
* [getV1SalaryEstimatesId](docs/sdks/salaryestimates/README.md#getv1salaryestimatesid) - Get a salary estimate
* [putV1SalaryEstimatesId](docs/sdks/salaryestimates/README.md#putv1salaryestimatesid) - Update a salary estimate
* [postV1SalaryEstimatesUuidAccept](docs/sdks/salaryestimates/README.md#postv1salaryestimatesuuidaccept) - Accept a salary estimate
* [getV1SalaryEstimatesOccupations](docs/sdks/salaryestimates/README.md#getv1salaryestimatesoccupations) - Search for BLS occupations

### [Signatories](docs/sdks/signatories/README.md)

* [list](docs/sdks/signatories/README.md#list) - Get the signatories for a company
* [create](docs/sdks/signatories/README.md#create) - Create a signatory
* [invite](docs/sdks/signatories/README.md#invite) - Invite a signatory
* [update](docs/sdks/signatories/README.md#update) - Update a signatory
* [delete](docs/sdks/signatories/README.md#delete) - Delete a signatory

### [TaxRequirements](docs/sdks/taxrequirements/README.md)

* [get](docs/sdks/taxrequirements/README.md#get) - Get tax requirements for a state
* [updateState](docs/sdks/taxrequirements/README.md#updatestate) - Update tax requirements for a state
* [getAll](docs/sdks/taxrequirements/README.md#getall) - Get all tax requirements for a company

### [TimeOffRequests](docs/sdks/timeoffrequests/README.md)

* [postV1CompaniesCompanyUuidTimeOffAdminApprovedRequests](docs/sdks/timeoffrequests/README.md#postv1companiescompanyuuidtimeoffadminapprovedrequests) - Create an admin-approved time off request
* [getV1CompaniesCompanyUuidTimeOffBalances](docs/sdks/timeoffrequests/README.md#getv1companiescompanyuuidtimeoffbalances) - Get time off balances for a company
* [getV1CompaniesCompanyUuidTimeOffRequests](docs/sdks/timeoffrequests/README.md#getv1companiescompanyuuidtimeoffrequests) - List time off requests for a company
* [postV1CompaniesCompanyUuidTimeOffRequests](docs/sdks/timeoffrequests/README.md#postv1companiescompanyuuidtimeoffrequests) - Create a time off request
* [postV1CompaniesCompanyUuidTimeOffRequestsPreview](docs/sdks/timeoffrequests/README.md#postv1companiescompanyuuidtimeoffrequestspreview) - Preview a time off request
* [getV1TimeOffRequestsTimeOffRequestUuid](docs/sdks/timeoffrequests/README.md#getv1timeoffrequeststimeoffrequestuuid) - Get a time off request
* [deleteV1TimeOffRequestsTimeOffRequestUuid](docs/sdks/timeoffrequests/README.md#deletev1timeoffrequeststimeoffrequestuuid) - Delete a time off request
* [putV1TimeOffRequestsTimeOffRequestUuidApprove](docs/sdks/timeoffrequests/README.md#putv1timeoffrequeststimeoffrequestuuidapprove) - Approve a time off request
* [putV1TimeOffRequestsTimeOffRequestUuidDecline](docs/sdks/timeoffrequests/README.md#putv1timeoffrequeststimeoffrequestuuiddecline) - Decline a time off request

### [TimeOffPolicies](docs/sdks/timeoffpolicies/README.md)

* [calculateAccruingTimeOffHours](docs/sdks/timeoffpolicies/README.md#calculateaccruingtimeoffhours) - Calculate accruing time off hours
* [get](docs/sdks/timeoffpolicies/README.md#get) - Get a time off policy
* [update](docs/sdks/timeoffpolicies/README.md#update) - Update a time off policy
* [getAll](docs/sdks/timeoffpolicies/README.md#getall) - Get all time off policies for a company
* [create](docs/sdks/timeoffpolicies/README.md#create) - Create a time off policy
* [addEmployees](docs/sdks/timeoffpolicies/README.md#addemployees) - Add employees to a time off policy
* [removeEmployees](docs/sdks/timeoffpolicies/README.md#removeemployees) - Remove employees from a time off policy
* [updateBalance](docs/sdks/timeoffpolicies/README.md#updatebalance) - Update employee time off balances
* [deactivate](docs/sdks/timeoffpolicies/README.md#deactivate) - Deactivate a time off policy

### [Webhooks](docs/sdks/webhooks/README.md)

* [listSubscriptions](docs/sdks/webhooks/README.md#listsubscriptions) - List webhook subscriptions
* [createSubscription](docs/sdks/webhooks/README.md#createsubscription) - Create a webhook subscription
* [getSubscription](docs/sdks/webhooks/README.md#getsubscription) - Get a webhook subscription
* [updateSubscription](docs/sdks/webhooks/README.md#updatesubscription) - Update a webhook subscription
* [deleteSubscription](docs/sdks/webhooks/README.md#deletesubscription) - Delete a webhook subscription
* [verify](docs/sdks/webhooks/README.md#verify) - Verify a webhook subscription
* [requestVerificationToken](docs/sdks/webhooks/README.md#requestverificationtoken) - Request a verification token for a webhook subscription
* [getV1WebhooksHealthCheck](docs/sdks/webhooks/README.md#getv1webhookshealthcheck) - Get the webhooks health status

### [WireInRequests](docs/sdks/wireinrequests/README.md)

* [get](docs/sdks/wireinrequests/README.md#get) - Get a single Wire In Request
* [submit](docs/sdks/wireinrequests/README.md#submit) - Submit a wire in request
* [list](docs/sdks/wireinrequests/README.md#list) - Get all Wire In Requests for a company

</details>
<!-- End Available Resources and Operations [operations] -->

<!-- Start Error Handling [errors] -->
## Error Handling

Handling errors in this SDK should largely match your expectations. All operations return a response object or raise an exception.


[`GustoEmbeddedException`](./src/main/java/models/errors/GustoEmbeddedException.java) is the base class for all HTTP error responses. It has the following properties:

| Method           | Type                        | Description                                                              |
| ---------------- | --------------------------- | ------------------------------------------------------------------------ |
| `message()`      | `String`                    | Error message                                                            |
| `code()`         | `int`                       | HTTP response status code eg `404`                                       |
| `headers`        | `Map<String, List<String>>` | HTTP response headers                                                    |
| `body()`         | `byte[]`                    | HTTP body as a byte array. Can be empty array if no body is returned.    |
| `bodyAsString()` | `String`                    | HTTP body as a UTF-8 string. Can be empty string if no body is returned. |
| `rawResponse()`  | `HttpResponse<?>`           | Raw HTTP response (body already read and not available for re-read)      |

### Example
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.components.*;
import com.gusto.embedded_api.models.errors.GustoEmbeddedException;
import com.gusto.embedded_api.models.errors.UnprocessableEntityError;
import com.gusto.embedded_api.models.operations.*;
import java.io.UncheckedIOException;
import java.lang.Exception;
import java.util.List;
import java.util.Optional;

public class Application {

    public static void main(String[] args) throws UnprocessableEntityError, Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
            .build();
        try {

            PostV1PartnerManagedCompaniesResponse res = sdk.companies().createPartnerManaged()
                    .security(PostV1PartnerManagedCompaniesSecurity.builder()
                        .systemAccessAuth(System.getenv().getOrDefault("SYSTEM_ACCESS_AUTH", ""))
                        .build())
                    .xGustoAPIVersion(PostV1PartnerManagedCompaniesHeaderXGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                    .partnerManagedCompanyCreateRequest(PartnerManagedCompanyCreateRequest.builder()
                        .user(User.builder()
                            .firstName("Frank")
                            .lastName("Ocean")
                            .email("frank@example.com")
                            .phone("2345558899")
                            .build())
                        .company(PartnerManagedCompanyCreateRequestCompany.builder()
                            .name("Frank's Ocean, LLC")
                            .tradeName("Frank’s Ocean")
                            .ein("123456789")
                            .contractorOnly(false)
                            .build())
                        .build())
                    .call();

            if (res.partnerManagedCompany().isPresent()) {
                System.out.println(res.partnerManagedCompany().get());
            }
        } catch (GustoEmbeddedException ex) { // all SDK exceptions inherit from GustoEmbeddedException

            // ex.ToString() provides a detailed error message including
            // HTTP status code, headers, and error payload (if any)
            System.out.println(ex);

            // Base exception fields
            var rawResponse = ex.rawResponse();
            var headers = ex.headers();
            var contentType = headers.first("Content-Type");
            int statusCode = ex.code();
            Optional<byte[]> responseBody = ex.body();

            // different error subclasses may be thrown 
            // depending on the service call
            if (ex instanceof UnprocessableEntityError) {
                var e = (UnprocessableEntityError) ex;
                // Check error data fields
                e.data().ifPresent(payload -> {
                      List<EntityErrorObject> errors = payload.errors();
                });
            }

            // An underlying cause may be provided. If the error payload 
            // cannot be deserialized then the deserialization exception 
            // will be set as the cause.
            if (ex.getCause() != null) {
                var cause = ex.getCause();
            }
        } catch (UncheckedIOException ex) {
            // handle IO error (connection, timeout, etc)
        }    }
}
```

### Error Classes
**Primary errors:**
* [`GustoEmbeddedException`](./src/main/java/models/errors/GustoEmbeddedException.java): The base class for HTTP error responses.
  * [`com.gusto.embedded_api.models.errors.NotFoundErrorObject`](./src/main/java/models/errors/com.gusto.embedded_api.models.errors.NotFoundErrorObject.java): Not Found     The requested resource does not exist. Make sure the provided ID/UUID is valid. *

<details><summary>Less common errors (10)</summary>

<br />

**Network errors:**
* `java.io.IOException` (always wrapped by `java.io.UncheckedIOException`). Commonly encountered subclasses of
`IOException` include `java.net.ConnectException`, `java.net.SocketTimeoutException`, `EOFException` (there are
many more subclasses in the JDK platform).

**Inherit from [`GustoEmbeddedException`](./src/main/java/models/errors/GustoEmbeddedException.java)**:
* [`com.gusto.embedded_api.models.errors.UnprocessableEntityError`](./src/main/java/models/errors/com.gusto.embedded_api.models.errors.UnprocessableEntityError.java): Unprocessable Entity    This may happen when the body of your request contains errors such as `invalid_attribute_value`, or the request fails due to an `invalid_operation`. See the [Errors Categories](https://docs.gusto.com/embedded-payroll/docs/error-categories) guide for more details. Applicable to 152 of 297 methods.*
* [`com.gusto.embedded_api.models.errors.ConflictErrorObject`](./src/main/java/models/errors/com.gusto.embedded_api.models.errors.ConflictErrorObject.java): Conflict    This error occurs when the resource version provided does not match the current version. Retrieve the latest version and retry. Status code `409`. Applicable to 2 of 297 methods.*
* [`com.gusto.embedded_api.models.errors.PeopleBatchConflictError`](./src/main/java/models/errors/com.gusto.embedded_api.models.errors.PeopleBatchConflictError.java): Error response when a people batch idempotency key conflict occurs. Status code `409`. Applicable to 1 of 297 methods.*
* [`com.gusto.embedded_api.models.errors.PayrollBlockersError`](./src/main/java/models/errors/com.gusto.embedded_api.models.errors.PayrollBlockersError.java): Payroll Blockers Error  For detailed information, see the [Payroll Blockers guide](https://docs.gusto.com/embedded-payroll/docs/payroll-blockers). Status code `422`. Applicable to 1 of 297 methods.*


</details>

\* Check [the method documentation](#available-resources-and-operations) to see if the error is applicable.
<!-- End Error Handling [errors] -->

<!-- Start Server Selection [server] -->
## Server Selection

### Select Server by Name

You can override the default server globally using the `.server(AvailableServers server)` builder method when initializing the SDK client instance. The selected server will then be used as the default on the operations that use it. This table lists the names associated with the available servers:

| Name   | Server                       | Description |
| ------ | ---------------------------- | ----------- |
| `demo` | `https://api.gusto-demo.com` | Demo        |
| `prod` | `https://api.gusto.com`      | Prod        |

#### Example

```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.operations.GetV1TokenInfoResponse;
import com.gusto.embedded_api.models.operations.XGustoAPIVersion;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .server(GustoEmbedded.AvailableServers.DEMO)
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1TokenInfoResponse res = sdk.introspection().getInfo()
                .xGustoAPIVersion(XGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.tokenInfo().isPresent()) {
            System.out.println(res.tokenInfo().get());
        }
    }
}
```

### Override Server URL Per-Client

The default server can also be overridden globally using the `.serverURL(String serverUrl)` builder method when initializing the SDK client instance. For example:
```java
package hello.world;

import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.models.operations.GetV1TokenInfoResponse;
import com.gusto.embedded_api.models.operations.XGustoAPIVersion;
import java.lang.Exception;

public class Application {

    public static void main(String[] args) throws Exception {

        GustoEmbedded sdk = GustoEmbedded.builder()
                .serverURL("https://api.gusto-demo.com")
                .companyAccessAuth(System.getenv().getOrDefault("COMPANY_ACCESS_AUTH", ""))
            .build();

        GetV1TokenInfoResponse res = sdk.introspection().getInfo()
                .xGustoAPIVersion(XGustoAPIVersion.TWO_THOUSAND_AND_TWENTY_FIVE_MINUS06_MINUS15)
                .call();

        if (res.tokenInfo().isPresent()) {
            System.out.println(res.tokenInfo().get());
        }
    }
}
```
<!-- End Server Selection [server] -->

<!-- Start Custom HTTP Client [http-client] -->
## Custom HTTP Client

The Java SDK makes API calls using an `HTTPClient` that wraps the native
[HttpClient](https://docs.oracle.com/en/java/javase/11/docs/api/java.net.http/java/net/http/HttpClient.html). This
client provides the ability to attach hooks around the request lifecycle that can be used to modify the request or handle
errors and response.

The `HTTPClient` interface allows you to either use the default `SpeakeasyHTTPClient` that comes with the SDK,
or provide your own custom implementation with customized configuration such as custom executors, SSL context,
connection pools, and other HTTP client settings.

The interface provides synchronous (`send`) methods and asynchronous (`sendAsync`) methods. The `sendAsync` method
is used to power the async SDK methods and returns a `CompletableFuture<HttpResponse<Blob>>` for non-blocking operations.

The following example shows how to add a custom header and handle errors:

```java
import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.utils.HTTPClient;
import com.gusto.embedded_api.utils.SpeakeasyHTTPClient;
import com.gusto.embedded_api.utils.Utils;

import java.io.IOException;
import java.net.URISyntaxException;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.io.InputStream;
import java.time.Duration;

public class Application {
    public static void main(String[] args) {
        // Create a custom HTTP client with hooks
        HTTPClient httpClient = new HTTPClient() {
            private final HTTPClient defaultClient = new SpeakeasyHTTPClient();
            
            @Override
            public HttpResponse<InputStream> send(HttpRequest request) throws IOException, URISyntaxException, InterruptedException {
                // Add custom header and timeout using Utils.copy()
                HttpRequest modifiedRequest = Utils.copy(request)
                    .header("x-custom-header", "custom value")
                    .timeout(Duration.ofSeconds(30))
                    .build();
                    
                try {
                    HttpResponse<InputStream> response = defaultClient.send(modifiedRequest);
                    // Log successful response
                    System.out.println("Request successful: " + response.statusCode());
                    return response;
                } catch (Exception error) {
                    // Log error
                    System.err.println("Request failed: " + error.getMessage());
                    throw error;
                }
            }
        };

        GustoEmbedded sdk = GustoEmbedded.builder()
            .client(httpClient)
            .build();
    }
}
```

<details>
<summary>Custom HTTP Client Configuration</summary>

You can also provide a completely custom HTTP client with your own configuration:

```java
import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.utils.HTTPClient;
import com.gusto.embedded_api.utils.Blob;
import com.gusto.embedded_api.utils.ResponseWithBody;

import java.io.IOException;
import java.net.URISyntaxException;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.io.InputStream;
import java.time.Duration;
import java.util.concurrent.Executors;
import java.util.concurrent.CompletableFuture;

public class Application {
    public static void main(String[] args) {
        // Custom HTTP client with custom configuration
        HTTPClient customHttpClient = new HTTPClient() {
            private final HttpClient client = HttpClient.newBuilder()
                .executor(Executors.newFixedThreadPool(10))
                .connectTimeout(Duration.ofSeconds(30))
                // .sslContext(customSslContext) // Add custom SSL context if needed
                .build();

            @Override
            public HttpResponse<InputStream> send(HttpRequest request) throws IOException, URISyntaxException, InterruptedException {
                return client.send(request, HttpResponse.BodyHandlers.ofInputStream());
            }

            @Override
            public CompletableFuture<HttpResponse<Blob>> sendAsync(HttpRequest request) {
                // Convert response to HttpResponse<Blob> for async operations
                return client.sendAsync(request, HttpResponse.BodyHandlers.ofPublisher())
                    .thenApply(resp -> new ResponseWithBody<>(resp, Blob::from));
            }
        };

        GustoEmbedded sdk = GustoEmbedded.builder()
            .client(customHttpClient)
            .build();
    }
}
```

</details>

You can also enable debug logging on the default `SpeakeasyHTTPClient`:

```java
import com.gusto.embedded_api.GustoEmbedded;
import com.gusto.embedded_api.utils.SpeakeasyHTTPClient;

public class Application {
    public static void main(String[] args) {
        SpeakeasyHTTPClient httpClient = new SpeakeasyHTTPClient();
        httpClient.enableDebugLogging(true);

        GustoEmbedded sdk = GustoEmbedded.builder()
            .client(httpClient)
            .build();
    }
}
```
<!-- End Custom HTTP Client [http-client] -->

<!-- Start Debugging [debug] -->
## Debugging

### Debug

You can setup your SDK to emit debug logs for SDK requests and responses.

For request and response logging (especially json bodies), call `enableHTTPDebugLogging(boolean)` on the SDK builder like so:

```java
SDK.builder()
    .enableHTTPDebugLogging(true)
    .build();
```
Example output:
```
Sending request: http://localhost:35123/bearer#global GET
Request headers: {Accept=[application/json], Authorization=[******], Client-Level-Header=[added by client], Idempotency-Key=[some-key], x-speakeasy-user-agent=[speakeasy-sdk/java 0.0.1 internal 0.1.0 org.openapis.openapi]}
Received response: (GET http://localhost:35123/bearer#global) 200
Response headers: {access-control-allow-credentials=[true], access-control-allow-origin=[*], connection=[keep-alive], content-length=[50], content-type=[application/json], date=[Wed, 09 Apr 2025 01:43:29 GMT], server=[gunicorn/19.9.0]}
Response body:
{
  "authenticated": true, 
  "token": "global"
}
```
__WARNING__: This logging should only be used for temporary debugging purposes. Leaving this option on in a production system could expose credentials/secrets in logs. <i>Authorization</i> headers are redacted by default and there is the ability to specify redacted header names via `SpeakeasyHTTPClient.setRedactedHeaders`.

__NOTE__: This is a convenience method that calls `HTTPClient.enableDebugLogging()`. The `SpeakeasyHTTPClient` honors this setting. If you are using a custom HTTP client, it is up to the custom client to honor this setting.


Another option is to set the System property `-Djdk.httpclient.HttpClient.log=all`. However, this second option does not log bodies.
<!-- End Debugging [debug] -->

<!-- Start Jackson Configuration [jackson] -->
## Jackson Configuration

The SDK ships with a pre-configured Jackson [`ObjectMapper`][jackson-databind] accessible via
`JSON.getMapper()`. It is set up with type modules, strict deserializers, and the feature flags
needed for full SDK compatibility (including ISO-8601 `OffsetDateTime` serialization):

```java
import com.gusto.embedded_api.utils.JSON;

String json = JSON.getMapper().writeValueAsString(response);
```

To compose with your own `ObjectMapper`, register the provided `GustoEmbeddedJacksonModule`, which
bundles all the same modules and feature flags as a single plug-and-play module:

```java
import com.gusto.embedded_api.utils.GustoEmbeddedJacksonModule;
import com.fasterxml.jackson.databind.ObjectMapper;

ObjectMapper myMapper = new ObjectMapper()
    .registerModule(new GustoEmbeddedJacksonModule());

String json = myMapper.writeValueAsString(response);
```

[jackson-databind]: https://github.com/FasterXML/jackson-databind
[jackson-jsr310]: https://github.com/FasterXML/jackson-modules-java8/tree/master/datetime
<!-- End Jackson Configuration [jackson] -->

<!-- Placeholder for Future Speakeasy SDK Sections -->

# Development

## Maturity

This SDK is in beta, and there may be breaking changes between versions without a major version update. Therefore, we recommend pinning usage
to a specific package version. This way, you can install the same version each time without breaking changes unless you are intentionally
looking for the latest version.

## Contributions

While we value open-source contributions to this SDK, this library is generated programmatically. Any manual changes added to internal files will be overwritten on the next generation. 
We look forward to hearing your feedback. Feel free to open a PR or an issue with a proof of concept and we'll do our best to include it in a future release. 

### SDK Created by [Speakeasy](https://www.speakeasy.com/?utm_source=openapi&utm_campaign=java)
