---
description: >-
  The below steps outline the test plan for creating a schema, and Credential
  definitions.
---

# Testing the Credential Management API

#### **Introduction** <a href="#introduction" id="introduction"></a>

The below steps outline the test plan for creating a schema, and Credential definitions.

#### **Test Objective** <a href="#test-objective" id="test-objective"></a>

* To ensure that schema is drafted and registered
* To validate that the cred def can be created and fetched
* Confirm all the API endpoints are working perfectly

#### **Pr-requisites** <a href="#pr-requisites" id="pr-requisites"></a>

* The NB Orbit Enterprise Issuer API has been downloaded to your system.
* POSTMAN has been installed on your system.

#### **Environment Setup in Postman** <a href="#environment-setup-in-postman" id="environment-setup-in-postman"></a>

1. **Create a Global Environment**:
   * Go to Environments on the top right corner of Postman.
   * Click on Add.
   * Name the environment (e.g., "credential API Environment").
   *   Add the following variables:

       * `baseUrl`: [https://testapi-credential.nborbit.ca/](https://testapi-issuer.nborbit.ca/)​
       * `apiKey`: GOrx\_-zseD3yN5MGKQLemhF4dawcX9\_f
       * `lobId`: 18545c09-c144-43f3-9239-146f3b083d88

       ​

#### Test Cases <a href="#test-cases" id="test-cases"></a>

### <mark style="color:blue;">Test Scenario 2:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test Draft Schema API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
  * Name the request "Draft Schema".
  * Set the request type to POST.
  * Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/schema/draft.



2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

**3 . Add Request Body**:: \
a. ANONCREDS

```json
 {
        "schemaInfo": {
          "schemaName": "Student_info",
          "schemaVersion": "3.0",
          "governanceUrl": "https://mining.ca.governance",
          "credentialFormat": "ANONCRED"
        },
        "attributes": 
          {
          "first_name": "text",
           "last_name": "text", 
           "dob": "text"
          },
​
        "isDraft": true
      },
      
```

**Detailed Breakdown**&#x20;

* **`schemaInfo`**: This object holds metadata about the schema itself.
  * **`schemaName`:** `"Student_info"`
    * This defines the name of the schema. It indicates the schema is used to issue credentials related to student information.
  * **`schemaVersion`:** `"3.0"`
    * Represents the version of the schema. Incrementing this helps track changes or improvements to the schema over time.
  * **`governanceUrl`:** `"https://mining.ca.governance"`
    * This is the URL that points to a governance framework or policy. It outlines the rules, standards, and procedures under which the schema is governed. In this case, it's hosted under a Canadian mining governance domain.
  * **`credentialFormat`:** `"ANONCRED"`
    * Specifies the format in which the credential will be issued. "ANONCRED" is short for **Anonymous Credentials**, which are privacy-preserving credentials typically used in systems like **Hyperledger Indy** and **Aries**, allowing selective disclosure and zero-knowledge proofs.
* **`attributes`**: This object defines the set of attributes that will be included in the credential issued using this schema.
  * **`first_name`:** `"text"`
    * The first name of the student, represented as a text string.
  * **`last_name`:** `"text"`
    * The last name or surname of the student.
  * **`dob`:** `"text"`
    * The date of birth of the student. Although stored as text, in practice, this might follow a specific date format (e.g., `YYYY-MM-DD`).
* **`isDraft`:** `true`
  * Indicates that the schema is still in the **draft state**. It has not been finalized or published for public/production use. This allows for further modifications before the schema is registered or used for issuing actual credentials.

b. JSON-LD

```json
{
        "schemaInfo": {
          "schemaName": "json_address_proof_new",
          "schemaVersion": "3.0",
          "governanceUrl": "https://mining.ca.governance",
          "credentialFormat": "JSON_LD"
      },
      "attributes": {
          "PersonalDetail": {
              "familyName": "text",
              "givenName": "text",
              "address": "AddressInfo"
          },
          "AddressInfo": {
              "streetAddress": "text",
              "postalAddress": "text"
          }
      },
      "isDraft": true
  }
```

Detailed Breakdown:&#x20;

* **`schemaInfo`**: Contains metadata that describes the schema.
  * **`schemaName`:** `"json_address_proof_new"`
    * This is the name of the schema. It suggests that the credential is intended to serve as proof of address in JSON format, and this is likely a newer version or variant.
  * **`schemaVersion`:** `"3.0"`
    * Indicates that this is version 3.0 of the schema, suggesting there were prior iterations or updates made to improve or extend the schema.
  * **`governanceUrl`:** `"https://mining.ca.governance"`
    * This URL points to the governance framework overseeing the schema. It establishes the policies, procedures, and trust mechanisms around schema usage, likely under a Canadian mining-related governance body.
  * **`credentialFormat`:** `"JSON_LD"`
    * Specifies that the credential follows the **JSON-LD (JavaScript Object Notation for Linked Data)** format. JSON-LD is a W3C standard that allows for semantic linking of data and is often used in verifiable credentials for interoperability, extensibility, and machine-readability.
* **`attributes`**: Defines the data fields (attributes) that will be part of the credential.
  * This schema uses a **nested structure** to organize related information under logical groupings, which is well-suited for the JSON-LD format.
  * **`PersonalDetail`**: A logical grouping that includes basic personal details of the individual:
    * **`familyName`:** `"text"`
      * Represents the surname or last name of the individual.
    * **`givenName`:** `"text"`
      * The first or given name of the individual.
    * **`address`:** `"AddressInfo"`
      * Instead of using a flat structure, this references another nested object (`AddressInfo`), enabling structured representation of address-related data.
  * **`AddressInfo`**: A nested object specifically for storing address-related details:
    * **`streetAddress`:** `"text"`
      * Represents the full street address (e.g., “123 Main Street”).
    * **`postalAddress`:** `"text"`
      * Could include ZIP/postal code, city, or additional address descriptors, depending on implementation.
* **`isDraft`:** `true`
  * Indicates the schema is still in **draft mode**, meaning it is under development or review. It has not yet been finalized for production use or publishing.

4. Send Request
5. expected result - status code should be 200

**Response Body**

{% code overflow="wrap" %}
```json
{"success":true,"message":"Schema draft created successfully!","data":{"schemaDraftId":27,"schemaState":"draft"}}
```
{% endcode %}

**Detailed Breakdown:**

* **`success`: `true`**
  * This Boolean flag confirms that the API request was successful.
  * It implies that no errors occurred during the schema draft creation process.
* **`message`: `"Schema draft created successfully!"`**
  * A descriptive message returned by the server, indicating the result in human-readable form.
  * It provides immediate feedback confirming that the draft creation was executed without issues.

***

**🔹 Data Object (`data`)**

This nested object holds the core result values returned by the API after processing:

* **`schemaDraftId`: `27`**
  * A unique identifier assigned to the newly created schema draft.
  * This ID is likely required for performing further actions such as publishing the schema, updating it, or deleting it later.
  * It serves as a reference or key for this specific draft in the system.
* **`schemaState`: `"draft"`**
  * Indicates the current status of the schema.
  * In this case, the schema is in a **draft** state, meaning it has been created but not yet finalized or published for use.
  * This allows for further edits, validations, or approvals before it transitions to an active or published state.





***

### <mark style="color:blue;">Test Scenario 2:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test Register Schema API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Register Schema".
* Set the request type to POST.
  * Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/schema/register.

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

3. **Add the Parameter Valure schemaId**
4. **Send Request**:

* Click Send.
* Verify the response with the status code must be 201 to ensure the credential offer is sent successfully.

**Expected Result**: The status code should be 200.

**Response Body**&#x20;

{% code overflow="wrap" %}
```json
{"success":true,"message":"Schema registered on ledger successfully.","data":{"schemaId":27,"schemaState":"available","schemaLedgerId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.6"}}
```
{% endcode %}

**Detailed Breakdown:**

* **`"success": true`**
  * Indicates the operation completed **successfully**, with no errors in processing the schema registration.

***

**🔹 Message**

* **`"message": "Schema registered on ledger successfully."`**
  * Confirms that the schema was **successfully recorded on the ledger**, making it immutable, transparent, and accessible to other agents or issuers/verifiers.

***

**🔹 Data Section**

* **`"schemaId": 27`**
  * Represents the **internal system ID** used to reference this schema within the platform or application's database.
* **`"schemaState": "available"`**
  * Shows the **current status** of the schema.
  * The state **"available"** means that it is now **ready to be used** for issuing credentials or for presentation by holders.
* **`"schemaLedgerId": "6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.6"`**
  * This is the **ledger-specific identifier** of the schema, broken down as follows:
    * `6YXT2jddYg1TZarJjbKGng`: The **DID (Decentralized Identifier)** of the schema issuer.
    * `2`: Refers to the object type **"Schema"** (in Hyperledger Aries, 2 represents a schema).
    * `Emp_cred_new`: The **schema name**.
    * `5.6`: The **schema version** that was registered on the ledger.\


### <mark style="color:blue;">Test Scenario 3:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test Get All Schema API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Get Schemas".
* Set the request type to GET.
* Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/schemas.

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

3. **Send Request**:

* Click Send.
* Verify the response with the status code must be 200

**Expected Result**: All the shcema should be displayed .

**Response Body**

{% code overflow="wrap" %}
```json
{"success":true,"message":"Schema fetched successfully!","data":{"items":[{"schemaId":27,"schemaName":"Emp_cred_new","schemaVersion":"5.6","attributes":["{\"attributeName\":\"full_name\",\"displayName\":\"Full name\",\"dataType\":\"text\",\"categoryId\":40,\"isRequired\":true,\"isRestricted\":true,\"isRestrictedBoolean\":true,\"restrictedValues\":[\"string\"],\"categoryName\":\"Name\",\"parentCategoryName\":\"\"}","{\"attributeName\":\"id\",\"displayName\":\"Emp ID\",\"dataType\":\"text\",\"categoryId\":41,\"isRequired\":true,\"isRestricted\":true,\"isRestrictedBoolean\":true,\"restrictedValues\":[\"string\"],\"categoryName\":\"ID\",\"parentCategoryName\":\"\"}"],"schemaLedgerId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.6","issuerDid":"6YXT2jddYg1TZarJjbKGng","governanceURL":"https://mining.ca.governance","credentialFormat":"ANONCRED","state":"available","primaryAttribute":"full_name","secondaryAttribute":"id","orgLogo":null,"backgroundImage":null,"backgroundImageSlice":null,"primaryBackgroundColor":"#11FC33","secondaryBackgroundColor":"#E3892A","endorsementState":null,"transactionId":null,"subjectType":null,"createEndorserTransaction":false},{"schemaId":26,"schemaName":"Test_jsonLd_context_schema","schemaVersion":"2.0","attributes":["{\"attributeName\":\"name\",\"displayName\":\"name\",\"dataType\":\"text\",\"categoryId\":37,\"isRequired\":true,\"isRestricted\":true,\"isRestrictedBoolean\":true,\"restrictedValues\":[\"string\"],\"categoryName\":\"ConformityAttestation\",\"parentCategoryName\":\"\"}","{\"attributeName\":\"assessorLevel\",\"displayName\":\"assessorLevel\",\"dataType\":\"text\",\"categoryId\":37,\"isRequired\":true,\"isRestricted\":true,\"isRestrictedBoolean\":true,\"restrictedValues\":[\"string\"],\"categoryName\":\"ConformityAttestation\",\"parentCategoryName\":\"\"}","{\"attributeName\":\"assessmentLevel\",\"displayName\":\"assessmentLevel\",\"dataType\":\"text\",\"categoryId\":37,\"isRequired\":true,\"isRestricted\":true,\"isRestrictedBoolean\":true,\"restrictedValues\":[\"string\"],\"categoryName\":\"ConformityAttestation\",\"parentCategoryName\":\"\"}","{\"attributeName\":\"issuedToParty\",\"displayName\":\"issuedToParty\",\"dataType\":\"object\",\"categoryId\":38,\"isRequired\":true,\"isRestricted\":true,\"isRestrictedBoolean\":true,\"restrictedValues\":[\"string\"],\"categoryName\":\"Party\",\"parentCategoryName\":\"ConformityAttestation\"}","{\"attributeName\":\"name\",\"displayName\":\"name\",\"dataType\":\"text\",\"categoryId\":38,\"isRequired\":true,\"isRestricted\":true,\"isRestrictedBoolean\":true,\"restrictedValues\":[\"string\"],\"categoryName\":\"Party\",\"parentCategoryName\":\"\"}","{\"attributeName\":\"registeredId\",\"displayName\":\"registeredId\",\"dataType\":\"text\",\"categoryId\":38,\"isRequired\":true,\"isRestricted\":true,\"isRestrictedBoolean\":true,\"restrictedValues\":[\"string\"],\"categoryName\":\"Party\",\"parentCategoryName\":\"\"}","{\"attributeName\":\"authorisation\",\"displayName\":\"authorisation\",\"dataType\":\"array\",\"categoryId\":39,\"isRequired\":true,\"isRestricted\":true,\"isRestrictedBoolean\":true,\"restrictedValues\":[\"string\"],\"categoryName\":\"Endorsement\",\"parentCategoryName\":\"ConformityAttestation\"}","{\"attributeName\":\"name\",\"displayName\":\"name\",\"dataType\":\"text\",\"categoryId\":39,\"isRequired\":true,\"isRestricted\":true,\"isRestrictedBoolean\":true,\"restrictedValues\":[\"string\"],\"categoryName\":\"Endorsement\",\"parentCategoryName\":\"\"}","{\"attributeName\":\"issuingAuthority\",\"displayName\":\"issuingAuthority\",\"dataType\":\"text\",\"categoryId\":39,\"isRequired\":true,\"isRestricted\":true,\"isRestrictedBoolean\":true,\"restrictedValues\":[\"string\"],\"categoryName\":\"Endorsement\",\"parentCategoryName\":\"\"}","{\"attributeName\":\"accreditationCertificate\",\"displayName\":\"accreditationCertificate\",\"dataType\":\"text\",\"categoryId\":39,\"isRequired\":true,\"isRestricted\":true,\"isRestrictedBoolean\":true,\"restrictedValues\":[\"string\"],\"categoryName\":\"Endorsement\",\"parentCategoryName\":\"\"}"],"schemaLedgerId":"https://context.nborbit.com/Test_jsonLd_context_schema.jsonld","issuerDid":"did:sov:6YXT2jddYg1TZarJjbKGng","governanceURL":"https://mining.ca.governance","credentialFormat":"JSON_LD","state":"available","primaryAttribute":"name","secondaryAttribute":"assessorLevel","orgLogo":null,"backgroundImage":null,"backgroundImageSlice":null,"primaryBackgroundColor":"#ACCAE8","secondaryBackgroundColor":"#6BF6D1","endorsementState":null,"transactionId":null,"subjectType":["ConformityAttestation","Party","Endorsement"],"createEndorserTransaction":false},{"schemaId":21,"schemaName":"Emp_cred_new","schemaVersion":"5.5","attributes":["{\"attributeName\":\"full_name\",\"displayName\":\"Full name\",\"dataType\":\"text\",\"categoryId\":32,\"isRequired\":true,\"isRestricted\":true,\"isRestrictedBoolean\":true,\"restrictedValues\":[\"string\"],\"categoryName\":\"Name\",\"parentCategoryName\":\"\"}","{\"attributeName\":\"id\",\"displayName\":\"Emp ID\",\"dataType\":\"text\",\"categoryId\":33,\"isRequired\":true,\"isRestricted\":true,\"isRestrictedBoolean\":true,\"restrictedValues\":[\"string\"],\"categoryName\":\"ID\",\"parentCategoryName\":\"\"}"],"schemaLedgerId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5","issuerDid":"6YXT2jddYg1TZarJjbKGng","governanceURL":"https://mining.ca.governance","credentialFormat":"ANONCRED","state":"available","primaryAttribute":"full_name","secondaryAttribute":"id","orgLogo":null,"backgroundImage":null,"backgroundImageSlice":null,"primaryBackgroundColor":"#213767","secondaryBackgroundColor":"#E55E4C","endorsementState":null,"transactionId":null,"subjectType":null,"createEndorserTransaction":false},{"schemaId":20,"schemaName":"test_bob_schema","schemaVersion":"1.0","attributes":["{\"attributeName\":\"full_name\",\"displayName\":\"Full name\",\"dataType\":\"text\",\"categoryId\":31,\"isRequired\":true,\"isRestricted\":true,\"isRestrictedBoolean\":true,\"restrictedValues\":[\"string\"],\"categoryName\":\"Category2\",\"parentCategoryName\":\"Category1\"}"],"schemaLedgerId":"6YXT2jddYg1TZarJjbKGng:2:test_bob_schema:1.0","issuerDid":"6YXT2jddYg1TZarJjbKGng","governanceURL":"https://mining.ca.governance","credentialFormat":"ANONCRED","state":"available","primaryAttribute":"full_name","secondaryAttribute":null,"orgLogo":null,"backgroundImage":null,"backgroundImageSlice":null,"primaryBackgroundColor":"#93E6D6","secondaryBackgroundColor":"#272B41","endorsementState":null,"transactionId":null,"subjectType":null,"createEndorserTransaction":false}],"meta":{"totalItems":4,"itemCount":4,"itemsPerPage":10,"totalPages":1,"currentPage":1}}}
```
{% endcode %}

**Detailed Breakdown:**

* The key `"success": true` confirms that the API call to fetch the schema data was successful.
* **Message**: The message `"Schema fetched successfully!"` provides human-readable confirmation of the operation’s success.
* **Data Object**: The `data` object contains two main parts — a list of `items` (schemas) and a `meta` object describing pagination details.

***

**Schemas (`items` list):**

**1. Schema ID 27 – `Emp_cred_new` (Version 5.6)**

* Uses the **ANONCRED** credential format.
* Contains two attributes: `full_name` and `id`, each required, restricted, and categorized (`Name` and `ID`).
* Assigned the ledger ID: `6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.6`
* Issued by DID: `6YXT2jddYg1TZarJjbKGng`
* Governed via: `https://mining.ca.governance`
* State: **Available** (indicates it’s live and usable).
* Design colors: Primary background `#11FC33`, Secondary `#E3892A`.
* No endorsement or UI branding (logos or images) specified.

**2. Schema ID 26 – `Test_jsonLd_context_schema` (Version 2.0)**

* Uses **JSON\_LD** as the credential format.
* Has **10 detailed attributes** including nested and categorized attributes like `issuedToParty`, `name`, and `authorisation`.
* Organized into three categories: `ConformityAttestation`, `Party`, and `Endorsement`.
* Ledger ID is a JSON-LD context URL: `https://context.nborbit.com/Test_jsonLd_context_schema.jsonld`
* DID format issuer ID: `did:sov:6YXT2jddYg1TZarJjbKGng`
* Color theme: Primary `#ACCAE8`, Secondary `#6BF6D1`
* Subject types defined explicitly for this schema.
* Still no endorsement transaction created.

**3. Schema ID 21 – `Emp_cred_new` (Version 5.5)**

* Also follows the **ANONCRED** format.
* Attributes are identical to Schema ID 27 but this is the **older version (5.5)**.
* Same issuer DID and governance URL.
* Ledger ID: `6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5`
* UI Colors: Primary `#213767`, Secondary `#E55E4C`

**4. Schema ID 20 – `test_bob_schema` (Version 1.0)**

* Simple schema with a single attribute: `full_name`.
* Categorized under `Category2` nested within `Category1`.
* Format: **ANONCRED**
* Ledger ID: `6YXT2jddYg1TZarJjbKGng:2:test_bob_schema:1.0`
* Color theme: Primary `#93E6D6`, Secondary `#272B41`

***

**Metadata Summary (`meta`):**

* `totalItems`: 4 – There are four schemas returned.
* `itemCount`: 4 – All items are part of the current page.
* `itemsPerPage`: 10 – Default page size set to 10.
* `totalPages`: 1 – Only one page exists in the response.
* `currentPage`: 1 – You're viewing the first and only page.



### <mark style="color:blue;">Test Scenario 4:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test Get Schema Details API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Get Schemas".
* Set the request type to GET.
* Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/schema/{schema\_id}.
* schema\_id =  27 in parameter

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

3. **Send Request**:

* Click Send.
* Verify the response with the status code must be 200

**Expected Result**: All the shcema should be displayed .

**Response Body**

```json
{
  "success": true,
  "message": "Schema retrieved successfully!",
  "data": {
    "schemaId": 27,
    "schemaName": "Driving_license",
    "schemaVersion": "1.0",
    "attributes": {
      "first_name": "text",
      "last_name": "text",
      "dob_dateint": "text"
    },
    "schemaLedgerId": "Ud5n8k3RnY8EkVHRfUyRri:2:Driving_license:1.0",
    "issuerDid": "Ud5n8k3RnY8EkVHRfUyRri",
    "governanceURL": null,
    "credentialFormat": "ANONCRED",
    "state": "draft",
    "endorsementState": null,
    "transactionId": null
  }
}
```

Detailed Breakdown :&#x20;

* **`success`:** `true`\
  Indicates that the API call was successful. This flag confirms that the requested schema data was retrieved without any errors.
* **`message`:** `"Schema retrieved successfully!"`\
  A human-readable confirmation message that the schema details were fetched from the system or ledger.
* **`data`:**\
  This main object holds the actual schema metadata and definition details, which include the following:
  * **`schemaId`:** `1`\
    A unique internal identifier for the schema in the local system or database. It may be used to reference this schema in other API operations.
  * **`schemaName`:** `"Driving_license"`\
    The name of the schema. In this case, it represents a schema designed for a **Driving License** credential.
  * **`schemaVersion`:** `"1.0"`\
    Indicates the version of the schema. Useful for tracking updates and managing backward compatibility.
  * **`attributes`:**\
    An object listing the names and data types (as `"text"`) of the schema's attributes:
    * `"first_name"` – The given name of the credential holder.
    * `"last_name"` – The family name or surname.
    * `"dob_dateint"` – Likely represents date of birth in **integer format**, typically used to ensure compatibility with legacy ledger constraints in AnonCreds.
  * **`schemaLedgerId`:** `"Ud5n8k3RnY8EkVHRfUyRri:2:Driving_license:1.0"`\
    This is the **fully qualified identifier** of the schema on the ledger. It follows the format:\
    `DID:2:schema_name:schema_version`, indicating it was written by issuer DID `Ud5n8k3RnY8EkVHRfUyRri`.
  * **`issuerDid`:** `"Ud5n8k3RnY8EkVHRfUyRri"`\
    The **Decentralized Identifier (DID)** of the issuer who created or owns the schema. This DID is essential for schema verification and trust.
  * **`governanceURL`:** `null`\
    Optional field, likely intended to link to governance documentation or policy for this schema, but currently not set.
  * **`credentialFormat`:** `"ANONCRED"`\
    Specifies the credential format associated with this schema. **AnonCreds** is a privacy-preserving credential format commonly used in Hyperledger Indy-based ecosystems.
  * **`state`:** `"draft"`\
    Indicates the **current lifecycle status** of the schema. "draft" implies it is not yet finalized or published for issuing credentials.
  * **`endorsementState`:** `null`\
    This field would typically indicate the **endorsement status** of the schema if endorsement workflows are involved (e.g., approval from a third party). It’s currently not set.
  * **`transactionId`:** `null`\
    Refers to the ledger transaction ID, which would be generated once the schema is written to the ledger. Since this is `null`, the schema hasn't been endorsed or committed yet.



### <mark style="color:blue;">Test Scenario 5:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test the API , Store External Schema to database.</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Get Schemas".
* Set the request type to POST.
* Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/schema/store.

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

3. Add Request Body

```json
{
  "schemaInfo": {
    "schemaLedgerId": "Ud5n8k3RnY8EkVHRfUyRri:2:Driving_license:1.0",
    "governanceUrl": "https://mining.ca.governance",
    "credentialFormat": "ANONCRED"
  }
}
```

**detailed Breakdown:**&#x20;

* **`schemaInfo`:**\
  This object encapsulates metadata about a specific schema used for credential issuance. It includes the following key fields:
  *   **`schemaLedgerId`:** `"Ud5n8k3RnY8EkVHRfUyRri:2:Driving_license:1.0"`\
      This is the **fully qualified identifier of the schema** on the ledger. It follows the format:

      ```
      rubyCopyEdit<issuerDid>:2:<schema_name>:<schema_version>
      ```

      In this case:

      * `Ud5n8k3RnY8EkVHRfUyRri` is the **issuer's DID**
      * `Driving_license` is the **name of the schema**
      * `1.0` is the **version of the schema**\
        The number `2` represents the object type (schema) in Hyperledger Indy.
  * **`governanceUrl`:** `"https://mining.ca.governance"`\
    This URL links to the **governance authority or policy documentation** that governs the schema. It defines the rules, compliance, and trust framework under which the schema is managed or accepted. This helps relying parties or verifiers validate the schema’s legitimacy.
  * **`credentialFormat`:** `"ANONCRED"`\
    Specifies the **format of credentials** that will be issued based on this schema.
    * `"ANONCRED"` refers to **Anonymous Credentials**, which enable selective disclosure and zero-knowledge proofs, preserving user privacy.\
      This format is typically used in Hyperledger Indy/Aries ecosystems.

4. **Send Request**:

* Click Send.
* Verify the response with the status code must be 201

**Expected Result**: All the shcema should be displayed .

**Response Body**

```json
{
  "success": true,
  "message": "Schema stored successfully!",
  "data": {
    "schemaId": 1,
    "schemaState": "available",
    "schemaLedgerId": "Ud5n8k3RnY8EkVHRfUyRri:2:Driving_license:1.0"
  }
}
```

**Detailed Breakdown:**&#x20;

* **`success`:** `true`\
  Indicates that the API operation completed successfully. In this context, it confirms that the schema has been stored without errors.
* **`message`:** `"Schema stored successfully!"`\
  A user-friendly message stating the result of the operation — the schema was saved or published, most likely to the ledger or internal schema registry.
* **`data`:**\
  Contains metadata about the stored schema, including:
  * **`schemaId`:** `1`\
    A unique internal identifier for the schema within the application or backend system. This ID can be used to reference this schema in subsequent API requests.
  * **`schemaState`:** `"available"`\
    Indicates the **current status or lifecycle state** of the schema.\
    `"available"` means the schema is now active and can be used for credential issuance (e.g., it's no longer in a "draft" or "pending" state).
  *   **`schemaLedgerId`:** `"Ud5n8k3RnY8EkVHRfUyRri:2:Driving_license:1.0"`\
      The **unique identifier of the schema on the ledger**.\
      It follows the Indy format:

      ```
      rubyCopyEdit<issuer_did>:2:<schema_name>:<schema_version>
      ```

      In this case:

      * Issuer DID: `Ud5n8k3RnY8EkVHRfUyRri`
      * Schema name: `Driving_license`
      * Schema version: `1.0`\
        This ID can be used by other agents or systems to reference and retrieve the schema from the ledger.



### <mark style="color:blue;">Test Scenario 6:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test Create Cred Def API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Create Cred Def".
* Set the request type to POST.
* Set the URL to `{{baseUrl}}` /api/lob/{lob\_id}/cred-def.

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

2. Request Body

```json

  "schemaId": 1,
  "tag": "Driving_License",
  "supportRevocation": false,
  "revocationRegistrySize": 100,
  "description": "Driving license issued by Northern Block"
}
```

Detailed Breakdown:&#x20;

* **`schemaId`:** `1`\
  This is the **unique identifier** of the schema within the local system or database. It is used to reference this specific schema when creating or managing credential definitions, issuing credentials, or querying metadata.
* **`tag`:** `"Driving_License"`\
  The **tag** is typically a human-readable label used to distinguish this credential definition or schema instance. It helps in identifying the purpose or type of credential quickly — in this case, it's related to a **Driving License**.
* **`supportRevocation`:** `false`\
  Indicates whether **revocation** is supported for credentials issued under this schema.
  * `false` means that once issued, the credentials **cannot be revoked**.
  * This is often a design decision based on the type of credential — for example, temporary access badges might need revocation, while permanent documents like licenses may not.
* **`revocationRegistrySize`:** `100`\
  Specifies the **maximum number of credentials** that can be supported in a **revocation registry**, if revocation were enabled.
  * Although `supportRevocation` is set to `false`, this field still defines the capacity that would be allocated if revocation were turned on.
  * A value of `100` means that up to 100 credentials could be managed in the revocation registry.
* **`description`:** `"Driving license issued by Northern Block"`\
  A brief **description** of the schema or credential definition.
  * It clarifies the issuer's identity ("Northern Block") and the credential type ("Driving license"), aiding in context and clarity when schemas are listed or displayed in UIs or logs.

1. **Send Request**:

* Click Send.
* Verify the response with 201.

**Response Body**

```json
{
  "success": true,
  "message": "credential definition created successfully.",
  "data": {
    "credentialDefinitionId": "Ud5n8k3RnY8EkVHRfUyRri:3:CL:896218:Driving_License",
    "credentialId": 1
  }
}
```

Detailed Breakdown :&#x20;

* **`success`:** `true`\
  Indicates that the operation was successful — in this case, a **credential definition was created** without any errors.
* **`message`:** `"credential definition created successfully."`\
  A human-readable confirmation message stating that the **credential definition** was registered or stored properly, likely on the ledger or within the issuer's system.
* **`data`:**\
  Contains the key identifiers related to the newly created credential definition:
  *   **`credentialDefinitionId`:** `"Ud5n8k3RnY8EkVHRfUyRri:3:CL:896218:Driving_License"`\
      This is the **fully qualified ID of the credential definition** on the ledger. The structure follows the **Hyperledger Indy** format:

      ```
      rubyCopyEdit<issuerDid>:3:CL:<schema_seq_no>:<tag>
      ```

      * `Ud5n8k3RnY8EkVHRfUyRri` → The **DID of the issuer**
      * `3` → Indicates a **credential definition** (object type)
      * `CL` → Stands for **CredDef linked to a schema**
      * `896218` → The **schema sequence number** on the ledger
      * `Driving_License` → The **tag** used to label or identify this specific credential definition\
        This ID is used whenever a credential is issued, referenced, or verified.
  * **`credentialId`:** `1`\
    This is the **internal identifier** for the credential definition within the issuer's local system or database. It can be used in API calls for managing or issuing credentials.





### <mark style="color:blue;">Test Scenario 7:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test</mark> <mark style="color:blue;"></mark><mark style="color:blue;">retrieve  all Cred Def   API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Retrieve All Cred Defs".
* Set the request type to GET.
* Set the URL to `{{baseUrl}}` /api/lob/{lob\_id}/cred-defs.

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

​​

3. **Send Request**:

* Click Send.
* Verify the response with 201 to ensure it displays all credential offers with details.

**Expected Result**: The response should display all the credential definitions​

**Response Body**&#x20;

{% code overflow="wrap" %}
```json
:"emplpye_details","displayName":"Test jsonld Cred","supportRevocation":true,"revocationRegistrySize":100,"description":"cred def for demo for test app with TR claim","issuerName":"did:sov:6YXT2jddYg1TZarJjbKGng","primaryAttribute":"full_name","secondaryAttribute":null,"orgLogo":null,"backgroundImage":null,"backgroundImageSlice":null,"primaryBackgroundColor":"#FFFFFF","secondaryBackgroundColor":"#d3553a","credentialId":24,"credDefnId":"6YXT2jddYg1TZarJjbKGng:3:CL:2776219:emplpye_details","credIssuerId":"did:sov:6YXT2jddYg1TZarJjbKGng"},{"schemaId":26,"tag":"json_ld","displayName":"Test jsonld Cred","supportRevocation":true,"revocationRegistrySize":100,"description":"cred def for demo for test app with TR claim","issuerName":"did:sov:6YXT2jddYg1TZarJjbKGng","primaryAttribute":"full_name","secondaryAttribute":null,"orgLogo":null,"backgroundImage":null,"backgroundImageSlice":null,"primaryBackgroundColor":"#FFFFFF","secondaryBackgroundColor":"#d3553a","credentialId":23,"credDefnId":"https://context.nborbit.com/Test_jsonLd_context_schema.jsonld","credIssuerId":"did:sov:6YXT2jddYg1TZarJjbKGng"},{"schemaId":25,"tag":"Person","displayName":"Person","supportRevocation":false,"revocationRegistrySize":100,"description":"BC Person Credentials","issuerName":"did:sov:6YXT2jddYg1TZarJjbKGng","primaryAttribute":"family_name","secondaryAttribute":"given_names","orgLogo":"https://nborbit.com/logo.png","backgroundImage":"https://nborbit.com/bg.png","backgroundImageSlice":"https://nborbit.com/bg-slice.png","primaryBackgroundColor":"#FFFFFF","secondaryBackgroundColor":"#FFFFFF","credentialId":22,"credDefnId":"6YXT2jddYg1TZarJjbKGng:3:CL:2758294:Person","credIssuerId":"did:sov:6YXT2jddYg1TZarJjbKGng"},{"schemaId":21,"tag":"emp_new_1_non_revo","displayName":"Test App Cred","supportRevocation":false,"revocationRegistrySize":100,"description":"cred def for demo for test app with TR claim","issuerName":"did:sov:6YXT2jddYg1TZarJjbKGng","primaryAttribute":"full_name","secondaryAttribute":null,"orgLogo":null,"backgroundImage":null,"backgroundImageSlice":null,"primaryBackgroundColor":"#FFFFFF","secondaryBackgroundColor":"#d3553a","credentialId":18,"credDefnId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo","credIssuerId":"did:sov:6YXT2jddYg1TZarJjbKGng"},{"schemaId":21,"tag":"emp_new_1_non_revokable","displayName":"Test App Cred","supportRevocation":true,"revocationRegistrySize":100,"description":"cred def for demo for test app with TR claim","issuerName":"did:sov:6YXT2jddYg1TZarJjbKGng","primaryAttribute":"full_name","secondaryAttribute":null,"orgLogo":null,"backgroundImage":null,"backgroundImageSlice":null,"primaryBackgroundColor":"#FFFFFF","secondaryBackgroundColor":"#d3553a","credentialId":17,"credDefnId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revokable","credIssuerId":"did:sov:6YXT2jddYg1TZarJjbKGng"},{"schemaId":21,"tag":"emp_new_1","displayName":"Test App Cred","supportRevocation":true,"revocationRegistrySize":100,"description":"cred def for demo for test app with TR claim","issuerName":"did:sov:6YXT2jddYg1TZarJjbKGng","primaryAttribute":"full_name","secondaryAttribute":null,"orgLogo":null,"backgroundImage":null,"backgroundImageSlice":null,"primaryBackgroundColor":"#FFFFFF","secondaryBackgroundColor":"#d3553a","credentialId":16,"credDefnId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1","credIssuerId":"did:sov:6YXT2jddYg1TZarJjbKGng"},{"schemaId":20,"tag":"test_bob_schema","displayName":"Driving License","supportRevocation":true,"revocationRegistrySize":1000,"description":"Driving license issued by Northern Block","issuerName":"did:sov:6YXT2jddYg1TZarJjbKGng","primaryAttribute":"full_name","secondaryAttribute":"2025","orgLogo":"https://nborbit.com/logo.png","backgroundImage":"https://nborbit.com/bg.png","backgroundImageSlice":"https://nborbit.com/bg-slice.png","primaryBackgroundColor":"#FFFFFF","secondaryBackgroundColor":"#FFFFFF","credentialId":15,"credDefnId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755398:test_bob_schema","credIssuerId":"did:sov:6YXT2jddYg1TZarJjbKGng"}],"meta":{"totalItems":7,"itemCount":7,"itemsPerPage":10,"totalPages":1,"currentPage":1}}}
```
{% endcode %}

**Detailed Breakdown**&#x20;

* &#x200B;**`tag`**
* A unique identifier or label assigned to the credential definition.
* Helps categorize or differentiate multiple definitions under the same schema.
* Example: `"emplpye_details"` or `"test_bob_schema"`.

**🔹 `displayName`**

* The user-friendly name of the credential as it appears in UI or wallet.
* Designed to be easily recognizable by users.
* Example: `"Test jsonld Cred"` or `"Driving License"`.

**🔹 `supportRevocation`**

* Boolean value indicating if the credential supports revocation.
* `true` means credentials can be revoked after issuance.
* Important for time-bound or conditional credentials.
* Example: `true` or `false`.

**🔹 `revocationRegistrySize`**

* Maximum number of credentials that can be issued before creating another revocation registry.
* Only relevant when `supportRevocation` is true.
* Example: `100` or `1000`.

**🔹 `description`**

* A brief description of the credential and its intended use or context.
* Often used in UI or admin portals to explain its purpose.
* Example: `"cred def for demo for test app with TR claim"`.

**🔹 `issuerName` / `credIssuerId`**

* The DID (Decentralized Identifier) of the entity issuing the credential.
* Represents the unique and verifiable identity of the issuer.
* Example: `"did:sov:6YXT2jddYg1TZarJjbKGng"`.

**🔹 `primaryAttribute`**

* The key attribute that is most prominently displayed.
* Often used as a summary or title for the credential card in a wallet.
* Example: `"full_name"` or `"family_name"`.

**🔹 `secondaryAttribute`**

* An optional secondary attribute shown with less emphasis.
* Can be used to display supporting information.
* Example: `"given_names"` or `null` if not provided.

**🔹 `orgLogo`**

* URL pointing to the organization’s logo image.
* Displayed in credential preview (like in digital wallets).
* Example: `"https://nborbit.com/logo.png"` or `null`.

**🔹 `backgroundImage`**

* URL for a background image displayed on the credential.
* Makes the credential visually distinctive.
* Example: `"https://nborbit.com/bg.png"` or `null`.

**🔹 `backgroundImageSlice`**

* Optional overlay or slice image to enhance the visual appearance.
* Used for creative UI purposes.
* Example: `"https://nborbit.com/bg-slice.png"` or `null`.

**🔹 `primaryBackgroundColor`**

* HEX color code for the primary background of the credential card.
* Used to style the UI presentation.
* Example: `"#FFFFFF"`.

**🔹 `secondaryBackgroundColor`**

* HEX color code for the secondary or accent background color.
* Typically used for borders or highlights.
* Example: `"#d3553a"`.

**🔹 `credentialId`**

* Internal identifier for the credential record in the issuer’s database.
* Not the same as the on-ledger definition ID.
* Example: `24`, `17`, etc.

**🔹 `credDefnId` (Credential Definition ID)**

* A unique identifier for the credential definition on the ledger.
* Contains issuer DID, schema sequence, and tag.
* For JSON-LD, it could be a URL instead of Sovrin format.
* Example:
  * Sovrin format: `6YXT2jddYg1TZarJjbKGng:3:CL:2758294:Person`
  * JSON-LD: `https://context.nborbit.com/Test_jsonLd_context_schema.jsonld`

**🔹 `schemaId`**

* Refers to the schema that defines the structure and attributes of the credential.
* This ID ties back to the schema created and stored on the ledger.
* Example: `21`, `26`, etc.





### <mark style="color:blue;">Test Scenario 8:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test the API retrieve  details of a Cred Def</mark>_ &#x20;

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Retrieve A Cred Defs" details.
* Set the request type to GET.
* Set the URL to `{{baseUrl}}` /api/lob/{lob\_id}/cred-defs/{credential\_id}.

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.
* Set the crdedntial\_id value -—  24

​​

3. **Send Request**:

* Click Send.
* Verify the response with 201 to ensure it displays all credential offers with details.

**Expected Result**: The response should display all the credential definitions​

**Response Body**&#x20;

```json
{
  "success": true,
  "message": "Credential definition fetched successfully!",
  "data": {
    "schemaId": 88,
    "tag": "47_attr_cred",
    "supportRevocation": false,
    "revocationRegistrySize": 100,
    "description": "cred def for demo for test app with TR claim",
    "credentialId": 24,
    "credentialDefinitionId": "PcfhoMwWpSzX5ogFSLQKDb:3:CL:2833449:47_attr_cred",
    "credIssuerId": "did:sov:PcfhoMwWpSzX5ogFSLQKDb"
  }
}
```

Detailed Breakdown:&#x20;

* **Success Flag**:\
  The `"success": true` field indicates that the API request was successful and the credential definition was fetched without any error.
* **Message**:\
  The `"message": "Credential definition fetched successfully!"` confirms the operation's result in human-readable form, reaffirming that the credential definition was retrieved.
* **Schema ID**:\
  `"schemaId": 88` identifies the schema to which this credential definition belongs. A schema defines the structure of the credential, including its name, version, and attributes.
* **Tag**:\
  The `"tag": "47_attr_cred"` serves as a unique label to distinguish this credential definition from others based on the same schema. Tags are especially useful when multiple credential definitions are created using the same schema but with different configurations (e.g., with/without revocation).
* **Revocation Support**:\
  `"supportRevocation": false` indicates that this credential definition does **not** support revocation. In practical terms, credentials issued from this definition cannot be revoked once issued.
* **Revocation Registry Size**:\
  `"revocationRegistrySize": 100` defines the capacity of the revocation registry if revocation were enabled. Despite revocation being disabled in this case, this field may still be included for consistency or future enablement.
* **Description**:\
  The field `"description": "cred def for demo for test app with TR claim"` provides human-readable context about the purpose of this credential definition. It seems to be intended for demonstration or testing purposes, possibly within a test application involving Trust Registry (TR) claims.
* **Credential ID**:\
  `"credentialId": 24` is likely an internal identifier used by the system to uniquely reference this particular credential definition within the platform or database.
* **Credential Definition ID**:\
  `"credentialDefinitionId": "PcfhoMwWpSzX5ogFSLQKDb:3:CL:2833449:47_attr_cred"` is the fully qualified identifier used on the ledger. It includes:
  * The **issuer DID** (`PcfhoMwWpSzX5ogFSLQKDb`)
  * The versioning and type information (`3:CL`)
  * The schema ledger sequence number (`2833449`)
  * The tag (`47_attr_cred`)
* **Credential Issuer DID**:\
  `"credIssuerId": "did:sov:PcfhoMwWpSzX5ogFSLQKDb"` refers to the decentralized identifier (DID) of the entity that issued this credential definition. It is registered on the Sovrin (or similar Hyperledger Indy-based) network.



### <mark style="color:blue;">Test Scenario 9:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test the API , store external   Cred Def  to Database</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Store external Cred Def".
* Set the request type to POST.
* Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/cred-def/store

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

2. Request Body

```
{
  "schemaId": 1,
  "credentialDefinitionId": "Ud5n8k3RnY8EkVHRfUyRri:3:CL:896218:Driving_License",
  "description": "Driving license issued by Northern Block"
}
```

Detailed Breakdown :&#x20;

* **Schema ID**:\
  `"schemaId": 1` identifies the schema associated with this credential. In decentralized identity systems, a schema defines the structure of a credential, such as its name, version, and the attributes it contains (e.g., name, DOB, license number).
* **Credential Definition ID**:\
  `"credentialDefinitionId": "Ud5n8k3RnY8EkVHRfUyRri:3:CL:896218:Driving_License"` is a unique, ledger-resolved identifier representing this specific credential definition. Here's a breakdown of its components:
  * `Ud5n8k3RnY8EkVHRfUyRri`: The DID (Decentralized Identifier) of the issuer who created this credential definition.
  * `3:CL`: Indicates the type and version; in this case, it's a **Credential Definition** (`CL`) using version `3`.
  * `896218`: The ledger sequence number (or ID) of the associated schema.
  * `Driving_License`: The tag used to identify and distinguish this credential definition—suggesting this definition is for a driving license.
* **Description**:\
  `"description": "Driving license issued by Northern Block"` provides a human-readable explanation of the credential definition. It clearly states that this credential definition is meant for issuing driving licenses and is associated with **Northern Block**, likely the credential issuer.

3. Click Send.

* Verify the response with 201.

**Response Body**

```json
{
  "success": true,
  "message": "Credential definition stored successfully.",
  "data": {
    "credentialDefinitionId": "Ud5n8k3RnY8EkVHRfUyRri:3:CL:896218:Driving_License",
    "credentialId": 1
  }
}
```

Detailed Breakdown:&#x20;

* **Success Flag**:\
  The field `"success": true` indicates that the API operation was executed successfully. In this context, it confirms that the credential definition has been successfully stored on the ledger or in the system.
* **Message**:\
  `"message": "Credential definition stored successfully."` provides a user-friendly confirmation that the credential definition was successfully saved or registered, possibly after being submitted by an issuer.
* **Credential Definition ID**:\
  `"credentialDefinitionId": "Ud5n8k3RnY8EkVHRfUyRri:3:CL:896218:Driving_License"` is the fully qualified ledger identifier of the stored credential definition. It includes:
  * The issuer’s **DID** (`Ud5n8k3RnY8EkVHRfUyRri`)
  * The marker `3:CL`, indicating that this is a **Credential Definition** for a schema (`CL`) using the versioning format used in Indy-style ledgers
  * The **schema sequence number** (`896218`), which maps to the associated schema
  * The **tag** (`Driving_License`), used to uniquely identify this credential definition among others tied to the same schema
* **Credential ID**:\
  `"credentialId": 1` is likely an internal system-generated identifier that uniquely identifies this credential definition in the application's backend database. It simplifies reference without requiring the full ledger ID.
