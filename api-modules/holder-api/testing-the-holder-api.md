# Testing the Holder API

### **Introduction**

The below steps outline the test plan for accepting credential Offer, storing credential into wallet , sending credential proof presentation. In addition to the test plan, the details below also include steps for above scenarios.

### **Test Objective**

* To ensure that credential offers can be is received to holders from issuer
* To validate that holders receive the credential offers from the issuer.
* To confirm that credentials can be stored successfully
* Present proof request of Verifier

### **Pr-requisites**

* The NB Orbit Enterprise Issuer API has been downloaded to your system.
* POSTMAN has been installed on your system.

### **Environment Setup in Postman**

1. **Create a Global Environment**:
   * Go to Environments on the top right corner of Postman.
   * Click on Add.
   * Name the environment (e.g., "Holder API Environment").
   *   Add the following variables:

       * `baseUrl`: [https://testapi-holder.nborbit.ca/](https://testapi-issuer.nborbit.ca/)
       * `apiKey`: ru04t0PD3Hq\_5ddOUdXagmwEh2AWntn6
       * `lobId`: 4461a984-1dfd-4c59-a974-eddc5f64f519



### Test Cases <a href="#test-cases" id="test-cases"></a>

### <mark style="color:blue;">Test Scenario 1:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test Fetch Credential Offer API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Fetch  Credential Offers".
* Set the request type to GET.
* Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/credential-offers.

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

3.  **Send Request**:

    Click Send.\
    Verify the response with 200 to ensure it displays all credential offers with details.

**Expected Result**: The response should display all the credential offers received from the issuer

#### Response Body&#x20;

```json
{
  "success": true,
  "message": "Credential offer fetched successfully.",
  "data": {
    "meta": {
      "totalItems": 2,
      "itemCount": 2,
      "itemsPerPage": 10,
      "totalPages": 1,
      "currentPage": 1
    },
    "items": [
      {
        "issuanceId": 42,
        "credentialStatus": "offer-received",
        "issuerDid": "6YXT2jddYg1TZarJjbKGng",
        "issuanceDate": "2025-04-15",
        "credDefId": "6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1",
        "schemaLedgerId": "6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5",
        "credentialPreview": {
          "attributes": [
            {
              "name": "full_name",
              "value": "amarjeet_march28"
            },
            {
              "name": "id",
              "value": "1061"
            }
          ]
        },
      {
        "issuanceId": 30,
        "credentialStatus": "offer-received",
        "issuerDid": "6YXT2jddYg1TZarJjbKGng",
        "issuanceDate": "2025-04-07",
        "credDefId": "6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1",
        "schemaLedgerId": "6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5",
        "credentialPreview": {
          "attributes": [
            {
              "name": "full_name",
              "value": "amarjeet_march28"
            },
            {
              "name": "id",
              "value": "1061"
            }
          ]
        },
        "comments": null,
        "credFormat": "indy",
        "messageProtocol": "AIP2_0",
        "signature": "Ed25519Signature2018",
        "shortUrl": "http://34.237.85.119:5004/url/bd13840c-e4b6-4a03-bda2-817dc6847a3f",
        "longUrl": null,
        "recipientEmail": null,
        "recipientName": null,
        "declineReason": null,
        "errorMessage": null,
        "issuanceType": "DID_EXCHANGE",
        "authorityStatement": null,
        "createdAt": "2025-04-07T14:12:46.878Z",
        "updatedAt": "2025-04-07T14:12:46.878Z"
      }
    ]
  }
}
```

#### Detailed Breakdown

* **`success`: `true`**\
  Indicates the API call was successful.
* **`message`: `"Credential offer fetched successfully."`**\
  Describes the result of the API call — in this case, credential offers were retrieved.

#### &#x20;**`data`**&#x20;

This contains pagination metadata, even though only 2 items are returned:

* **`totalItems`: `2`** – Total number of credential offers retrieved.
* **`itemCount`: `2`** – Number of items in the current response.
* **`itemsPerPage`: `10`** – Max items per page (pagination support).
* **`totalPages`: `1`** – There is only one page of data.
* **`currentPage`: `1`** – Current page number being viewed.

#### &#x20;**`items`**&#x20;

This array contains **two credential offers**, each with its own metadata and preview.

**Item 1: Credential Offer with `issuanceId` 42**

* **`issuanceId`: `42`** – Unique ID of this credential issuance process.
* **`credentialStatus`: `"offer-received"`** – Indicates that the offer has been received but the credential is not yet issued.
* **`issuerDid`: `"6YXT2jddYg1TZarJjbKGng"`** – DID of the issuer who sent the credential offer.
* **`issuanceDate`: `"2025-04-15"`** – Date when the credential offer was created.
* **`credDefId`: `"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1"`** – Credential Definition ID used for the credential.
* **`schemaLedgerId`: `"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5"`** – Schema details for the credential type/version.
* **`credentialPreview`**:
  * `attributes`: Shows the attributes that will be included in the credential:
    * **`full_name`: `"amarjeet_march28"`**
    * **`id`: `"1061"`**

_Note:_ This item seems to be truncated or missing some fields like `comments`, `shortUrl`, etc.

&#x20;**Item 2: Credential Offer with `issuanceId` 30**

* **`issuanceId`: `30`** – Unique identifier for this credential issuance.
* **`credentialStatus`: `"offer-received"`** – The credential offer has been received.
* **`issuerDid`: `"6YXT2jddYg1TZarJjbKGng"`** – Issuer's DID.
* **`issuanceDate`: `"2025-04-07"`** – Offer creation date.
* **`credDefId`:** `"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1"` – Matches the one from Item 1.
* **`schemaLedgerId`:** `"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5"` – Matches Item 1 too.
* **`credentialPreview`**:
  * `attributes`:
    * **`full_name`: `"amarjeet_march28"`**
    * **`id`: `"1061"`**
* **`comments`: `null`** – No comments provided during offer.
* **`credFormat`: `"indy"`** – Credential format used (Hyperledger Indy).
* **`messageProtocol`: `"AIP2_0"`** – Aries Interop Profile protocol version 2.0 is used.
* **`signature`: `"Ed25519Signature2018"`** – Digital signature type used for the credential.
* **`shortUrl`:**\
  `http://34.237.85.119:5004/url/bd13840c-e4b6-4a03-bda2-817dc6847a3f`\
  – A short URL likely pointing to the credential offer or proof request (e.g., a QR code viewer or deep link).
* **`longUrl`: `null`** – No long-form URL provided.
* **`recipientEmail`, `recipientName`: `null`** – No recipient info explicitly mentioned in the metadata.
* **`declineReason`, `errorMessage`: `null`** – No errors or declines were recorded.
* **`issuanceType`: `"DID_EXCHANGE"`** – Indicates the credential issuance is based on an existing DID connection (secure, peer-to-peer).
* **`authorityStatement`: `null`** – No additional authority or legal statement included.
* **`createdAt`: `"2025-04-07T14:12:46.878Z"`** – Timestamp when this offer was created.
* **`updatedAt`: `"2025-04-07T14:12:46.878Z"`** – Last update time for this record.

***

### <mark style="color:blue;">Test Scenario 2:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  "Accept Credential Offer" API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Accept  Credential Offers".
* Set the request type to POST.
* Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/offer-decision.

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.



3. Request Body \
   credOfferId = IssuanceId (42) from Get Offers API

```
{
        "credOfferId":42,
        "consent": "Accept",
        "declineReason": "decline offer reason",
        "retainConnection": True
    }
```

#### Detailed Breakdown

**`credOfferId`: `42`**

* **Type:** Integer
* **Meaning:**\
  This is the **unique identifier** for the credential offer being acted upon.
* **Purpose:**\
  It allows the backend to identify which specific offer the holder is responding to.
* **Contextual Example:**\
  This corresponds to an `issuanceId` from the previously fetched list of credential offers (e.g., the one with ID `42`).

**`consent`: `"Accept"`**

* **Type:** String (Enum-like)
* **Possible Values:**
  * `"Accept"` – The holder agrees to receive and store the credential.
  * `"Decline"` – The holder chooses not to accept the offer.
* **Purpose:**\
  Represents the **user's decision** regarding the credential offer.
* **Behavior:**
  * If `"Accept"`: The agent will typically send a `request-credential` message to complete the issuance process.
  * If `"Decline"`: The offer is rejected, and the process is stopped or logged.

**`declineReason`: `"decline offer reason"`**

* **Type:** String
* **Meaning:**\
  A textual reason explaining **why the credential offer is being declined**.
* **Important Note:**
  * This field is still present even when `"consent": "Accept"` — which may not be required and could be ignored in that case.
  * Typically **used only when declining** an offer (`"consent": "Decline"`).
* **Use Case Example:**
  * `"declineReason": "Information mismatch"`
  * `"declineReason": "Duplicate credential"`

**`retainConnection`: `true`**

* **Type:** Boolean
* **Meaning:**\
  Indicates whether to **retain the DID connection** with the issuer after handling the credential offer.
* **Use Cases:**
  * **`true`**: Keep the secure connection active for future interactions (e.g., for proof presentations, future credentials).
  * **`false`**: Close or clean up the connection after the action is performed.



4. **Send Request**:

Click Send.\
Verify the response with 201 to ensure it displays all credential offers with details.

**Expected Result**: The response should display that  the credential offers is accepted successfully



#### Response Body&#x20;

```json
{"success":true,"message":"Credential offer processed successfully","data":{"responseDetails":"Credential offer accepted successfully"}}    
```

#### Detailed Breakdown

**`success`: `true`**

* **Type:** Boolean
* **Meaning:**\
  Indicates whether the request to process the credential offer was **successful**.
* **Value:**
  * `true`: The operation completed without errors.
  * `false`: There was an error or failure in processing.

**`message`: `"Credential offer processed successfully"`**

* **Type:** String
* **Meaning:**\
  A general status **message** about the result of the request.
* **Purpose:**\
  Used to confirm the **successful handling** of the credential offer request (either accept or decline).

&#x20;**`data`**

* **Type:** Object
* **Meaning:**\
  Contains **additional information** or response details specific to the operation performed.

&#x20;**`responseDetails`: `"Credential offer accepted successfully"`**

* **Type:** String
* **Meaning:**\
  A more specific and descriptive message explaining what happened — in this case, that the credential offer was **successfully accepted**.
* **Use Case:**\
  This helps clients or users **differentiate** between various outcomes like "accepted" vs "declined", even though the outer message is generic.

### <mark style="color:blue;">Test Scenario 3:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  "Fetch Issued Credential" API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Fetch  Issued Credential ".
* Set the request type to GET.
* Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/credential-offers.
* Set Query Parameter as state=credential-received

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

3.  **Send Request**:

    Click Send.\
    Verify the response with 200 to ensure it displays all credential offers with details.

**Expected Result**: The response should display all the credential offers received from the issuer

#### Response Body&#x20;

```json
{"success":true,"message":"Credential offer fetched successfully.","data":{"meta":{"totalItems":1,"itemCount":1,"itemsPerPage":10,"totalPages":1,"currentPage":1},"items":[{"issuanceId":43,"credentialStatus":"credential-received","issuerDid":"6YXT2jddYg1TZarJjbKGng","issuanceDate":"2025-04-15","credDefId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1","schemaLedgerId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5","credentialPreview":{"attributes":[{"name":"full_name","value":"amarjeet_march28"},{"name":"id","value":"1061"}]},"comments":null,"credFormat":"indy","messageProtocol":"AIP2_0","signature":"Ed25519Signature2018","shortUrl":"http://34.237.85.119:5004/url/31a30ca8-52e0-4fa7-8dde-69798b890a7c","longUrl":null,"recipientEmail":null,"recipientName":null,"declineReason":null,"errorMessage":null,"issuanceType":"DID_EXCHANGE","authorityStatement":null,"createdAt":"2025-04-15T15:53:32.809Z","updatedAt":"2025-04-15T15:53:53.273Z"}]}}
```

#### Detailed Breakdown

#### `success: true`

* **Type:** Boolean
* **Meaning:** The request to fetch the credential offer was successful.

#### &#x20;`message: "Credential offer fetched successfully."`

* **Type:** String
* **Purpose:** A descriptive message confirming the successful retrieval of the credential offer(s).

#### &#x20;`data`

* **Type:** Object
* **Contains:** Metadata and a list of credential offers.

#### `meta`

* **Details about pagination and item count.**

**• `totalItems: 1`**

* Total number of credential offers retrieved.

**• `itemCount: 1`**

* Number of items in the current response.

**• `itemsPerPage: 10`**

* Maximum number of items that can be displayed per page.

**• `totalPages: 1`**

* Total pages of results available.

**• `currentPage: 1`**

* The current page number.

#### &#x20;`items` (Array of credential offer entries)

&#x20;**Credential Offer 1**

**🔹 `issuanceId: 43`**

* Unique identifier for this credential issuance.

**🔹 `credentialStatus: "credential-received"`**

* Indicates the current status.
  * `"credential-received"` means the credential has been issued and received by the holder.

**🔹 `issuerDid: "6YXT2jddYg1TZarJjbKGng"`**

* DID (Decentralized Identifier) of the issuing agent.

**🔹 `issuanceDate: "2025-04-15"`**

* The date when the credential was issued.

**🔹 `credDefId`**

* Credential Definition ID.
* Format: `{issuer DID}:3:CL:{schema ID}:{tag}`
* Used to identify the structure and type of the credential.

**🔹 `schemaLedgerId`**

* Identifier for the schema on the ledger.

&#x20;`credentialPreview.attributes`

* A list of attributes being shared as part of the credential.

**Attributes:**

* `full_name`: "amarjeet\_march28"
* `id`: "1061"

#### &#x20;Other Technical Details

**🔹 `comments`: `null`**

* No comment was included with the credential offer.

**🔹 `credFormat`: `"indy"`**

* Format used for credential (Hyperledger Indy format).

**🔹 `messageProtocol`: `"AIP2_0"`**

* Aries Interop Profile version used for this credential exchange.

**🔹 `signature`: `"Ed25519Signature2018"`**

* Signature algorithm used for signing the credential.

**🔹 `shortUrl`**

* A shortened URL for accessing or sharing the credential:
  * `http://34.237.85.119:5004/url/31a30ca8-52e0-4fa7-8dde-69798b890a7c`

**🔹 `longUrl`: `null`**

* No expanded long URL provided.

#### Recipient Details

**• `recipientEmail`, `recipientName`: `null`**

* No specific email or name recorded for the recipient.

#### Error Handling

**• `declineReason`, `errorMessage`: `null`**

* No decline reason or error message — this indicates the offer was processed successfully.

#### `issuanceType: "DID_EXCHANGE"`

* Type of issuance — credential was shared through a DID connection.

#### `authorityStatement`: `null`

* Not included; possibly used in regulatory or compliance cases.

#### &#x20;Timestamps

**• `createdAt`: `"2025-04-15T15:53:32.809Z"`**

* Timestamp when the offer record was created.

**• `updatedAt`: `"2025-04-15T15:53:53.273Z"`**

* Timestamp when the offer record was last updated (possibly when received).

***

### <mark style="color:blue;">Test Scenario 4:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  "Store Credential " API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Acceptch  Credential ".
* Set the request type to POST.
* Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/store-credential.

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.



3. Request Body \
   credOfferId = IssuanceId (42) from Get Offers API

```
{
                   "credOfferId": 1,
                   "createClaim": false
                  }
```

#### Detailed Breakdown

* **`credOfferId`: 1**
  * This is the unique identifier (`ID`) for a specific credential offer.
  * It tells the system **which offer** this action refers to.
  * In this case, the credential offer with ID **1** is being targeted.
* **`createClaim`: false**
  * This boolean flag indicates whether or not to **automatically create a credential claim** after accepting the offer.
  * `false` means the system **should not proceed** with claim creation.
  * This is typically used when the recipient wants to **delay** storing the credential in the wallet or handle the credential in a custom way before storing.

4. **Send Request**:

Click Send.\
Verify the response with 201 to ensure it displays all credential offers with details.

**Expected Result**: The response should display that  the credential offers is accepted successfully



#### Response Body&#x20;

```json
{"success":true,"message":"Credential stored successfully","data":{"responseDetails":"Credential record (31a30ca8-52e0-4fa7-8dde-69798b890a7c) stored successfully"}}
```

#### Detailed Breakdown

* **`success`: `true`**
  * This is a boolean flag indicating the outcome of the request.
  * `true` confirms that the operation (storing the credential) was **successful**.
* **`message`: `"Credential stored successfully"`**
  * A user-friendly message summarizing the result of the request.
  * Confirms that the credential has been stored in the holder’s wallet or database.
* **`data`: { ... }**
  * Contains additional **metadata or details** about the outcome.
  * Inside `data`, we have:
    * **`responseDetails`:**\
      `"Credential record (31a30ca8-52e0-4fa7-8dde-69798b890a7c) stored successfully"`
      * Provides more specific context about what was stored.
      * The string inside the parentheses — `31a30ca8-52e0-4fa7-8dde-69798b890a7c` — is likely the **unique identifier (UUID)** for the credential record that was successfully stored.
      * This ID can be used later for:
        * Retrieving credential details
        * Proof generation
        * Verifying or revoking the credential\
          \


### <mark style="color:blue;">Test Scenario 5:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  "Fetch Wallet Credential " API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Fetch  Wallet Credential".
* Set the request type to GET.
* Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/wallet/credentials.



2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

3.  **Send Request**:

    Click Send.\
    Verify the response with 200 to ensure it displays all credential offers with details.

**Expected Result**: The response should display all the credential offers received from the issuer

#### Response Body&#x20;

```json
{
  "success": true,
  "message": "Credential Offers fetched successfully.",
  "data": {
    "items": [
      {
        "issuanceId": 1,
        "credentialStatus": "offer-received",
        "issuerDid": "did:sov:7ordz2rHZ31iX9R25jjcMY",
        "issuanceDate": "2024-08-06",
        "credDefId": "7ordz2rHZ31iX9R25jjcMY:3:CL:1505846:DL_cred",
        "schemaLedgerId": "PQ3H8NiUBguTivwkJRuHGC:2:Driving_license_New:6.0",
        "credentialPreview": {
          "attributes": [
            {
              "name": "full_name",
              "value": "John Doe"
            }
          ]
        },
        "comments": "A comment",
        "credFormat": "Hyperledger Indy Credential Abstract",
        "messageProtocol": "AIP2_0",
        "signature": "Ed25519Signature2018",
        "shortUrl": "http://100.28.204.79:5004/url/c41e9706-aee1-4397-bb91-ab027cf08a6d",
        "longUrl": "http://100.28.204.79:5004?oob=eyhchc41e9706aee14397...bb91ab027cf08a6d",
        "recipientEmail": "john@example.com",
        "recipientName": "john",
        "declineReason": "Data is incorrect",
        "errorMessage": "error message",
        "issuanceType": "DID_EXCHANGE",
        "authorityStatement": "offer-trusted",
        "createdAt": "2024-08-06T16:02:15.484Z",
        "updatedAt": "2024-08-06T16:02:15.484Z"
      }
    ],
    "meta": {
      "totalItems": 100,
      "itemCount": 10,
      "itemsPerPage": 10,
      "totalPages": 10,
      "currentPage": 1
    }
  }
}
```

#### Detailed Breakdown

* **`success`**: This boolean flag is set to `true`, which confirms that the request was successfully processed by the server.
* **`message`**: The string message `"Credential Offers fetched successfully."` provides a human-readable confirmation that the list of credential offers was retrieved without any issues.
* **`data`**: This is the main container object that includes the actual list of credential offers (`items`) and pagination metadata (`meta`).

#### Credential Offer Details (Inside `data.items`)

The `items` array contains individual credential offer objects. In this example, there is one credential offer with the following details:

* **`issuanceId`**: A unique ID `1` assigned to this particular credential issuance record.
* **`credentialStatus`**: The status is `"offer-received"`, which means the credential has been received but not yet accepted or declined.
* **`issuerDid`**: This field holds the DID of the issuer, which is `"did:sov:7ordz2rHZ31iX9R25jjcMY"`. It uniquely identifies the organization or agent offering the credential.
* **`issuanceDate`**: `"2024-08-06"` marks the date the credential offer was issued.
* **`credDefId`**: The Credential Definition ID is `"7ordz2rHZ31iX9R25jjcMY:3:CL:1505846:DL_cred"`, which specifies the credential’s schema and definition on the ledger.
* **`schemaLedgerId`**: This ID `"PQ3H8NiUBguTivwkJRuHGC:2:Driving_license_New:6.0"` identifies the specific schema used for issuing this credential.
* **`credentialPreview`**: This object contains a preview of the credential attributes being offered. It includes:
  * `"full_name"` with value `"John Doe"`
* **`comments`**: The value `"A comment"` indicates that the issuer may have added a custom note or description for this offer.
* **`credFormat`**: The format is `"Hyperledger Indy Credential Abstract"`, showing that the credential follows the Indy standard.
* **`messageProtocol`**: `"AIP2_0"` specifies the Aries Interop Profile version being used for messaging.
* **`signature`**: `"Ed25519Signature2018"` is the cryptographic signature algorithm used for signing the credential.
* **`shortUrl`**: A shortened link (`"http://100.28.204.79:5004/url/c41e9706-aee1-4397-bb91-ab027cf08a6d"`) is provided, likely to be shared with the holder for easy access.
* **`longUrl`**: The full URL (`"http://100.28.204.79:5004?oob=..."`) represents the encoded Out-of-Band invitation or credential data in more detail.
* **`recipientEmail`** and **`recipientName`**: These fields (`"john@example.com"` and `"john"`) identify the person to whom the credential is being offered.
* **`declineReason`**: `"Data is incorrect"` suggests that a reason was given previously (if applicable) for declining the offer.
* **`errorMessage`**: Contains a general `"error message"` if there were any issues during the offer process.
* **`issuanceType`**: `"DID_EXCHANGE"` indicates that the offer was made over a secure DID connection.
* **`authorityStatement`**: `"offer-trusted"` may imply a trust level or regulatory statement attached to the credential offer.
* **`createdAt`** and **`updatedAt`**: Both timestamps (`"2024-08-06T16:02:15.484Z"`) mark when the credential offer was created and last updated.

#### &#x20;Pagination Metadata (Inside `data.meta`)

The `meta` object provides essential information for handling multiple credential offers across pages:

* **`totalItems`**: There are 100 total credential offers in the system.
* **`itemCount`**: The current response contains 10 credential offers.
* **`itemsPerPage`**: Each page is limited to 10 items.
* **`totalPages`**: There are 10 pages in total.
* **`currentPage`**: This is the 1st page of the results.



### <mark style="color:blue;">Test Scenario 6:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  "Delete Credential Offer" API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Delete  Credential Offers".
* Set the request type to DELETE.
* Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/credential-offer

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.



3. Request Body \
   credOfferId = IssuanceId (42) from Get Offers API

```
{
                   "credOfferId": 42
                  }
```

#### Detailed Breakdown

* **`credOfferId`: 1**
  * This is the unique identifier (`ID`) for a specific credential offer.
  * It tells the system **which offer** this action refers to.
  * In this case, the credential offer with ID **1** is being targeted.



4. **Send Request**:

Click Send.\
Verify the response with 200 to ensure it displays all credential offers with details.

**Expected Result**: The response should display that  the credential offers is accepted successfully



#### Response Body&#x20;

```json
 {"success":true,"message":"Credential offer deleted successfully.","data":{"responseDetails":"Credential offer deleted successfully."}}
```

#### Detailed Breakdown

*

    * **`"success": true`**
      * This indicates that the API request was **successfully processed** without any errors.
      * A `true` value means the system performed the requested action as expected.
    * **`"message": "Credential offer deleted successfully."`**
      * This is a general message confirming the **outcome of the request**.
      * It provides a **user-friendly description** of what happened: the credential offer was deleted.
    * **`"data"`** (an object containing further details):
      * This field **encapsulates more specific information** about the response.
      * **`"responseDetails": "Credential offer deleted successfully."`**
        * This echoes the main message but is likely used internally for logging, auditing, or debugging.
        * It ensures that there’s **redundancy in communication**, reinforcing that the operation was successful.



### <mark style="color:blue;">Test Scenario 7:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  "Delete Credential" API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Delete  Credential ".
* Set the request type to DELETE.
* Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/wallet/credential

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.



3. Request Body \
   credentialId = IssuanceId (42) from Get wallet credential API

```
{
                   "credentialId": 42
                  }
```

#### Detailed Breakdown

* credentialI&#x64;**: 42**
  * This is the unique identifier (`ID`) for a specific credential offer.
  * It tells the system **which offer** this action refers to.
  * In this case, the credential offer with ID **1** is being targeted.



4. **Send Request**:

Click Send.\
Verify the response with 200 to ensure it displays all credential offers with details.

**Expected Result**: The response should display that  the credential offers is accepted successfully



#### Response Body&#x20;

```json
{"success":true,"message":"credential deleted successfully.","data":{"responseDetails":"Credential deleted successfully from wallet."}}
```

#### Detailed Breakdown

* **`success: true`**\
  Indicates that the API call was successfully processed without any error.
* **`message: "credential deleted successfully."`**\
  A high-level message confirming that the credential deletion was executed as intended.
* **`data`**\
  Contains a nested object that provides more detailed information about the operation.
  * **`responseDetails: "Credential deleted successfully from wallet."`**\
    Specifically clarifies that the deleted credential was removed from the **wallet**, not just from a record or system queue. This ensures the user or system knows the data has been fully erased from the agent's storage.



### <mark style="color:blue;">Test Scenario 8:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  "Fetch Proof Request" API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Fetch  Proof Offers".
* Set the request type to GET.
* Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/proof-requests.



2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

3.  **Send Request**:

    Click Send.\
    Verify the response with 200 to ensure it displays all credential offers with details.

**Expected Result**: The response should display all the credential offers received from the issuer

#### Response Body&#x20;

```json
{"success":true,"message":"proof request fetch successfully.","data":{"items":[{"id":47,"presentationInvitationUrl":null,"presentationRequest":{"name":"emp_details_prro","nonce":"1","requestedAttributes":{"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo":{"restrictions":[{"schemaId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5","credDefId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo"}],"attributes":["full_name","id"]}},"requestedPredicates":{}},"presentationInvitationShortUrl":"http://34.237.85.119:5004/url/8249b361-db8f-47e0-ad74-efd2a52b4307","presentationExchangeId":"8249b361-db8f-47e0-ad74-efd2a52b4307","invitationMsgId":null,"proofProtocol":null,"messageProtocol":null,"threadId":null,"presentationStatus":"request-received","declineReason":null,"authorityStatement":null,"createClaim":false,"errorMessage":null,"createdAt":"2025-04-16T12:04:18.930Z","updatedAt":"2025-04-16T12:04:18.930Z"},{"id":45,"presentationInvitationUrl":null,"presentationRequest":{"name":"emp_details_prro","nonce":"1","requestedAttributes":{"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo":{"restrictions":[{"schemaId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5","credDefId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo"}],"attributes":["full_name","id"]}},"requestedPredicates":{}},"presentationInvitationShortUrl":"http://34.237.85.119:5004/url/e52a877e-11e1-4d94-bada-2a1c8d9cb160","presentationExchangeId":"e52a877e-11e1-4d94-bada-2a1c8d9cb160","invitationMsgId":null,"proofProtocol":null,"messageProtocol":null,"threadId":null,"presentationStatus":"request-received","declineReason":null,"authorityStatement":null,"createClaim":false,"errorMessage":null,"createdAt":"2025-04-10T10:46:54.144Z","updatedAt":"2025-04-10T10:46:54.144Z"},{"id":43,"presentationInvitationUrl":null,"presentationRequest":{"name":"emp_details_prro","nonce":"1","requestedAttributes":{"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo":{"restrictions":[{"schemaId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5","credDefId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo"}],"attributes":["full_name","id"]}},"requestedPredicates":{}},"presentationInvitationShortUrl":"http://34.237.85.119:5004/url/81b06248-2ec8-4482-95b5-fc15d26eb4a1","presentationExchangeId":"81b06248-2ec8-4482-95b5-fc15d26eb4a1","invitationMsgId":null,"proofProtocol":null,"messageProtocol":null,"threadId":null,"presentationStatus":"request-received","declineReason":null,"authorityStatement":null,"createClaim":false,"errorMessage":null,"createdAt":"2025-04-10T10:35:03.257Z","updatedAt":"2025-04-10T10:35:03.257Z"},{"id":42,"presentationInvitationUrl":null,"presentationRequest":{"name":"emp_details_prro","nonce":"1","requestedAttributes":{"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo":{"restrictions":[{"schemaId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5","credDefId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo"}],"attributes":["full_name","id"]}},"requestedPredicates":{}},"presentationInvitationShortUrl":"http://34.237.85.119:5004/url/6d8115f6-cd0d-4d48-b64e-e41f8223f092","presentationExchangeId":"6d8115f6-cd0d-4d48-b64e-e41f8223f092","invitationMsgId":null,"proofProtocol":null,"messageProtocol":null,"threadId":null,"presentationStatus":"request-received","declineReason":null,"authorityStatement":null,"createClaim":false,"errorMessage":null,"createdAt":"2025-04-10T10:34:15.416Z","updatedAt":"2025-04-10T10:34:15.416Z"},{"id":41,"presentationInvitationUrl":null,"presentationRequest":{"name":"emp_details_prro","nonce":"1","requestedAttributes":{"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo":{"restrictions":[{"schemaId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5","credDefId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo"}],"attributes":["full_name","id"]}},"requestedPredicates":{}},"presentationInvitationShortUrl":"http://34.237.85.119:5004/url/29f32d64-a66e-41d7-aa69-d156d12705bd","presentationExchangeId":"29f32d64-a66e-41d7-aa69-d156d12705bd","invitationMsgId":null,"proofProtocol":null,"messageProtocol":null,"threadId":null,"presentationStatus":"request-received","declineReason":null,"authorityStatement":null,"createClaim":false,"errorMessage":null,"createdAt":"2025-04-10T10:32:26.747Z","updatedAt":"2025-04-10T10:32:26.747Z"},{"id":40,"presentationInvitationUrl":null,"presentationRequest":{"name":"emp_details_prro","nonce":"1","requestedAttributes":{"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo":{"restrictions":[{"schemaId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5","credDefId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo"}],"attributes":["full_name","id"]}},"requestedPredicates":{}},"presentationInvitationShortUrl":"http://34.237.85.119:5004/url/755ceaa8-1dae-4fc7-90b9-b9559333596d","presentationExchangeId":"755ceaa8-1dae-4fc7-90b9-b9559333596d","invitationMsgId":null,"proofProtocol":null,"messageProtocol":null,"threadId":null,"presentationStatus":"request-received","declineReason":null,"authorityStatement":null,"createClaim":false,"errorMessage":null,"createdAt":"2025-04-10T10:30:14.483Z","updatedAt":"2025-04-10T10:30:14.483Z"},{"id":39,"presentationInvitationUrl":null,"presentationRequest":{"name":"emp_details_prro","nonce":"1","requestedAttributes":{"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo":{"restrictions":[{"schemaId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5","credDefId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo"}],"attributes":["full_name","id"]}},"requestedPredicates":{}},"presentationInvitationShortUrl":"http://34.237.85.119:5004/url/a500144d-2665-4760-81b2-09a4daa7d77f","presentationExchangeId":"a500144d-2665-4760-81b2-09a4daa7d77f","invitationMsgId":null,"proofProtocol":null,"messageProtocol":null,"threadId":null,"presentationStatus":"request-received","declineReason":null,"authorityStatement":null,"createClaim":false,"errorMessage":null,"createdAt":"2025-04-07T15:12:32.099Z","updatedAt":"2025-04-07T15:12:32.099Z"},{"id":38,"presentationInvitationUrl":null,"presentationRequest":{"name":"emp_details_prro","nonce":"1","requestedAttributes":{"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo":{"restrictions":[{"schemaId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5","credDefId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo"}],"attributes":["full_name","id"]}},"requestedPredicates":{}},"presentationInvitationShortUrl":"http://34.237.85.119:5004/url/d6292fa3-7811-48b0-8a26-858e790fbf79","presentationExchangeId":"d6292fa3-7811-48b0-8a26-858e790fbf79","invitationMsgId":null,"proofProtocol":null,"messageProtocol":null,"threadId":null,"presentationStatus":"request-received","declineReason":null,"authorityStatement":null,"createClaim":false,"errorMessage":null,"createdAt":"2025-04-07T10:17:28.548Z","updatedAt":"2025-04-07T10:17:28.548Z"},{"id":37,"presentationInvitationUrl":null,"presentationRequest":{"name":"emp_details_prro","nonce":"1","requestedAttributes":{"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo":{"restrictions":[{"schemaId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5","credDefId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo"}],"attributes":["full_name","id"]}},"requestedPredicates":{}},"presentationInvitationShortUrl":"http://34.237.85.119:5004/url/8738b361-3476-4936-b7d3-170040d4ab2b","presentationExchangeId":"8738b361-3476-4936-b7d3-170040d4ab2b","invitationMsgId":null,"proofProtocol":null,"messageProtocol":null,"threadId":null,"presentationStatus":"request-received","declineReason":null,"authorityStatement":null,"createClaim":false,"errorMessage":null,"createdAt":"2025-04-04T16:45:05.376Z","updatedAt":"2025-04-04T16:45:05.376Z"}],"meta":{"totalItems":9,"itemCount":9,"itemsPerPage":10,"totalPages":1,"currentPage":1}}}
```

#### Detailed Breakdown

*
  * **Presentation Name & Attributes**:
    * The proof request is named **"emp\_details\_prro"**.
    * It uses a **nonce value of "1"** for cryptographic uniqueness.
    * The proof request includes **requested attributes** related to employment credentials, specifically:
      * `full_name`
      * `id`
    * These attributes must be drawn from credentials matching the **credential definition ID**:\
      `6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo`,\
      and the **schema ID**:\
      `6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5`.
  * 🔹 **URLs & Identifiers**:
    * The **short invitation URL** that can be shared with a holder is:\
      `http://34.237.85.119:5004/url/8249b361-db8f-47e0-ad74-efd2a52b4307`.
    * This corresponds to a **presentation exchange ID**:\
      `8249b361-db8f-47e0-ad74-efd2a52b4307`.
  * 🔹 **Status & Metadata**:
    * The current **status** of the proof exchange is `"request-received"`, indicating that the request has been sent and the holder has not yet responded.
    * Other protocol-related fields like `proofProtocol`, `messageProtocol`, `threadId`, and `invitationMsgId` are **null**, suggesting this may be a basic proof protocol or a simplified flow without advanced threading or protocol metadata.
    * Flags like `createClaim` are set to **false**, meaning there is no intention to auto-generate a new claim based on this presentation.
    * **No errors** are reported (`errorMessage` is null), and no **decline reason** has been provided.
  * 🔹 **Timestamps**:
    * This proof request was **created and last updated** at the exact same time:\
      `"2025-04-16T12:04:18.930Z"`, showing no updates have occurred since creation.



### <mark style="color:blue;">Test Scenario 9:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  "Find Matching Credential" API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Fetch  Matcing credential for Proofs".
* Set the request type to GET.
* Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/{proof\_id}/matching-credentials.
* Add a path parameter for Proof Id -



2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

3.  **Send Request**:

    Click Send.\
    Verify the response with 200 to ensure it displays all credential offers with details.

**Expected Result**: The response should display all the credential offers received from the issuer

#### Response Body&#x20;

```json
{"success":true,"message":"wallet credential record found successfully.","data":[{"credDefId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo","schemaLedgerId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5","credentialReferentId":"e5ef13f4-025d-428e-9a2e-4ec89aa9094d","credentialId":27,"credentialStatus":"done","attributes":{"full_name":"amarjeet_non revo","id":"1061"}},{"credDefId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo","schemaLedgerId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5","credentialReferentId":"e14c0e41-8e40-4c44-8239-62db11962a69","credentialId":23,"credentialStatus":"done","attributes":{"full_name":"amarjeet_march28","id":"1061"}},{"credDefId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo","schemaLedgerId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5","credentialReferentId":"27b79e1d-95ce-483e-890f-1e8583a18c62","credentialId":28,"credentialStatus":"done","attributes":{"full_name":"amarjeet_non revo","id":"1061"}},{"credDefId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo","schemaLedgerId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5","credentialReferentId":"02073594-6c55-4600-93df-e2d79a8ce59a","credentialId":29,"credentialStatus":"done","attributes":{"full_name":"amarjeet_non revo","id":"1061"}},{"credDefId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo","schemaLedgerId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5","credentialReferentId":"4e320355-2041-4a1e-bd83-c6f96252533f","credentialId":24,"credentialStatus":"done","attributes":{"full_name":"amarjeet_non revo","id":"1061"}},{"credDefId":"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo","schemaLedgerId":"6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5","credentialReferentId":"1d60ed40-9ad3-4198-9107-398df490565c","credentialId":22,"credentialStatus":"done","attributes":{"full_name":"amarjeet_march28","id":"1061"}}]}
```

#### Detailed Breakdown

#### General Summary:

* **Success Message**: `wallet credential record found successfully.`
* **Credential Entries**: There are **6 credential records**, all marked with status `done`.

***

#### Credential Details (Grouped by `full_name`):

**1. Name: amarjeet\_non revo**

* Appears **4 times**
* All with same:
  * `credDefId`: `6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo`
  * `schemaLedgerId`: `6YXT2jddYg1TZarJjbKGng:2:Emp_cred_new:5.5`
  * `id`: `"1061"`
* Different `credentialReferentId` and `credentialId`

**2. Name: amarjeet\_march28**

* Appears **2 times**
* Also shares the same `credDefId`, `schemaLedgerId`, and `id`





### <mark style="color:blue;">Test Scenario 10:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  "Send Presentation " API</mark>_&#x20;

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Send Presentationl for Proofs".
* Set the request type to POST.
* Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/send-presentation.
* Add a path parameter for Proof Id -



2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

3. **Request Body**

```
{
  "proofId": 47,
  "createClaim": false,
  "requestedAttributes": {
    "6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo": 37
  },
  "requestedPredicates": {},
  "selfAttestedAttributes": {}
}
```

**Detailed Breakdown:**

* **`proofId`: 47**
  * This is a unique identifier assigned to this particular proof request. It helps in tracking or referencing the specific proof exchange session in logs, APIs, or databases.
* **`createClaim`: false**
  * This boolean flag indicates that no new claim (or credential issuance) is to be created as part of this operation. Instead, the holder is expected to present existing credentials in response to the proof request.
* **`requestedAttributes`**
  * This object defines which credential attributes are being requested for verification.
  * In this case, the key is a **Credential Definition ID**:\
    `"6YXT2jddYg1TZarJjbKGng:3:CL:2755408:emp_new_1_non_revo"`. This ID corresponds to a credential schema related to an employee credential named "emp\_new\_1\_non\_revo", which is **non-revocable**.
  * The value `37` is lthe credential Id stored iin the wallet..
* **`requestedPredicates`: { }**
  * This is an empty object, which means **no predicate-based conditions** (e.g., age > 18) are being requested in this proof. Predicates are often used for zero-knowledge proofs when the verifier wants to validate a condition without knowing the exact value.
* **`selfAttestedAttributes`: { }**
  * This is also empty, indicating that the verifier does **not permit any self-attested attributes** in this proof. Self-attested attributes are values the holder can provide manually without cryptographic verification from a credential.

**4.Send Request**:

Click Send.\
Verify the response with 201 to ensure it displays all credential offers with details.

**Expected Result**: The response should display all the credential offers received from the issuer

#### Response Body&#x20;

```json
{"success":true,"message":"Presentation processed successfully.","data":{"responseDetails":"Presentation sent successfully."}}
```

#### Detailed Breakdown

* **`success`: true**
  * This boolean value confirms that the API operation was **successful**. It signals to the client that the proof presentation was handled as expected, with no errors encountered.
* **`message`: "Presentation processed successfully."**
  * This human-readable message reiterates that the **presentation** (i.e., the holder's response to a proof request) has been successfully processed by the server.
* **`data`**
  * This object contains specific details related to the result of the operation:
    * **`responseDetails`: "Presentation sent successfully."**
      * This further confirms that the **presentation was sent** by the holder agent to the verifier.
      * It indicates that the credential data matched the requested attributes, and all validations (e.g., schema, revocation check if any, etc.) were passed, allowing the holder to send the cryptographic proof.



### <mark style="color:blue;">Test Scenario 11:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  "Decline Proof " API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Decline Proofs".
* Set the request type to POST.
* Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/decline-proof.





2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

3. **Request Body**

```
{
  "proofId": 1,
  "declineReason": "No trust"
}
```

**Detailed Breakdown:**

* **`proofId`: 1**
  * This is the **unique identifier** for the proof request that was declined. It serves as a reference to track or audit this specific proof interaction in the system.
* **`declineReason`: "No trust"**
  * This provides the **explicit reason** for declining the proof request. In this case, the phrase **"No trust"** indicates that the holder or entity receiving the request **did not trust the verifier** or had reservations about sharing the requested credential data.
  * This reason could stem from various concerns, such as:
    * The verifier was not known or verified.
    * The verifier’s DID or domain wasn't on the trust registry.
    * A mismatch in expected policies, security expectations, or intended purpose.

**4.Send Request**:

Click Send.\
Verify the response with 201 to ensure it displays all credential offers with details.

**Expected Result**: The response should display all the credential offers received from the issuer

#### Response Body&#x20;

```json
{"success":true,"message":"Presentation processed successfully.","data":{"responseDetails":"Presentation sent successfully."}}
```

#### Detailed Breakdown

* **`success`: true**
  * This indicates that the system **successfully handled the operation** — in this case, the process of declining a proof request.
  * It confirms that the system did not encounter any internal errors while recording or executing the decline.
* **`message`: "Proof Request processed successfully."**
  * This provides a **summary status message** stating that the proof request was processed, regardless of the final outcome (accepted or declined).
* **`data.responseDetails`: "Proof Request has been declined."**
  * This is the **core outcome**: the proof request was **explicitly declined** by the holder or responder.
  * This might happen for several reasons such as:
    * The holder doesn’t want to share personal information.
    * The verifier is not trusted.
    * The required credentials are not available or valid.



### <mark style="color:blue;">Test Scenario 12:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  "Delete Proof " API</mark>_

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Delete  Proof ".
* Set the request type to DELETE.
* Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/proof-request

2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.



3. Request Body \
   credentialId = IssuanceId (42) from Get wallet credential API

```
{
  "proofId": 1
}
```

#### Detailed Breakdown

* proofI&#x64;**: 42**
  * This is the unique identifier (`ID`) for a specific Proof request.
  * It tells the system **which Proof** this action refers to.
  * In this case, the Proof request with ID **1** is being targeted.



4. **Send Request**:

Click Send.\
Verify the response with 200 to ensure it displays all credential offers with details.

**Expected Result**: The response should display that  the credential offers is accepted successfully



#### Response Body&#x20;

```json
{"success":true,"message":"Proof record deleted successfully.","data":{"proofId":43,"status":"deleted"}}
```

#### Detailed Breakdown

* &#x20;**`"success": true`**\
  This confirms that the API call executed without errors and the operation (deletion of a proof record) was completed successfully.
* &#x20;**`"message": "Proof record deleted successfully."`**\
  A human-readable message that describes what happened — in this case, it confirms that the proof record has been deleted.
* &#x20;**`"data"`** object contains specific details about the deleted proof record:
  * **`"proofId": 43`**\
    This is the unique identifier of the proof record that was deleted.
  * **`"status": "deleted"`**\
    This shows the final state of the proof record after the operation, which is `"deleted"`, confirming that the record is no longer active or retrievable.



### <mark style="color:blue;">Test Scenario 13:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  "Find OOB Details " API</mark>_&#x20;

**Steps**:

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Fetch OOB details.
* Set the request type to POST.
* Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/oob-details.





2. **Add Authorization**:

* Click on the Authorization tab.
* Select API Key from the dropdown.
* Set the Key to `api-key`.
* Set the Value to `{{apiKey}}`.

3. **Request Body**

```
{
  "url": "http://localhost:5003/url/1a5b1427-7715-4fad-84c8-129cf04af1e7"
}
```

**Detailed Breakdown:**

* **`url`:**&#x20;
  * This is the **url for OOB credential or OOB proof requesr**.



**4.Send Request**:

Click Send.\
Verify the response with 201 to ensure it displays all credential offers with details.

**Expected Result**: The response should display all the credential offers received from the issuer

#### Response Body&#x20;

```json
{"success":true,"message":"out-of-band invitation accept successfully.","data":{"connectionLess":"No","givenName":"Issuer Test App Agent","messageProtocol":"AIP2_0","credOfferId":45}}
```

#### Detailed Breakdown

* **`"success": true`**\
  This indicates that the operation, in this case, accepting the out-of-band invitation, was successful without any errors.
* &#x20;**`"message": "out-of-band invitation accept successfully."`**\
  A human-readable message providing a confirmation that the out-of-band invitation has been successfully accepted.
* **`"data"`** object contains detailed information about the accepted invitation:
  * &#x20;**`"connectionLess": "No"`**\
    This shows the connection type used for the invitation. `"No"` here suggests that the invitation is not connectionless, meaning that the invitation was likely processed using a connection.
  * &#x20;**`"givenName": "Issuer Test App Agent"`**\
    This represents the name of the issuer or the agent associated with the invitation, in this case, labeled as `"Issuer Test App Agent"`. This is the entity that sent the invitation.
  * &#x20;**`"messageProtocol": "AIP2_0"`**\
    Indicates the message protocol used in this interaction. Here, `"AIP2_0"` refers to a specific version of the protocol, which could pertain to a particular implementation or standard in the out-of-band invitation process.
  * **`"credOfferId": 45`**\
    This is the unique identifier for the credential offer associated with the invitation. It links the invitation to a specific credential offer that is being extended.

Now , using this **`credOfferId`   one can perform the action to accept this credential and store it in the wallet. Same can be done with url of OOB proof request which provides proofId , and then can be processed to send proof presentation to the Verifier.**



