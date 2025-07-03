# Testing the Issuer API

### **Introduction**

The below steps outline the test plan for creating a schema, sending credential offers, and issuing credentials using API endpoints. In addition to the test plan, the details below also include steps for creating a schema, sending credential offers, issuing credentials, and verifying the expected results.

### **Test Objective**

* To ensure that credential offers can be sent to holders
* To validate that holders receive the credential offers from the issuer.]
* To confirm that credentials can be issued successfully

### **Pr-requisites**

* The NB Orbit Enterprise Issuer API has been downloaded to your system.
* POSTMAN has been installed on your system.

### **Environment Setup in Postman**

1. **Create a Global Environment**:
   * Go to Environments on the top right corner of Postman.
   * Click on Add.
   * Name the environment (e.g., "Issuer API Environment").
   *   Add the following variables:

       * `baseUrl`: [https://testapi-issuer.nborbit.ca/](https://testapi-issuer.nborbit.ca/)
       * `apiKey`: GOrx\_-zseD3yN5MGKQLemhF4dawcX9\_f
       * `lobId`: 18545c09-c144-43f3-9239-146f3b083d88



### Test Cases <a href="#test-cases" id="test-cases"></a>

### <mark style="color:blue;">Test Scenario 1:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  "Send OOB cred Offer" API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Send Out-of-Band Credential Offer".
* Set the request type to POST.
* Set the URL to `{{baseUrl}}/api/lob/{{lobId}}/send-oob-offer`.

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

3. **Add Request Body**:\
   A. ANONCREDS

```json
{
        "comment": "oob_anoncred",
        "credAttributes": {
            "familyName": "Verma",
            "givenName": "Amarjeet",
            "address": "patna"
          
        },
        "recipientEmail":"akvamar@getnada.com",
        "credAutoIssue": true,
        "credentialId": 56,
        "holderDid": "did:sov:ETkmK7bUbzcL5mxYasADBF",
​
        "credOfferId": "",
        "messageProtocol": "AIP2_0",
​
        "issuerDid": "did:sov:PcfhoMwWpSzX5ogFSLQKDb",
        "prevCredOfferId": ""
    },
```

**Detailed Breakdown** :

*
  * **`comment`:** `"oob_anoncred"`\
    This field is used to provide a comment or label for the credential issuance process. "oob" likely stands for "Out of Band," and "anoncred" refers to the **AnonCreds** credential format, which is privacy-preserving and widely used in SSI (Self-Sovereign Identity).
  * **`credAttributes`:**\
    This object holds the actual user data that will be included in the credential. It contains:
    * `"familyName": "Verma"` – the surname of the credential subject.
    * `"givenName": "Amarjeet"` – the first name or given name of the subject.
    * `"address": "patna"` – a simplified representation of the subject's address (could be expanded for more granularity).
  * **`recipientEmail`:** `"akvamar@getnada.com"`\
    The email address of the person who will receive the credential offer. This is typically used for notification or identification purposes in OOB flows.
  * **`credAutoIssue`:** `true`\
    This boolean flag indicates that the credential should be automatically issued upon acceptance, without requiring manual approval or additional steps by the issuer.
  * **`credentialId`:** `56`\
    This is a unique identifier (probably internal) used to reference the credential definition or schema template that this credential belongs to.
  * **`holderDid`:** `"did:sov:ETkmK7bUbzcL5mxYasADBF"`\
    This is the **Decentralized Identifier (DID)** of the holder (recipient) of the credential. It is based on the Sovrin ledger (`did:sov`), signifying that the holder is known and resolvable on that network.
  * **`credOfferId`:** `""`\
    This is an empty string, suggesting that no existing credential offer ID is associated yet. It may be generated later when the offer is created.
  * **`messageProtocol`:** `"AIP2_0"`\
    Refers to **Aries Interop Profile 2.0**, which is the communication protocol standard used for this interaction. It governs the message formats and flows between agents (issuer and holder).
  * **`issuerDid`:** `"did:sov:PcfhoMwWpSzX5ogFSLQKDb"`\
    This is the DID of the issuing party (agent). It identifies the issuer on the Sovrin network and is used to establish trust and validate the source of the credential.
  * **`prevCredOfferId`:** `""`\
    This is also an empty field, possibly indicating that there is no previous or related credential offer being referenced for this issuance. In some cases, this field might be used for re-issuance or linking to prior offers.\

* B. JSON-LD

```json
{
      "comment": "oob_json_ld",
      "credAttributes": {
        "PersonalDetail": {
           "familyName": "Verma",
           "givenName": "Amarjeet",
           "address": {
            "streetAddress": "Patna",
            "postalAddress": "2343546"
           } 
        }
      },
      "recipientEmail":"akvamar@getnada.com",
      "credAutoIssue": true,
      "messageProtocol": "AIP2_0",

      "credentialId": 56,
      "credOfferId": "",
      "issuerDid": "did:sov:TRHJGKDFgkhgrkjh",
      "prevCredOfferId": ""
    },
```

**Detailed BreakDown:** \


* **`comment`:** `"oob_json_ld"`\
  This indicates the type or purpose of the credential issuance. "oob" likely stands for **Out-of-Band**, and `"json_ld"` refers to the **JSON-LD credential format**, a standard used for Verifiable Credentials in W3C specifications. JSON-LD is typically used for semantic interoperability across systems.
* **`credAttributes`:**\
  This object holds the **structured credential data** to be issued. It contains one main attribute group:
  * **`PersonalDetail`:** A nested object containing personal information:
    * `"familyName": "Verma"` – The last name of the individual.
    * `"givenName": "Amarjeet"` – The first name of the individual.
    * `"address"` – An embedded object for address details:
      * `"streetAddress": "Patna"` – Represents the location or city.
      * `"postalAddress": "2343546"` – Likely a postal or zip code.\
        The hierarchical structure here is compatible with JSON-LD and helps in modeling complex data with semantic meaning.
* **`recipientEmail`:** `"akvamar@getnada.com"`\
  This is the email of the credential recipient, typically used for notification purposes or to identify the user during Out-of-Band interactions.
* **`credAutoIssue`:** `true`\
  Indicates that the credential should be issued automatically, without manual approval or intervention from the issuer side after the holder accepts the offer.
* **`messageProtocol`:** `"AIP2_0"`\
  Specifies the messaging protocol being used – **Aries Interop Profile 2.0**. This governs how agents communicate and ensures compatibility between different agent implementations.
* **`credentialId`:** `56`\
  Represents the ID of the credential schema or definition used for issuing this credential. This ID likely maps to metadata such as schema name, version, and supported formats.
* **`credOfferId`:** `""`\
  Currently empty, this field is meant to store the unique identifier for a credential offer, which will be generated once the credential issuance process starts.
* **`issuerDid`:** `"did:sov:TRHJGKDFgkhgrkjh"`\
  The **Decentralized Identifier (DID)** of the issuer, registered on the **Sovrin network**. This DID uniquely identifies the agent or organization issuing the credential.
* **`prevCredOfferId`:** `""`\
  Also empty, this field can be used to reference a **previous credential offer**, typically useful in re-issuance, updates, or in credential revocation/re-offering workflows.

***

**Expected Result**: The holder should receive an out-of-band offer.

**Response Body**

```
{
  "success": true,
  "message": "out-of-band offer send successfully.",
  "data": {
    "responseDetails": "Credential Offer successfully sent to newtest4@getnada.com"
  }
}
```

**Detailed Breakdown:**

* **success: true:** The `"success": true` field indicates that the operation was executed successfully without any errors or exceptions. This confirms that the request to send an out-of-band offer was processed correctly by the server.
* **message: "out-of-band offer send successfully.":** This message provides a clear confirmation to the user or client that the out-of-band offer has been sent successfully. It confirms that the action to send a credential offer out-of-band was completed without any issues.
* **Data Object:** The `data` object contains specific information about the result of the offer operation:
* **responseDetails: "Credential Offer successfully sent to** [**newtest4@getnada.com**](mailto:newtest4@getnada.com)**":** The `"responseDetails"` field provides a detailed confirmation message indicating that the credential offer was successfully sent to the email address `newtest4@getnada.com`. This gives additional context to the user, confirming that the offer has been dispatched to the intended recipient.

***

### <mark style="color:blue;">Test Scenario 2:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  "Prepare URL Offer" API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Prepare Url Offer".
* Set the request type to POST.
* Set the URL to `{{baseUrl}}/api/lob/{{lobId}}/prepare-url-offer`.

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

3. **Add Request Body**:\
   a. ANONCRED

```json
{
        "comment": "oob_anoncred",
        "credAttributes": {
            "familyName": "Verma",
            "givenName": "Amarjeet",
            "address": "patna"
          
        },
​
        "credAutoIssue": true,
        "credentialId": 56,
        "holderDid": "did:sov:ETkmK7bUbzcL5mxYasADBF",
​
        "credOfferId": "",
        "messageProtocol": "AIP2_0",
​
        "issuerDid": "did:sov:PcfhoMwWpSzX5ogFSLQKDb",
        "prevCredOfferId": ""
    },
```

**Detailed Breakdown**&#x20;

* **Comment (`"comment": "oob_json_ld"`):** This field acts as a label or identifier for the credential issuance request. `"oob_json_ld"` likely refers to an **Out-of-Band (OOB)** invitation method using **JSON-LD** credential format, which is commonly used for decentralized credentials.
* **Credential Attributes (`"credAttributes"`):** This object includes the actual data that will be embedded in the credential:
  * `"familyName": "Verma"` – The recipient's surname.
  * `"givenName": "Amarjeet"` – The recipient's first name.
  * `"address": "patna"` – The recipient's address. These attributes are typically defined in the schema that governs the credential's structure.
* **Automatic Credential Issuance (`"credAutoIssue": true`):** This boolean flag indicates that the credential should be issued automatically without requiring manual approval or acceptance steps by the issuer.
* **Credential ID (`"credentialId": 56`):** This is a unique identifier for the specific credential record or template in the issuer's system. It can be used to reference metadata or configuration for the credential.
* **Holder DID (`"holderDid": "did:sov:ETkmK7bUbzcL5mxYasADBF"`):** This is the **Decentralized Identifier (DID)** of the credential holder. It uniquely identifies the entity that will receive and own the credential.
* **Credential Offer ID (`"credOfferId": ""`):** This is currently an empty string, implying that a new credential offer is being initiated and no prior offer exists or is being referenced at this stage.
* **Message Protocol (`"messageProtocol": "AIP2_0"`):** Specifies that the issuance flow follows **Aries Interop Profile 2.0 (AIP 2.0)** standards, which dictate how agents communicate, especially for DIDComm V2 messaging.
* **Issuer DID (`"issuerDid": "did:sov:PcfhoMwWpSzX5ogFSLQKDb"`):** This is the **Decentralized Identifier** of the credential issuer. It represents the agent or organization that is issuing the credential.
* **Previous Credential Offer ID (`"prevCredOfferId": ""`):** Another optional field which is empty here. If present, it would refer to a prior credential offer, potentially to update, revoke, or replace an earlier issuance.

b. JSON-LD

```json
{
      "comment": "oob_json_ld",
      "credAttributes": {
        "PersonalDetail": {
           "familyName": "Verma",
           "givenName": "Amarjeet",
           "address": {
            "streetAddress": "Patna",
            "postalAddress": "2343546"
           } 
        }
      },
​
      "credAutoIssue": true,
      "messageProtocol": "AIP2_0",
​
      "credentialId": 56,
      "credOfferId": "",
      "issuerDid": "did:sov:TRHJGKDFgkhgrkjh",
      "prevCredOfferId": ""
    }
    
```

Detailed Breakdown :&#x20;

* **Comment (`"comment": "oob_json_ld"`):** This label describes the context or method of the credential issuance process. The term `"oob_json_ld"` indicates that this process is using an **Out-of-Band (OOB)** invitation flow and the **JSON-LD** (Linked Data) credential format, suitable for verifiable credentials under W3C standards.
* **Credential Attributes (`"credAttributes"`):** This section defines the actual **data being issued** in the credential. The attribute structure is nested, representing a more **complex schema**:
  * `"PersonalDetail"`: This is a **top-level attribute** grouping related subfields:
    * `"familyName": "Verma"` – The last name of the credential subject.
    * `"givenName": "Amarjeet"` – The first name of the credential subject.
    * `"address"`: A nested object with:
      * `"streetAddress": "Patna"` – The main address line.
      * `"postalAddress": "2343546"` – Likely a postal code or extended address field. This nested structure is typical for **JSON-LD-based credentials**, where complex data models are supported with linked relationships.
* **Credential Auto-Issue (`"credAutoIssue": true`):** A boolean flag that tells the issuer system to **automatically issue** the credential without manual intervention, assuming all other requirements are met.
* **Message Protocol (`"messageProtocol": "AIP2_0"`):** Specifies the communication standard to be followed. `"AIP2_0"` refers to **Aries Interop Profile 2.0**, which supports **DIDComm V2** messaging and JSON-LD credential exchanges among Aries-compatible agents.
* **Credential ID (`"credentialId": 56`):** An internal or system-wide identifier representing the credential template or type being issued. This ID may map to a credential definition or schema in the issuer's agent.
* **Credential Offer ID (`"credOfferId": ""`):** Currently empty, suggesting that this request is creating a **new credential offer** rather than continuing or responding to an existing one.
* **Issuer DID (`"issuerDid": "did:sov:TRHJGKDFgkhgrkjh"`):** This is the **Decentralized Identifier (DID)** of the **issuer agent**, uniquely identifying the organization or agent that will issue the credential.
* **Previous Credential Offer ID (`"prevCredOfferId": ""`):** Also left empty. If this were populated, it might point to a previous credential issuance attempt or offer, used for retries or updates.

4. **Send Request**:

* Click Send.
* Verify the response with 201 to ensure a URL is generated for the QR code.

**Expected Result**: A URL is generated for the credential offer.

**Response Body**&#x20;

```
{
  "success": true,
  "message": "prepare qr offer successfully.",
  "data": {
    "shortUrl": "https://testapi-issuer.nborbit.ca/url/796803f0-fda2-41ad-aff2-b8737b6e0fdc",
    "longUrl": "https://issuertestapp.test-eapi.nborbit.ca?oob=..."
  }
}
```

**Detailed Breakdown**

* `success`: A boolean field indicating the success of the operation.
  * **Value**: `true`\

* `message`: A string field providing a brief message about the operation.
  * **Value**: `"prepare qr offer successfully."`
* `data`: An object containing detailed information related to the QR offer. This is the main part of the response.

Inside the `data` Object:

* `shortUrl`: A shortened URL that can be used for quick access.
  * **Value**: `"`[`https://devapi-issuer.nborbit.ca/url/9a399865-74d8-457c-a846-74b77801b06b`](https://testapi-issuer.nborbit.ca/url/796803f0-fda2-41ad-aff2-b8737b6e0fdc)`"`
* `longUrl`: A longer, more detailed URL containing query parameters and other encoded data. This URL seems to be encoded with information required to perform the QR offer operation.

***

### <mark style="color:blue;">Test Scenario 3:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  "Send Cred Offer TO Contact" API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Send Credential Offer with Connection".
* Set the request type to POST.
  * Set the URL to `{{baseUrl}}/api/lob/{{lobId}}/send-offer`.

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

3. **Add Request Body**:

a. AnonCreds

```json
{
        "comment": "credential offer anoncred to holder trust org",
        "contactId": "d67e9262-2e89-48bb-a3b7-7e0e8e15a606",
        "credAttributes": {
            "first_name": "Verma",
            "last_name": "AmarjeetMay23",
            "dob": "19991010"
        },
        "credAutoIssue": false,
        "credentialId": 54,
        "credOfferId": "",
        "issuerDid": "did:sov:PcfhoMwWpSzX5ogFSLQKDb",
        "holderDid": "did:sov:6mToZR53GFrik3aaubKtTu",
        "validFrom": "2020-12-03T12:19:52Z",
        "validUntil": "2025-12-03T12:19:52Z",
        "prevCredOfferId": ""
    }
```



**Detailed Breakdown :**

* **`comment`**:
  * This field includes a descriptive note about the credential offer.
  * In this case, it indicates that the credential being offered is an **AnonCred** (Anonymous Credential) from the **issuer (trust organization)** to the **holder**.
* **`contactId`**:
  * A unique identifier that likely represents the relationship or connection record between the **issuer** and **holder**.
  * This UUID (`d67e9262-2e89-48bb-a3b7-7e0e8e15a606`) helps track the specific DIDComm connection used for issuing credentials.
* **`credAttributes`**:
  * Contains the actual **attribute values** to be included in the credential.
    * `first_name`: "Verma"
    * `last_name`: "AmarjeetMay23"
    * `dob`: "19991010" (Date of Birth, in `yyyyMMdd` format)
  * These values will be part of the issued credential under the specified schema.
* **`credAutoIssue`**:
  * A boolean flag (`false`) indicating whether the credential should be **automatically issued** once the offer is sent.
  * Setting this to false means the holder must **explicitly accept the offer** before the credential is issued.
* **`credentialId`**:
  * Indicates the **ID of the credential definition** or template being used to generate this credential.
  * Value `54` refers to a predefined credential structure stored in the issuer’s system.
* **`credOfferId`**:
  * Currently empty. This will typically be populated after the credential offer is created and sent.
  * It's used to **track the specific credential offer instance**.
* **`issuerDid`**:
  * The **Decentralized Identifier (DID)** of the credential issuer.
  * In this case, it's `"did:sov:PcfhoMwWpSzX5ogFSLQKDb"`, which points to a DID on a **Sovrin-based ledger**.
* **`holderDid`**:
  * The **DID of the credential holder**, i.e., the entity that will receive and store the credential.
  * `"did:sov:6mToZR53GFrik3aaubKtTu"` is also a Sovrin DID.
* **`validFrom`**:
  * The ISO 8601 timestamp indicating when the credential becomes **valid**.
  * `"2020-12-03T12:19:52Z"` means it’s valid from December 3, 2020, at 12:19:52 UTC.
* **`validUntil`**:
  * Specifies the **expiry date and time** for the credential.
  * `"2025-12-03T12:19:52Z"` means the credential will expire on December 3, 2025, at the same time.
* **`prevCredOfferId`**:
  * Left empty, which usually means this is a **new credential offer** and not a re-issuance or continuation of a previous offer.
  * This field could be used for version tracking or re-issuance workflows.

b. JSON-LD

```json
{
        "comment": "credential issuance nested of  cred to holder trust org",
        "contactId": "d67e9262-2e89-48bb-a3b7-7e0e8e15a606",
        "credAttributes": {
          "PersonalDetail": {
            "familyName": "Verma",
            "givenName": "Amarjeet",
            "address": {
              "streetAddress": "Patna",
              "postalAddress": "800010"
            } 
          }
        },
        "credAutoIssue": false,
        "credentialId": 56,
        "credOfferId": "",
        "issuerDid": "did:sov:PcfhoMwWpSzX5ogFSLQKDb",
        "holderDid": "did:sov:6mToZR53GFrik3aaubKtTu",
        "validFrom": "2020-12-03T12:19:52Z",
        "validUntil": "2025-12-03T12:19:52Z",
        "prevCredOfferId": ""
    }
    
```

**Detailed Breakdown:**&#x20;

* **`comment`**:
  * `"credential issuance nested of cred to holder trust org"`
  * Descriptive note indicating this is a **nested credential structure**, likely used for richer semantics or JSON-LD credential types.
  * Also highlights the trust org as the **issuer** and the other party as the **holder**.
* **`contactId`**:
  * `"d67e9262-2e89-48bb-a3b7-7e0e8e15a606"`
  * Represents a unique **connection ID** between issuer and holder (DIDComm connection).
* **`credAttributes`**:
  * Contains **nested attribute data** under the key `"PersonalDetail"`, which includes:
    * `familyName`: `"Verma"`
    * `givenName`: `"Amarjeet"`
    * `address`:
      * `streetAddress`: `"Patna"`
      * `postalAddress`: `"800010"`
  * This structure suggests support for **rich data modeling**, perhaps intended for interoperability with **Verifiable Credentials (VC)** or JSON-LD formats.
* **`credAutoIssue`**:
  * `false`
  * Indicates that **manual acceptance by the holder** is required before issuing the credential.
* **`credentialId`**:
  * `56`
  * Points to a predefined **credential template** or definition within the issuer’s registry/system.
* **`credOfferId`**:
  * `""` (empty string)
  * Will be filled after the credential offer is created. Used for **tracking and referencing** the offer instance.
* **`issuerDid`**:
  * `"did:sov:PcfhoMwWpSzX5ogFSLQKDb"`
  * DID of the **issuing organization** (trust org) on the **Sovrin ledger**.
* **`holderDid`**:
  * `"did:sov:6mToZR53GFrik3aaubKtTu"`
  * DID of the **credential holder** who will receive and store the credential.
* **`validFrom`**:
  * `"2020-12-03T12:19:52Z"`
  * Credential becomes **valid** starting from this timestamp.
* **`validUntil`**:
  * `"2025-12-03T12:19:52Z"`
  * Expiry of the credential validity window.
* **`prevCredOfferId`**:
  * `""`
  * Indicates this is a **new offer**, not a re-issuance or continuation of an existing one.

4. **Send Request**:

* Click Send.
* Verify the response with the status code must be 201 to ensure the credential offer is sent successfully.

**Expected Result**: The holder should receive a credential offer from the issuer.

**Response Body**&#x20;

```json
 {"success":true,"message":"Credential offer send successfully.","data":{"credOfferId":"fba5c211-de63-46c1-8cfe-3235b17383a3","credentialId":23,"credOfferStatus":"offer-sent"}}
```



**Detailed Breakdown:**

* `success`: A boolean field indicating whether the operation was successful.
  * **Value**: `true`
* `message`: A string field providing a brief message about the result of the operation.
  * **Value**: `"Credential offer send successfully."`
* `data`: An object that contains detailed information about the credential offer. This is the core part of the response.

Inside the `data` Object:

* `credOfferId`: A numeric field representing a unique identifier for the credential offer.
  * **Value**: `18`
  * `Credential Status : "Offer-sent"`

***

### <mark style="color:blue;">Test Scenario 4:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  "Issue Credential " API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Issue Credential".
* Set the request type to POST.
* Set the URL to `{{baseUrl}}/api/lob/{{lobId}}/issue-credential`.

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

3. **Send Request**:

* Click Send.
* Verify the response with the status code must be 201 to ensure the credential is issued successfully.

**Expected Result**: The holder should receive the issued credential.

**Response Body**

```json
{"success":true,"message":"Credential issued successfully.","data":{"credOfferId":"fba5c211-de63-46c1-8cfe-3235b17383a3","credOfferStatus":"credential-issued"}}
```



**Detailed Breakdown:**

* `success`: A boolean indicating whether the request was successful.
  * **Value**: `true`
* `message`: A string providing a brief description of the outcome of the request.
  * **Value**: `"Credential issued successfully."`
* `data`: An object that contains additional details about the issued credential.

Inside the `data` Object:

* `credOfferId`: A string providing more context or confirmation about the issuance of the credential.
  * credOfferStatus:"credential-issued" `"Credential has been issued successfully."`



***

### <mark style="color:blue;">Test Scenario 5:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  "Retrieve Credential Offer" API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Retrieve Credential Offer".
* Set the request type to GET.
* Set the URL to `{{baseUrl}}` api/lob/{lob\_id}/offers.

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

3. **Send Request**:

* Click Send.
* Verify the response with 200 to ensure it displays all credential offers with details.

**Expected Result**: The response should display all credential offers with details.

**Response Body**&#x20;

```json
{"success":true,"message":"credential record fetch successfully.","data":{"meta":{"totalItems":61,"itemCount":10,"itemsPerPage":10,"totalPages":7,"currentPage":1},"items":[{"credentialStatus":"offer-sent","credFormat":"ANONCREDS","issuanceDate":"2025-04-15","expirationDate":null,"credOfferId":"bdaf844f-61cd-422d-aeb9-ec66188284fd","credentialId":16,"credAutoIssue":true,"credPreview":{"attributes":[{"name":"full_name","value":"amarjeet"},{"name":"id","value":"1061"}]}},{"credentialStatus":"credential-issued","credFormat":"JSONLD","issuanceDate":"2025-04-15","expirationDate":null,"credOfferId":"fba5c211-de63-46c1-8cfe-3235b17383a3","credentialId":23,"credAutoIssue":false,"credPreview":{"id":"did:sov:3uvkkhAoXaMjbN9SZumFHv"}},{"credentialStatus":"offer-sent","credFormat":"ANONCREDS","issuanceDate":"2025-04-15","expirationDate":null,"credOfferId":"d9caaec9-9de2-4893-a74e-028d588db9d0","credentialId":16,"credAutoIssue":true,"credPreview":{"attributes":[{"name":"full_name","value":"amarjeet"},{"name":"id","value":"1061"}]}},{"credentialStatus":"offer-sent","credFormat":"ANONCREDS","issuanceDate":"2025-04-15","expirationDate":null,"credOfferId":"b66c0dc5-153c-4199-ae8a-ebac66911d67","credentialId":16,"credAutoIssue":false,"credPreview":{"attributes":[{"name":"full_name","value":"amarjeet"},{"name":"id","value":"1061"}]}},{"credentialStatus":"offer-sent","credFormat":"ANONCREDS","issuanceDate":"2025-04-15","expirationDate":null,"credOfferId":"624ddd77-5eae-46fa-a616-5d0bbabf0b14","credentialId":16,"credAutoIssue":false,"credPreview":{"attributes":[{"name":"full_name","value":"amarjeet"},{"name":"id","value":"1061"}]}},{"credentialStatus":"offer-sent","credFormat":"JSONLD","issuanceDate":"2025-04-10","expirationDate":null,"credOfferId":"b54df616-5c27-4ec5-aaf2-f838d2976907","credentialId":23,"credAutoIssue":false,"credPreview":{"id":"did:sov:3uvkkhAoXaMjbN9SZumFHv"}},{"credentialStatus":"offer-sent","credFormat":"JSONLD","issuanceDate":"2025-04-10","expirationDate":null,"credOfferId":"75503dde-88e1-4f48-ba4d-f5f16af87292","credentialId":23,"credAutoIssue":true,"credPreview":{"id":"did:sov:3uvkkhAoXaMjbN9SZumFHv"}},{"credentialStatus":"offer-sent","credFormat":"JSONLD","issuanceDate":"2025-04-10","expirationDate":null,"credOfferId":"4ac60961-30c1-45a8-aa8f-34c4506074c7","credentialId":23,"credAutoIssue":false,"credPreview":{"id":"did:sov:3uvkkhAoXaMjbN9SZumFHv"}},{"credentialStatus":"offer-sent","credFormat":"JSONLD","issuanceDate":"2025-04-09","expirationDate":null,"credOfferId":"4ed091f7-5108-4f76-ab77-d34c6942c068","credentialId":23,"credAutoIssue":false,"credPreview":{"id":"did:sov:3uvkkhAoXaMjbN9SZumFHv"}},{"credentialStatus":"offer-sent","credFormat":"JSONLD","issuanceDate":"2025-04-09","expirationDate":null,"credOfferId":"e20ebb5a-51a3-4f7b-a183-6fe4b6e1577e","credentialId":23,"credAutoIssue":false,"credPreview":{"id":"did:sov:3uvkkhAoXaMjbN9SZumFHv"}}]}}
```



**Detailed Breakdown:**

*   `success`: A boolean indicating whether the request was successful.



    * **`success`**:
      * Type: `boolean`
      * **Value**: `true`
      * Indicates the API request was successful.
    * **`message`**:
      * Type: `string`
      * **Value**: `"credential record fetch successfully."`
      * A message from the API summarizing the result.
    * **`data`**:
      * Type: `object`
      * Contains metadata and credential record details.

    **🔹 `data.meta` Object**

    Metadata for pagination:

    * **`totalItems`**: `61`\
      Total number of credential records available.
    * **`itemCount`**: `10`\
      Number of records returned in the current response (this page).
    * **`itemsPerPage`**: `10`\
      How many records are returned per page.
    * **`totalPages`**: `7`\
      Total number of pages available.
    * **`currentPage`**: `1`\
      The current page number being viewed.

    **🔹 `data.items` Array**

    An array of **credential record objects**. Each item contains:\


    #### **Fields in Each Credential Record**

    * **`credentialStatus`**:
      * Type: `string`
      * Example: `"offer-sent"`
      * Current status of the credential (e.g., offer-sent, credential-issued).
    * **`credFormat`**:
      * Type: `string`
      * Example: `"ANONCREDS"` or `"JSONLD"`
      * Credential format used (e.g., Anoncreds, JSON-LD).
    * **`issuanceDate`**:
      * Type: `string` (format: `YYYY-MM-DD`)
      * Example: `"2025-04-15"`
      * Date the credential was issued.
    * **`expirationDate`**:
      * Type: `string` or `null`
      * Example: `null`
      * Expiration date if set; `null` means no expiration.
    * **`credOfferId`**:
      * Type: `string`
      * Example: `"bdaf844f-61cd-422d-aeb9-ec66188284fd"`
      * Unique identifier for the credential offer.
    * **`credentialId`**:
      * Type: `integer`
      * Example: `16`
      * Unique ID for the credential.
    * **`credAutoIssue`**:
      * Type: `boolean`
      * Example: `true`
      * Indicates whether the credential will be issued automatically.
    * **`credPreview`**:
      * Type: `object`
      * Format varies:
        1. For **ANONCREDS**: Contains an `attributes` array of key-value pairs.
        2. For **JSONLD**: Contains an `id` field, often a `did:` string.

### <mark style="color:blue;">Test Scenario 6:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  "Revoke Credential" API</mark>_&#x20;

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Retrieve Credential Offer".
* Set the request type to POST.
* Set the URL to `{{baseUrl}}` api/lob/{lob\_id}/revoke-credential.

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

3. **Add Request Body**:\
   credOfferId = cfe8aa01-74d4-43ca-8e54-77719e963dbd

```json
{
        "comment": "revoking cred as i dont trust the holder",
        "credOfferId": cfe8aa01-74d4-43ca-8e54-77719e963dbd,
        "notify": False
    }
```



3. **Send Request**:

* Click Send.
* Verify the response with 201 to ensure it displays all credential offers with details.

**Expected Result**: The response should display the credential details which has been revoked..



**Detailed Breakdown of the Request Body above**

**comment**

A descriptive note explaining the reason or context for revoking the credential.\
**Example**: `"revoking cred as i dont trust the holder"`\
**Explanation**:\
This field is useful for logging or auditing purposes. It helps track why a credential was revoked and can be shown in the UI or stored in system logs for future reference. In this example, it explicitly states a trust issue with the holder as the reason for revocation.

#### **credOfferId**

A unique identifier referring to the specific credential offer or issuance instance that is to be revoked.\
**Example**: `credOfferId` (placeholder for actual ID like `"a1b2c3d4-5678-90ab-cdef-1234567890gh"`)\
**Explanation**:\
This tells the revocation endpoint exactly which credential is being targeted. The ID connects to a record in the issuer's system that maps to the credential exchange or issuance.

**notify**

A boolean value indicating whether the holder (or relevant party) should be notified about the revocation.\
**Example**: `False`\
**Explanation**:

* `True`: The system will attempt to notify the holder (e.g., via message, webhook, or credential update).
* `False`: The system will revoke the credential silently, without informing the holder.

In this example, `False` implies the revocation is done quietly, possibly because of security or trust concerns.

#### Response Body&#x20;

```
{"success":true,"message":"Credential revoked successfully.","data":{"responseDetails":"Credential has been revoked successfully.","revokedDateTime":"2025-04-15T15:42:19.254Z"}}// Some code
```

#### **Detailed Breakdown of Revocation Response**

* **`success`**:\
  Indicates whether the API operation was completed successfully.
  * Value: `true`
  * This means the revocation request was processed without errors, confirming a successful execution.
* **`message`**:\
  A high-level summary or status message returned by the server.
  * Value: `"Credential revoked successfully."`
  * This acts as a quick confirmation for clients or front-end applications to understand that the revocation process was completed.
* **`data`**:\
  Contains specific details about the revocation outcome.
  * **`responseDetails`**:\
    A human-readable message that provides more context or confirmation about the revocation.
    * Value: `"Credential has been revoked successfully."`
    * Reinforces the status by giving a more descriptive acknowledgment of the revocation event.
  * **`revokedDateTime`**:\
    The exact date and time when the credential was revoked, in ISO 8601 format.
    * Value: `"2025-04-15T15:42:19.254Z"`
    * This timestamp is important for logging, auditing, and any systems that track credential lifecycle events. The `Z` indicates UTC time.

### <mark style="color:blue;">Test Scenario 7:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  "Retrieve Credential Offer using Id" API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Retrieve Credential Offer".
* Set the request type to GET.
* Set the URL to `{{baseUrl}}` api/lob/{lob\_id}/offers/{cred\_offer\_id}
* cred\_offer\_id = cfe8aa01-74d4-43ca-8e54-77719e963dbd

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

3. **Send Request**:

* Click Send.
* Verify the response with 200 to ensure it displays all credential offers with details.

**Expected Result**: The response should display the detail of  credential issued.

**Response Body**&#x20;

```json
{"success":true,"message":"Credential status retrieved successfully.","data":{"id":844,"credentialStatus":"credential-issued","credentialExchangeId":"6bda236d-3580-4e65-b889-b826377a7fc2","issuerDid":"6YXT2jddYg1TZarJjbKGng","issuanceDate":"2025-04-15","expirationDate":null,"credDefId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1","schemaLedgerId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5","credOffer":{"@id":"0456b36b-5c52-4f62-87dd-8c27b30a2fd0","@type":"https://didcomm.org/issue-credential/2.0/offer-credential","comment":"Emp id issance","formats":[{"format":"hlindy/cred-abstract@v2.0","attach_id":"indy"}],"~thread":{},"offers~attach":[{"@id":"indy","data":{"base64":"eyJzY2hlbWFfaWQiOiAiNllYVDJqZGRZZzFUWmFySmpiS0duZzoyOkVtcF9jcmVkX25ldzo1LjUiLCAiY3JlZF9kZWZfaWQiOiAiNllYVDJqZGRZZzFUWmFySmpiS0duZzozOkNMOjI3NTU0MDg6ZW1wX25ld18xIiwgImtleV9jb3JyZWN0bmVzc19wcm9vZiI6IHsiYyI6ICI3MjQ0MjI5ODk3OTUzMjA2ODc3MjQwMDA1MjYzMjM5MTI5NDgzMjkzOTY3MDI3NDQyNTIzMzg2MTQzNzE0NjAxODIyMTc1OTU3NTE0MiIsICJ4el9jYXAiOiAiODUzNTc1MjkxMDgzNTgxOTExODA2MTk5MjM3NTA4ODc0MDA1OTM0MTA3MjQ4NjYwMDA2OTMzMjA3NTA3MjA4OTI5NTYxOTYwMzc2MzMwODE1NjI0MzY3NjYxNDc0MjU3MzA3NTM5ODY0ODY1NTc4Nzg1OTMwMzM4MDkyODY3NzY0NTMzNTI3NDQ1OTM4ODMxMTEyNzg5NTYxNjk0MDkxODEwNjE4MzY1Mjk3MDE1NDYwNTcxMTA4NTA3ODgzOTA0MjI3MDgwNTk3OTg0MDY2NDkxMjExODc2NDQ0NjQ3NTA5MzYwNjgxNjgwMzAxOTAxMDYwNDAyMTEwMDU4MjE2NTA5MzY3NDUwODE4NDA2MTYyNjkzMTU3Mjg4NTAwODU5ODI0NTE0OTE3MzM5MzA1OTU5NzU1MzU1Mzc2NTM4NzMyMjUxMDAzMTEyOTEwNjgwNTY4ODgxOTcxODU3MzQxNDYyMDIxMjkyOTEzMjkyMTk2ODUxNDAyNzc4MzE0NzQwMTA3MzA3OTI3NjYzMjc5NjMxMTgxNDkzNDQxNjI4MDk3OTgwMzM5MjE5NTA5MDgwMjYzNDc1MDc4Mzk3OTMxODYxOTczODU1NjQ5NjMwNTcxMzU1NTcxNTg2MjMzNDYwNDY0MTExOTE2OTkxMDcxMDE4MTA2OTgwMzAzNDgxMzI2NjQxODM3MTM5NDU3NzQyNTg4NzczNDk5OTA3MjM5Mjg2MTcwNjU1OTc2Mzc1MDQ2Mzk3NTE1MzE2MjgyMDE2MDgyOTI0NDA4NDMzMjU5ODg0MzY0ODk4NDY0NzQ3OTY3MjM2ODY0MTg1ODQ1MTU3MzUxNzY0NTA5NTM4MDUzNTA0OTI2MDk0MjYzMDQ3MjA5NDAwMDc1NDQ2MDI4NDI4NTk3OTQyOTI2NzMzNjYxODUyNzQwIiwgInhyX2NhcCI6IFtbImlkIiwgIjU2OTA1MzY0NzE5MjY5NDMxNTY4NjE1MzMyNDk2NDI5NzgwMjk1MTQ4MjIxNDkzNDUyNzQ2MDA1MzU2NzExNTUyNTY5Mzc0NzA2Mzg2MzcxMDgxODY3NTA0NDI0MTQ4MzA3MDI3MTc4NDk0ODA0MTA3ODY0NTQ0NTYzOTEyMjc5Mjg3MjQ2MjA0MDY4MTEyNzY3MzY0MTI0MzQ4OTMwNzQ0NzUwOTU5NTI4MzgxNzk2NjE5NTI5NTM1NTY4NTQ5NDEzNjU2NjYzMDE5OTY4MzE3NDI4MTIwNDM0NjIwMTAyMzUwMTQzMTMyNTY3NTI5NzY4MDE5MDc2MzEzNTc0ODE1NzA0MTc3Njc5NTg2NTQ5ODkxNjQwNDE3NzM0Mjc0MTQzNTQwNjUzOTkxMDM1NTY1MzMzNjcyOTk0MzUxNTAxODQ4Nzc5NTI0NDYzMzUxNTkxMzU4NTcxODIwNDM2NjE2NzM3MTc1OTk4ODU1NzY2Mjc0NTE1MDQyNjkyMTY1MDYzNDI2NTI0MTExOTI0NzkzNDExMDY0MzI1NzkzNDA0ODQ0MTY1NTc2OTY4NzQwMzE4NTc4NjQ0MzUzMTE5NjIxNDM3NTE1MDM5MTQ1Nzc1MjQzNzYxMjExMjE2MTIyMTA3NTU5MzUwMDM3NDc2MTIwODU3OTU4MjMzNTcwMjM4NDQ1NTk5NzIxNDMyMTM2Mzk0MDQxNTE0Mjg0MjE0NjI3MDQ4MzExMzYxOTA5NTQwMzU4NDYyODU2OTM3NDEyMjIxNzk0OTEwMjE0Nzk3MDczNzcyMTI5MTQyOTM2ODk3MzI3MDUyMjUwNDU2OTY4Nzc4NjE2NzU3MjcyMDMyNTc5OTc1ODA3MDYxNjM3MDE1ODU4ODg3ODIxODEzMzA0NTA3OTUyMDU3MjIxNjEyOTk2Nzk1NyJdLCBbIm1hc3Rlcl9zZWNyZXQiLCAiMzQxNDYzOTI3NjM1NjExMDU1Mzg0MTE2NjEzMjA0NTIzOTYwNjEzMTAxODg3Mjg1ODkwNjA2NTcyMTA5MTA3OTYyNzY5MjU0NTA3OTg4Nzc3OTc4MTM1MDkxNTc4NDA2NTE5NzA4NzI5MTQ4MDE2NTY2OTQ2NjM0NzA0MzM5NjUxNTAxODE5MjkyNTI4MzA1MzM0OTc0NjE4MDI1MTMzNjY4NjkzNzg1MTc1Nzg4ODkwNzAxOTc2NDY5NTE2NTcxNTgzNzAwMjA5ODE3NDg5MjMyMjkxNjI0OTE4NDA4MjUyMTU1MDQxOTM1MDU0MzU5NDQ5NTc3MDY1NjYxMjU2MjAzNzk3NTA0MjA0MDY3MjM1MzM2Mjc4NDk4NjEzMDkzNDk2NzM2MjAwNjk3OTQ2Mzc1MDk4ODYzNTE0MDkxNDAyMTQ3NDM0NjQwODEwNjc4OTE2MDMwMzgyNjQ0MzUwOTAyMzc3Njc3Mjk5NzYzMjM3MDk0NDg0MDc1MTYyNDE2MTUyMjA0NzU1ODc1MTE5ODg2MTMwMDU5ODI5MTcwNjYwNDk4MDY1OTU5NTYzNzQzNzU3ODE2MzQwMzQ4NjE4ODE2NTI0MjE2Nzc0Nzg0NjY1MDA1MjM1NTQyNzI5MzUzMzU5NjIxNjQ0MjUxNjExODM3MzA0OTM0NTEwMzMyMjk4NzQ3NDIzNDIyMTIwNTA2MjE4MDY4Nzc0NDQxOTg0NDQ5NDU1MzY4NTQ2MDY5NDc3ODA0MTQxODQyNjk4NDM4NTE1MTYwNzYzODcyNTE2NzQ4Mjk3MDQyNzY3NjgxNjQwODg5NjA2MzM1MDc1MTM0NzkxODEwMTc3MDg1NzU0OTE1OTk5OTY4NDg1NTYwMzc1MTI0MDY1MDU0MzE1NTIwNTkyNjkwNDA3NTQ4MzM1MDU2MDQ0Il0sIFsiZnVsbF9uYW1lIiwgIjI3MDI2MTQ5NzEwODU5ODY0NzkzMjI1MjI3NjIyNDQxODYxNzk4Njc2Mjc2MjMyODcxOTM3MDkzMjMwNzA4MjI2MTc3NTY4Mjg0MTYzNTU2ODkzMTAxOTg3MzU4MTI0NTc2OTc4Njc2OTMxNDE1ODY0Mzc2MzU2OTEzNjIzODMyMDQ0NjcwOTE5NzQ3MTkwOTA0NzIzMzMwMjg0NDAzNTk1NzAxOTI0MjI3OTY3MzM2OTY2Mzg5OTI2NTM5MTQ4MjY3NTU3NTAzMzczMDM4OTI2Mzk5MjE4MjIwMDcyMDM5MTEyNTUxMzcxODEyMDgwNDE4NDg1MjY2ODc2ODE1Njg0MjExNzk0NTcyNDQ3MjU5NjMyNzIzMTc5MDIzMzcxMzEwMjU1NzAyMTQ5NDE0MTA1Njg3MDMwMDU5NDA2MjA1Mjk2NzIzMzYxNTA0NjI2MzkyNjI1MDY1NDIxMzA2MjMzNDU3MTY1MTM0MjI0ODIzNzk3NjkyNjA3MDUxNDQxODI5NDY1MTgwMjAyMzI3NzE1NDgzMzUwNTgyOTE1NjM5NTExMjE5NDE4NzQ4NDkyNjMyMzA4NDAwNDE1Nzc0NzM3NjcxODQwMzg0NTg4NTE0OTg2NDg3Mjg2MDIzMjc5NjMyMjc3NDYzNTgyMzA4MjQ5NzM1MTMyODU3NTU5ODM2ODU3OTkzMjczMjQ0MjczNjQ4NzAxODI5NzM1MjA4MTkyODU3MjU2OTU3NDAwMjc3ODQwMjQzNjc0NDYxNDQ4OTA5NzIyNjUxNzY3MzY2Mzk0MTIzODY3MDY1ODYwMjkxOTk5ODk0MTk3MTA1MTg3NDE2NDU0MDgxMzg1MDc3Mzg3MjYzMzQyNzQ5MjU4OTI3NjYxMDI1OTI3MTIyNzYzOTUxNzEzNjA4OTY4ODM2MTAxMTkwMiJdXX0sICJub25jZSI6ICI1MDM3MTk3ODA1OTM4OTYyNDY5NzY1OSJ9"},"mime-type":"application/json"}],"credential_preview":{"@type":"https://didcomm.org/issue-credential/2.0/credential-preview","attributes":[{"name":"full_name","value":"amarjeet_march28"},{"name":"id","value":"1061"}]}},"comments":"Emp id issance","credFormat":"indy","protocol":"AIP2_0","signature":"Ed25519Signature2018","shortUrl":"https://testapi-issuer.nborbit.ca/url/6bda236d-3580-4e65-b889-b826377a7fc2","credOfferId":"cfe8aa01-74d4-43ca-8e54-77719e963dbd","credAutoIssue":false,"createClaim":false,"longUrl":"","recipientEmail":null,"recipientName":null,"invitationMessageId":null,"declineReason":null,"errorMessage":null,"issuanceType":"DID_EXCHANGE","isRevoked":false,"revokedDateTime":null,"statusEntryCorrelationId":null,"statusListId":null,"statusListIndex":null,"createdAt":"2025-04-15T15:53:32.592Z","updatedAt":"2025-04-15T15:53:52.956Z"}}
```

#### Detailed Breakdown of the response&#x20;

* **Credential ID**: `844`\
  This is the internal identifier used by the system to track this specific credential.
* **Status**: `credential-issued`\
  This indicates that the credential has been fully issued to the holder and is available in their wallet.
* **Credential Exchange ID**: `6bda236d-3580-4e65-b889-b826377a7fc2`\
  A unique identifier used to track the entire credential issuance exchange between the issuer and holder agents.
* **Issuer DID**: `6YXT2jddYg1TZarJjbKGng`\
  The Decentralized Identifier (DID) of the issuer agent that created and issued the credential.
* **Issuance Date**: `2025-04-15`\
  This is the date when the credential was successfully issued.
* **Expiration Date**: `null`\
  No expiration date has been set for this credential, meaning it is valid indefinitely unless revoked manually.
* **Credential Definition ID**: `6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1`\
  This ID refers to the definition used to structure the credential. It includes the issuer’s DID, the type (`CL` stands for "Camenisch–Lysyanskaya" credential), the schema sequence number (`2755408`), and the tag (`emp_new_1`).
* **Schema Ledger ID**: `6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5`\
  This refers to the schema under which the credential was created. It includes the issuer’s DID, the schema name (`Emp_cred_new`), and version (`5.5`).
* **Credential Offer ID**: `0456b36b-5c52-4f62-87dd-8c27b30a2fd0`\
  This ID uniquely identifies the offer that was sent to the holder before the credential was issued.
* **Offer Type**: `https://didcomm.org/issue-credential/2.0/offer-credential`\
  This URL defines the protocol format used for issuing the credential, following the DIDComm v2 standard.
* **Comment**: `Emp id issuance`\
  A short note or reason for issuing the credential, indicating that this is an employee ID.
* **Attachment Format**: `hlindy/cred-abstract@v2.0`\
  This format defines the type of the credential being attached – it's a Hyperledger Indy abstract credential used in version 2.0 of the credential protocol.
* **Offer (Base64-encoded)**:\
  The actual credential offer is encoded in base64 for secure transmission. This encoded data contains the attributes and metadata of the credential offer and can be decoded if needed for inspection.





