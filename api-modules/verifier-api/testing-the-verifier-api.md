# Testing the Verifier API

### Pre-Requisites:

1. The NB Orbit Enterprise Verifier API has been downloaded in your system.
2. POSTMAN has been installed in your system

**Environment Setup in Postman:**

1. **Create a Global Environment**:
   * Go to **Environments** on the top right corner of Postman.
   * Click on **Add**.
   * Name the environment (e.g., "Verifier API Environment").
   * Add the following variables:
     * `baseUrl`: `https://testapi-verifier.nborbit.ca`
     * `apiKey`: iLBFuTxf\_FQcA2N4II8CjbgTQHhDPKwa
     * `lobId`: 40f2d2dd-3398-4ebc-b3a1-f250eb0f9b47



### <mark style="color:blue;">Test Scenario 1:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test defining a proof request</mark>_

**Objective**: Verify that proof requests can be defined

**Testing Steps:**

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "Define Proof Request".
* Set the request type to POST.
*   Set the URL to `{{baseUrl}}/api/lob/{{lob_id}}/define-proof-request`.



2. **Add Authorization**:

* Click on the **Authorization** tab.
* Select **API Key** from the dropdown.
* Set the **Key** to `api-key`.
* Set the **Value** to `{{apiKey}}`.

3. **Add Request Body**:\
   a. **AnonCred**

```json
 {
        "requestedAttributes": [
            {
                "attributes": [
                    "first_name",
                    "last_name"
                    ],
                "restrictions": [
                 {
                 "schemaId": 70,
                 "credentialId": 55
                 }
                ]
                }
            ],
            "requestedPredicates": [
                            {
                            "attributeName": "dob",
                            "pType": "<",
                            "pValue": 20101111,
                            "proofValidTill": "2025-05-21T17:54:09.706Z",
                            "proofValidFrom": "2025-05-18T17:54:09.706Z",
                            "restrictions": [
                            {
                               "credentialId": 55,
                                "schemaId":70
                            }
                            ]
                            }
                            ],
            "proofName": "student name Pan verification",

            "proofPurpose": "for verify pan of a person",
            "proofCredFormat": "ANONCREDS"
    }
```

Detailed Breakdown:

* `"ANONCREDS"`
* Specifies that the proof must be generated using the **AnonCreds** format (based on CL-signatures, Sovrin-based).
* This limits acceptable credentials to AnonCreds-based ones (not JSON-LD or other types).

#### Predicates:

* **`requestedPredicates`**\
  This section defines the predicates, which are conditions that apply to the attributes being requested. In this case, it requests the **age** attribute to satisfy the following condition:
  * **`attributeName`: "age"\`**: The attribute being used in the predicate is "age."
  * \*\*`pType`: "<"`: This defines the predicate type, which in this case is less than (`<\`), meaning that the holder needs to provide a value for age that is less than the specified threshold.
  * **`pValue`: 0**: The condition is that the age value should be less than `0` (likely for testing or a specific use case).
  * **`proofValidTill`** and **`proofValidFrom`**: Similar to the requested attributes, these fields define the validity period for the proof that must be met for the predicate condition.
  * **`restrictions`**: Restrictions for the predicate are similar to those for attributes and are bound to the same schema and credential definitions.

#### Proof Metadata:

* **`proofName`**:\
  This field defines the name of the proof request. The proof is named `"bcovrin proof define"`, which likely corresponds to a specific framework or project (e.g., BCOVRIN).
* **`proofPurpose`**:\
  This field explains the purpose of the proof. In this case, it is `"for verify anoncreds credential"`, indicating that the proof is used for verifying an anonymized credential.
* **`proofCredFormat`**:\
  This field specifies the format of the credential used for the proof. Here, it is `"ANONCREDS"`, indicating that the proof will involve credentials issued in the ANONCREDS format, a widely used privacy-preserving credential format.

b. JSON-LD

```json
{
        "requestedAttributes": [
            {
                "attributes": [
                "familyName",
                "givenName",
                "address.streetAddress",
                "address.postalAddress"
                ],
                "proofValidTill": "2025-05-21T12:33:22.196Z",
                 "proofValidFrom": "2025-05-20T12:33:22.196Z",
                "restrictions": [
                 {
                 "schemaId": 71,
                 "credentialId":56,
                 "type": [
                    "PersonalDetail",
                    "AddressInfo"
                  ]
                 }
                ]
                }
            ],
            "requestedPredicates": [],
            "proofName": "nested json ld proof define",
        "proofPurpose": "for verify jsonld credential proof",
        "proofCredFormat": "JSONLD"
    }
    
```

**Detailed Breakdown:**&#x20;

Includes one object with:

* **`attributes`**:
  * `"familyName"` – last name of the person
  * `"givenName"` – first name of the person
  * `"address.streetAddress"` – street address (nested under `address`)
  * `"address.postalAddress"` – postal code (nested under `address`)
  * These fields are **nested**, indicating the credential structure follows a **hierarchical schema**.
* **`proofValidFrom` / `proofValidTill`**:
  * Validity period of the proof request:
    * From: **May 20, 2025**
    * To: **May 21, 2025**
  * The holder can only present this proof during this window.
* **`restrictions`**:
  * Credential must satisfy the following:
    * **`schemaId`: `71`** — The credential must conform to schema ID 71.
    * **`credentialId`: `56`** — Only a specific credential issued under this ID can be used.
    * **`type`: `[ "PersonalDetail", "AddressInfo" ]`** — The credential must be of these **types**, suggesting it uses a JSON-LD `@type` field for semantic modeling. This ensures the right class of credential is being referenced.
  * &#x20;**`requestedPredicates`: `[]`**\

    * Empty list — No predicate (e.g., age checks or greater-than/less-than rules) is being requested.
    * This is a **pure disclosure proof** (revealing the actual values of selected fields), without any ZKP-based conditions.
  * **`proofName`**\

    * `"nested json ld proof define"`
    * A descriptive label that tells the verifier and the holder what the proof is for.
    * Here, it’s to **verify nested attributes** in a **JSON-LD credential**.
  * **`proofPurpose`**
    * `"for verify jsonld credential proof"`
    * Business or legal rationale for requesting this proof.
    * It helps ensure transparency in what the verifier is trying to achieve — likely a **KYC or identity check**.
  * &#x20;**`proofCredFormat`**
    * `"JSONLD"`
    * This explicitly defines that the credential proof must follow the **JSON-LD verifiable credential** format.
    * Unlike AnonCreds, JSON-LD proofs use **linked data signatures** (like BBS+), supporting selective disclosure with context-based validation.
  *

4.  **Send Request**:

    * Click **Send**.
    * Verify the response with sample response below and check the status code to be 201 to ensure the proof request is defined successfully
    * `{ "success": true, "message": "ANONCREDS proof has been defined successfully.", "data": { "`proofDefineId`": 11 } }`



Response Body:

```json
{"success":true,"message":"ANONCREDS proof has been defined successfully.","data":{"proofDefineId":14}}
```

**Detailed Breakdown :**

`success: true`:

The `success: true` status indicates that the operation was executed successfully without any errors or exceptions.

`"ANONCREDS proof has been defined successfully."`):

This message provides a clear confirmation to the user or client that the specific action of defining an ANONCREDS proof has been successfully carried out.

`"`proofDefineId`": 11` ):

The proofDefineId is a unique identifier assigned to the newly defined ANONCREDS proof.

***

### <mark style="color:blue;">Test Scenario 2:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test sending an Out of Band Proof Request</mark>_

**Objective**: Verify that proof requests can be sent to an Out of Band Holder

**Testing Steps**:

1. **Create Request**:
   * Open Postman and create a new request.
   * Name the request "Send OOB Proof Request".
   * Set the request type to POST.
   * Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/proof/send-oob.
2. **Add Authorization**:
   * Click on the **Authorization** tab.
   * Select **API Key** from the dropdown.
   * Set the **Key** to `api-key`.
   * Set the **Value** to `{{apiKey}}`.
3. **Add Request Body**:

```json
{
                     "proofDefineId": 13,
                     "credProofId": "",
                     "recipientEmail": "verifier@getnada.com",
                     "proofAutoVerify": false,
                     "recipientName": "john"
                   }
```

* **Detailed Breakdown**\
  **I**
  * **`proofDefineId`**:
    * This is the identifier for the proof definition, which uniquely represents a specific proof request. In this case, the `proofDefineId` is `13`. This ID is used to track and reference this particular proof request in the system.
  * **`credProofId`**:
    * This field is meant to store the ID of the credential proof, but in this case, it is empty (`""`). This might indicate that the proof has not yet been generated or linked to a credential, or it could simply be a placeholder for when the credential proof is created.
  * **`recipientEmail`**:
    * The email address of the recipient (the person who will receive the proof request). In this case, the recipient’s email is `"verifier@getnada.com"`, which is where the proof request will be sent. This is an essential part of the communication process, ensuring that the correct person or entity receives the proof request.
  * **`proofAutoVerify`**:
    * This field indicates whether the proof will be automatically verified once the recipient provides it. It is set to `false`, meaning the proof will not be automatically verified. Instead, it may require manual verification or further processing before acceptance. This provides more control over the verification process, allowing for review or additional steps before finalizing the validation.
  * **`recipientName`**:
    * This represents the name of the recipient who is to receive the proof request. Here, the recipient's name is `"john"`. This is typically used for personalization in the request or to identify the individual associated with the provided email.

4. **Send Request**:

* Click **Send**.
* Verify the response with sample response below and check the status code to be 201 to ensure the proof request is defined successfully

Response Body

```json
{
  "success": true,
  "message": "out-of-band proof request send successfully.",
  "data": {
    "credProofId": "58e02d58-a762-469e-84ba-882a47345775",
    "proofDefineId": 1,
    "proofStatus": "request-sent"
  }
}
```

**Detailed Breakdown**&#x20;

* **`success`**:
  * This field indicates the success status of the operation. The value `true` confirms that the out-of-band proof request was sent successfully.
* **`message`**:
  * This is a message providing more context about the operation. In this case, the message `"out-of-band proof request send successfully."` confirms that the proof request was successfully initiated and sent.
* **`data`**:
  * The `data` field contains additional details about the proof request that was sent. It includes:
  * **`credProofId`**:
    * This is the unique identifier for the credential proof associated with the request. In this case, the `credProofId` is `"58e02d58-a762-469e-84ba-882a47345775"`. This ID will be used to reference the specific credential proof within the system.
  * **`proofDefineId`**:
    * This represents the ID of the proof definition associated with the proof request. In this case, the `proofDefineId` is `1`, which uniquely identifies the type or template of proof request that has been sent.
  * **`proofStatus`**:
    * This field indicates the current status of the proof request. The value `"request-sent"` confirms that the proof request has been successfully sent, but the process is ongoing, and the request may still await further actions, such as receiving or verifying the proof.



***

### <mark style="color:blue;">Test Scenario 3:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test the generation of a Proof Request URL</mark>_

**Objective**: Verify that proof request URL codes can be generated

**Testing Steps:**

1. **Create Request**:
   * Open Postman and create a new request.
   * Name the request "Prepare Proof Request URL".
   * Set the request type to POST.
   * Set the URL to `{{baseUrl}}/api/lob/{{lob_id}}/proof/url`\

2. **Add Authorization**:
   * Click on the **Authorization** tab.
   * Select **API Key** from the dropdown.
   * Set the **Key** to `api-key`.
   * Set the **Value** to `{{apiKey}}`.\

3. **Add Request Body**:

```
{
                     "proofDefineId": 13,
                     "credProofId": "",
                     "messageProtocol": "AIP2_0",
                     "proofAutoVerify": false     
                   }
```

Detailed Breakdown

* **`proofDefineId`**:
  * This is the identifier for the proof definition. In this case, the `proofDefineId` is `13`, indicating the specific template or configuration of the proof request.
* **`credProofId`**:
  * This field is intended to hold the unique identifier for the credential proof associated with the request. However, in this case, the `credProofId` is an empty string (`""`), which suggests that no proof has been generated or linked yet.
* **`messageProtocol`**:
  * This field specifies the message protocol used for the proof request. In this case, the value `"AIP2_0"` refers to a specific version of the protocol (AIP 2.0). AIP (Aries Interoperability Protocol) defines how credentials and proofs are exchanged between agents in a secure and standardized manner.
* **`proofAutoVerify`**:
  * This boolean field indicates whether the proof should be automatically verified upon submission. The value `false` suggests that the proof will not be automatically verified, and manual verification will likely be required.



1.  **Send Request**:

    * Click **Send**.
    * Verify the response with sample response below and check the status code to be 201 to ensure the proof request is defined successfully
    * `{ "success": true, "message": "prepare qr proof request proceed successfully.", "data": { "`proofDefineId`": 13, "longUrl": "http://100.28.204.79:9007?oob=eyJAdHlwZSI6ICJodHRwczovL2RpZGNvbW0ub3JnL291dC1vZi1iYW5kLzEuMS9pbnZpdGF0aW9uIiwgIkBpZCI6ICJhYjYxN2Y1ZS1kOGE1LTRkMTgtYTA5YS0xNWFkOGNiOGZkYTkiLCAibGFiZWwiOiAiTmV3VGVzdDcgQWdlbnQiLCAiaGFuZHNoYWtlX3Byb3RvY29scyI6IFtdLCAicmVxdWVzdHN-YXR0YWNoIjogW3siQGlkIjogInJlcXVlc3QtMCIsICJtaW1lLXR5cGUiOiAiYXBwbGljYXRpb24vanNvbiIsICJkYXRhIjogeyJqc29uIjogeyJAdHlwZSI6ICJodHRwczovL2RpZGNvbW0ub3JnL3ByZXNlbnQtcHJvb2YvMi4wL3JlcXVlc3QtcHJlc2VudGF0aW9uIiwgIkBpZCI6ICI4NDA0YmNjYy03MDQzLTQ0NzYtYWY3OS00NGI3OGRjM2YxZTMiLCAifnRocmVhZCI6IHsicHRoaWQiOiAiYWI2MTdmNWUtZDhhNS00ZDE4LWEwOWEtMTVhZDhjYjhmZGE5In0sICJjb21tZW50IjogImZvciB2ZXJpZnkgYW5vbmNyZWQgY3JlZGVudGlhbCIsICJ3aWxsX2NvbmZpcm0iOiB0cnVlLCAiZm9ybWF0cyI6IFt7ImF0dGFjaF9pZCI6ICJpbmR5IiwgImZvcm1hdCI6ICJobGluZHkvcHJvb2YtcmVxQHYyLjAifV0sICJyZXF1ZXN0X3ByZXNlbnRhdGlvbnN-YXR0YWNoIjogW3siQGlkIjogImluZHkiLCAibWltZS10eXBlIjogImFwcGxpY2F0aW9uL2pzb24iLCAiZGF0YSI6IHsiYmFzZTY0IjogImV5SnVZVzFsSWpvZ0ltSmpiM1p5YVc0Z2NISnZiMllnWkdWbWFXNWxJaXdnSW01dmJtTmxJam9nSWpFaUxDQWljbVZ4ZFdWemRHVmtYMkYwZEhKcFluVjBaWE1pT2lCN0ltRmtaR2wwYVc5dVlXeFFjbTl3TVNJNklIc2ljbVZ6ZEhKcFkzUnBiMjV6SWpvZ1czc2lZM0psWkY5a1pXWmZhV1FpT2lBaVRqaEVSbkZyTjNkMlUyUmtObGhIUm1GeVIzQTFXRG96T2tOTU9qRTNORFUxTlRjNlJISnBkbWx1WjE5TWFXTmxibk5sWHpFaUxDQWlhWE56ZFdWeVgyUnBaQ0k2SUNKT09FUkdjV3MzZDNaVFpHUTJXRWRHWVhKSGNEVllJaXdnSW5OamFHVnRZVjlwWkNJNklDSk9PRVJHY1dzM2QzWlRaR1EyV0VkR1lYSkhjRFZZT2pJNlJISnBkbWx1WjE5c2FXTmxibk5sT2pJdU1DSXNJQ0p6WTJobGJXRmZhWE56ZFdWeVgyUnBaQ0k2SUNKT09FUkdjV3MzZDNaVFpHUTJXRWRHWVhKSGNEVllJaXdnSW5OamFHVnRZVjl1WVcxbElqb2dJa1J5YVhacGJtZGZiR2xqWlc1elpTSXNJQ0p6WTJobGJXRmZkbVZ5YzJsdmJpSTZJQ0l5TGpBaWZWMHNJQ0p1YjI1ZmNtVjJiMnRsWkNJNklIc2lkRzhpT2lBeE56STFNREk1TWprMmZTd2dJbTVoYldWeklqb2dXeUptZFd4c1gyNWhiV1VpWFgxOUxDQWljbVZ4ZFdWemRHVmtYM0J5WldScFkyRjBaWE1pT2lCN2ZTd2dJblpsY25OcGIyNGlPaUFpTVM0d0luMD0ifX1dfX19XSwgInNlcnZpY2VzIjogW3siaWQiOiAiI2lubGluZSIsICJ0eXBlIjogImRpZC1jb21tdW5pY2F0aW9uIiwgInJlY2lwaWVudEtleXMiOiBbImRpZDprZXk6ejZNa25idTZjTHBqZDhvaVFEaE5hblNVdXdFc3JrZUw5NjRUeXFBS1JYYzJIbVEyI3o2TWtuYnU2Y0xwamQ4b2lRRGhOYW5TVXV3RXNya2VMOTY0VHlxQUtSWGMySG1RMiJdLCAic2VydmljZUVuZHBvaW50IjogImh0dHA6Ly8xMDAuMjguMjA0Ljc5OjkwMDcifV19", "shortUrl": "https://devapi-verifier.nborbit.ca/url/7c204a3f-28ed-4656-8eda-7be899c26b56" } }`

    **Detailed Breakdown :**

    `success: true:`\
    The `success: true` status indicates that the operation was executed successfully without any errors or exceptions.

    `"prepare qr proof request proceed successfully."`:\
    This message confirms to the user or client that the specific action of preparing a QR proof request has been successfully completed.

    `"`proofDefineId`": 13`:\
    The proofDefineId is a unique identifier assigned to the newly created QR proof request. This ID can be used to reference the specific proof request in future operations, such as querying or validating the proof.

    `"longUrl": "http://100.28.204.79:9007?oob=eyJAdHlwZSI6ICJodHRwczovL2RpZGNvbW0ub3JnL291dC1vZi1iYW5kLzEuMS9pbnZpdGF0aW9uIiwgIkBpZCI6ICJhYjYxN2Y1ZS1kOGE1LTRkMTgtYTA5YS0xNWFkOGNiOGZkYTkiLCAibGFiZWwiOiAiTmV3VGVzdDcgQWdlbnQiLCAiaGFuZHNoYWtlX3Byb3RvY29scyI6IFtdLCAicmVxdWVzdHN-YXR0YWNoIjogW3siQGlkIjogInJlcXVlc3QtMCIsICJtaW1lLXR5cGUiOiAiYXBwbGljYXRpb24vanNvbiIsICJkYXRhIjogeyJqc29uIjogeyJAdHlwZSI6ICJodHRwczovL2RpZGNvbW0ub3JnL3ByZXNlbnQtcHJvb2YvMi4wL3JlcXVlc3QtcHJlc2VudGF0aW9uIiwgIkBpZCI6ICI4NDA0YmNjYy03MDQzLTQ0NzYtYWY3OS00NGI3OGRjM2YxZTMiLCAifnRocmVhZCI6IHsicHRoaWQiOiAiYWI2MTdmNWUtZDhhNS00ZDE4LWEwOWEtMTVhZDhjYjhmZGE5In0sICJjb21tZW50IjogImZvciB2ZXJpZnkgYW5vbmNyZWQgY3JlZGVudGlhbCIsICJ3aWxsX2NvbmZpcm0iOiB0cnVlLCAiZm9ybWF0cyI6IFt7ImF0dGFjaF9pZCI6ICJpbmR5IiwgImZvcm1hdCI6ICJobGluZHkvcHJvb2YtcmVxQHYyLjAifV0sICJyZXF1ZXN0X3ByZXNlbnRhdGlvbnN-YXR0YWNoIjogW3siQGlkIjogImluZHkiLCAibWltZS10eXBlIjogImFwcGxpY2F0aW9uL2pzb24iLCAiZGF0YSI6IHsiYmFzZTY0IjogImV5SnVZVzFsSWpvZ0ltSmpiM1p5YVc0Z2NISnZiMllnWkdWbWFXNWxJaXdnSW01dmJtTmxJam9nSWpFaUxDQWljbVZ4ZFdWemRHVmtYMkYwZEhKcFluVjBaWE1pT2lCN0ltRmtaR2wwYVc5dVlXeFFjbTl3TVNJNklIc2ljbVZ6ZEhKcFkzUnBiMjV6SWpvZ1czc2lZM0psWkY5a1pXWmZhV1FpT2lBaVRqaEVSbkZyTjNkMlUyUmtObGhIUm1GeVIzQTFXRG96T2tOTU9qRTNORFUxTlRjNlJISnBkbWx1WjE5TWFXTmxibk5sWHpFaUxDQWlhWE56ZFdWeVgyUnBaQ0k2SUNKT09FUkdjV3MzZDNaVFpHUTJXRWRHWVhKSGNEVllJaXdnSW5OamFHVnRZVjlwWkNJNklDSk9PRVJHY1dzM2QzWlRaR1EyV0VkR1lYSkhjRFZZT2pJNlJISnBkbWx1WjE5c2FXTmxibk5sT2pJdU1DSXNJQ0p6WTJobGJXRmZhWE56ZFdWeVgyUnBaQ0k2SUNKT09FUkdjV3MzZDNaVFpHUTJXRWRHWVhKSGNEVllJaXdnSW5OamFHVnRZVjl1WVcxbElqb2dJa1J5YVhacGJtZGZiR2xqWlc1elpTSXNJQ0p6WTJobGJXRmZkbVZ5YzJsdmJpSTZJQ0l5TGpBaWZWMHNJQ0p1YjI1ZmNtVjJiMnRsWkNJNklIc2lkRzhpT2lBeE56STFNREk1TWprMmZTd2dJbTVoYldWeklqb2dXeUptZFd4c1gyNWhiV1VpWFgxOUxDQWljbVZ4ZFdWemRHVmtYM0J5WldScFkyRjBaWE1pT2lCN2ZTd2dJblpsY25OcGIyNGlPaUFpTVM0d0luMD0ifX1dfX19XSwgInNlcnZpY2VzIjogW3siaWQiOiAiI2lubGluZSIsICJ0eXBlIjogImRpZC1jb21tdW5pY2F0aW9uIiwgInJlY2lwaWVudEtleXMiOiBbImRpZDprZXk6ejZNa25idTZjTHBqZDhvaVFEaE5hblNVdXdFc3JrZUw5NjRUeXFBS1JYYzJIbVEyI3o2TWtuYnU2Y0xwamQ4b2lRRGhOYW5TVXV3RXNya2VMOTY0VHlxQUtSWGMySG1RMiJdLCAic2VydmljZUVuZHBvaW50IjogImh0dHA6Ly8xMDAuMjguMjA0Ljc5OjkwMDcifV19"`:

    \
    The `longUrl` is a complete and detailed URL generated for the QR proof request. This URL is used to represent the proof request in a way that can be scanned via QR code or accessed directly by a client. It includes encoded data (`oob` parameter) necessary for the request to be processed. This URL may be useful for direct sharing or embedding in a QR code.

    `"shortUrl": "https://devapi-verifier.nborbit.ca/url/7c204a3f-28ed-4656-8eda-7be899c26b56"`:

    \
    The `shortUrl` is a condensed version of the `longUrl`, making it easier to share or use in contexts where a shorter URL is preferable. This shortened URL redirects to the same resource as the `longUrl`, simplifying its use in digital communication or QR code generation.



***

### <mark style="color:blue;">Test Scenario 4:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test sending a proof request to a contact</mark>_

**Objective**: Verify that proof requests can be sent to a Holder that is a contact

**Testing Steps:**

1. **Create Request**:
   * Open Postman and create a new request.
   * Name the request "Send Proof Request to Contact".
   * Set the request type to POST.
   * Set the URL to `{{baseUrl}}/api/lob/{{lob_id}}/proof/send-contact`\

2. **Add Authorization**:
   * Click on the **Authorization** tab.
   * Select **API Key** from the dropdown.
   * Set the **Key** to `api-key`.
   * Set the **Value** to `{{apiKey}}`.\

3. **Add Request Body**:

```json
{
                    "comment": "send proof request to holder",
                     "proofDefineId": 12,
                     "contactId": "bdcbf5ec-79f5-43b2-a49f-d98ea8f35b7a",
                     "credProofId": "",
                     "proofAutoVerify": false
                   }
```

&#x20;Detailed Breakdown

* **`comment`**:
  * This field provides additional context or information about the proof request. The value `"send proof request to holder"` indicates the purpose of this request is to send a proof to the holder, likely part of a larger verification process.
* **`proofDefineId`**:
  * This is the identifier of the proof definition template. The value `12` signifies the specific proof template that is being used in this case.
* **`contactId`**:
  * This is a unique identifier (`bdcbf5ec-79f5-43b2-a49f-d98ea8f35b7a`) that links the proof request to a specific contact. This ID helps identify the recipient (in this case, the holder) within the system.
* **`credProofId`**:
  * This field is intended to hold the unique identifier for the credential proof. It is currently an empty string (`""`), indicating that no proof has been generated or associated with this request yet.
* **`proofAutoVerify`**:
  * This boolean flag determines if the proof will be automatically verified upon submission. The value `false` means that the proof will not be automatically verified, and manual verification is likely required.

\


1.  **Send Request**:

    * Click **Send**.
    * Verify the response with sample response below and check the status code to be 201 to ensure the proof request is defined successfully

    `Response Body`

```json
{"success":true,"message":"proof request sended successfully.","data":{"proofDefineId":1019,"credProofId":"8b63b96d-5de1-4b72-aed6-13d749740443","proofStatus":"request-sent"}}
```

**Detailed Breakdown**&#x20;

* **`success`**:
  * The value `true` indicates that the operation was successful. The proof request has been sent successfully.
* **`message`**:
  * This field provides a descriptive message about the operation. The value `"proof request sended successfully."` confirms that the proof request has been sent without issues.
* **`data`**:
  * This object contains the actual data related to the proof request.
  * **`proofDefineId`**:
    * This field contains the identifier (`1019`) for the proof definition used to create this proof request. It links the request to a specific proof template.
  * **`credProofId`**:
    * The `credProofId` (`8b63b96d-5de1-4b72-aed6-13d749740443`) is the unique identifier for the credential proof that is being requested. This ID can be used to track and manage the proof request throughout its lifecycle.
  * **`proofStatus`**:
    * The `proofStatus` field (`request-sent`) indicates the current status of the proof request. In this case, it shows that the proof request has been sent and is awaiting further processing (such as verification or response).

***

### <mark style="color:blue;">Test Scenario 5:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test retrieving all proof requests</mark>_

**Objective**: Verify that all proof requests can be retrieved

**Testing Steps:**

1. **Create Request**:
   * Open Postman and create a new request.
   * Name the request "Get All Proof Requests".
   * Set the request type to GET.
   * Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/proof-requests\

2. **Add Authorization**:
   * Click on the **Authorization** tab.
   * Select **API Key** from the dropdown.
   * Set the **Key** to `api-key`.
   * Set the **Value** to `{{apiKey}}`.\

3.  **Send Request**:

    * Click **Send**.
    * Verify the response with sample response below and check the status code to be 200 to ensure the proof request is defined successfully

    **Response Body:**&#x20;

{% code overflow="wrap" %}
```json
{"success":true,"message":"proof request fetch successfully.","data":{"items":[{"credProofId":"8b63b96d-5de1-4b72-aed6-13d749740443","proofStatus":"request-sent","proofAutoVerify":false,"authorityStatement":null},{"credProofId":"5a5516a5-371b-456d-b3af-52114cbf0fa8","proofStatus":"request-sent","proofAutoVerify":false,"authorityStatement":null},{"credProofId":"3dc2338a-0f6d-46a5-82fe-78e7036552d1","proofStatus":"request-sent","proofAutoVerify":false,"authorityStatement":null},{"credProofId":"38b0eb95-5608-4046-a648-a1831ed7bb93","proofStatus":"done","proofAutoVerify":false,"authorityStatement":null,"verified":true},{"credProofId":"06268611-8f76-4e8e-b45a-cfb241f6ba96","proofStatus":"done","proofAutoVerify":false,"authorityStatement":null,"verified":true},{"credProofId":"d76d3bda-6f77-4a76-b42d-2f2350be3c4d","proofStatus":"abandoned","proofAutoVerify":false,"authorityStatement":null},{"credProofId":"6d674528-70ac-4a72-93e4-468c2fb73852","proofStatus":"done","proofAutoVerify":false,"authorityStatement":null,"verified":true},{"credProofId":"cd4bd563-9078-4989-9134-cf90d47dea71","proofStatus":"request-sent","proofAutoVerify":false,"authorityStatement":null},{"credProofId":"8f48580d-4f48-4d48-ab6c-06d7dbad99d0","proofStatus":"request-sent","proofAutoVerify":false,"authorityStatement":null},{"credProofId":"a2db6164-4c63-4b49-b2a2-350d4f52ae0f","proofStatus":"request-sent","proofAutoVerify":false,"authorityStatement":null}],"meta":{"totalItems":35,"itemCount":10,"itemsPerPage":10,"totalPages":4,"currentPage":1}}}
```
{% endcode %}

**Detailed Breakdown**&#x20;

* **`success`**:
  * The value `true` indicates that the operation was successful. The proof requests were fetched without any issues.
* **`message`**:
  * This field provides a descriptive message about the operation. The value `"proof request fetch successfully."` confirms that the proof requests were retrieved successfully.
* **`data`**:
  * This object contains the actual data related to the fetched proof requests.
  * **`items`**:
    * This array contains the list of proof requests fetched. Each item in the array represents a specific proof request with the following fields:
      * **`credProofId`**:
        * This field contains the unique identifier for the credential proof request. Each `credProofId` corresponds to a specific proof request. For example, `"8b63b96d-5de1-4b72-aed6-13d749740443"` is one such ID.
      * **`proofStatus`**:
        * This field indicates the current status of the proof request. The possible statuses include:
          * `"request-sent"`: The proof request has been sent, but no further action has occurred.
          * `"done"`: The proof request has been completed (usually after the proof was verified).
          * `"abandoned"`: The proof request was abandoned and is no longer in progress.
      * **`proofAutoVerify`**:
        * This field indicates whether the proof request is set for automatic verification. In this case, it is set to `false` for all requests, meaning the verification process will not be automatic.
      * **`authorityStatement`**:
        * This field contains any authority statement associated with the proof request. All the values are `null`, indicating no authority statements are provided for these requests.
      * **`verified`**:
        * This field indicates whether the proof request was successfully verified. For example, some requests have `"verified": true`, indicating the proof for those requests has been validated, while others don't have this field, implying the verification process has not yet occurred.
  * **`meta`**:
    * This object contains metadata about the pagination of the fetched proof requests.
      * **`totalItems`**: The total number of proof requests available (in this case, `35`).
      * **`itemCount`**: The number of proof requests returned in this response (here, `10`).
      * **`itemsPerPage`**: The number of items that can be displayed per page (here, `10`).
      * **`totalPages`**: The total number of pages available (here, `4`).
      * **`currentPage`**: The current page number (here, `1`).



***

### <mark style="color:blue;">Test Scenario 6:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test retrieving a specific proof request using a Proof ID</mark>_

**Objective**: Verify that a specific proof request, based on Proof ID, can be retrieved

**Variables**:

* `proofId`: Set this to a valid proof request ID.

**Testing Steps**:

1. **Create Request**:
   * Open Postman and create a new request.
   * Name the request "Get Proof Request by ID".
   * Set the request type to GET.
   *   Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/proof-request/{cred\_proof\_id}.

       \

2. **Add Authorization**:
   * Click on the **Authorization** tab.
   * Select **API Key** from the dropdown.
   * Set the **Key** to `api-key`.
   * Set the **Value** to `{{apiKey}}`.\

3.  **Send Request**:

    Click **Send**.

    Verify the response with sample response below and check the status code to be 200 to ensure the proof request is defined successfully

Response Body

```json
{"success":true,"message":"proof request fetch successfully.","data":{"items":[{"credProofId":"8b63b96d-5de1-4b72-aed6-13d749740443","proofStatus":"request-sent","proofAutoVerify":false,"authorityStatement":null},{"credProofId":"5a5516a5-371b-456d-b3af-52114cbf0fa8","proofStatus":"request-sent","proofAutoVerify":false,"authorityStatement":null},{"credProofId":"3dc2338a-0f6d-46a5-82fe-78e7036552d1","proofStatus":"request-sent","proofAutoVerify":false,"authorityStatement":null},{"credProofId":"38b0eb95-5608-4046-a648-a1831ed7bb93","proofStatus":"done","proofAutoVerify":false,"authorityStatement":null,"verified":true},{"credProofId":"06268611-8f76-4e8e-b45a-cfb241f6ba96","proofStatus":"done","proofAutoVerify":false,"authorityStatement":null,"verified":true},{"credProofId":"d76d3bda-6f77-4a76-b42d-2f2350be3c4d","proofStatus":"abandoned","proofAutoVerify":false,"authorityStatement":null},{"credProofId":"6d674528-70ac-4a72-93e4-468c2fb73852","proofStatus":"done","proofAutoVerify":false,"authorityStatement":null,"verified":true},{"credProofId":"cd4bd563-9078-4989-9134-cf90d47dea71","proofStatus":"request-sent","proofAutoVerify":false,"authorityStatement":null},{"credProofId":"8f48580d-4f48-4d48-ab6c-06d7dbad99d0","proofStatus":"request-sent","proofAutoVerify":false,"authorityStatement":null},{"credProofId":"a2db6164-4c63-4b49-b2a2-350d4f52ae0f","proofStatus":"request-sent","proofAutoVerify":false,"authorityStatement":null}],"meta":{"totalItems":35,"itemCount":10,"itemsPerPage":10,"totalPages":4,"currentPage":1}}}
```

**Detailed Breakdown:**

* **`success`**:
  * The value `true` indicates the operation was successful, meaning the proof requests were successfully fetched.
* **`message`**:
  * The message `"proof request fetch successfully."` confirms that the operation completed successfully, indicating that the proof requests were retrieved without any issues.
* **`data`**:
  * This object contains the data related to the fetched proof requests.
  * **`items`**:
    * This array holds a list of proof requests. Each object in this array represents a unique proof request with the following details:
      * **`credProofId`**:
        * This is the unique identifier for the proof request. For example, `"8b63b96d-5de1-4b72-aed6-13d749740443"` represents one such ID.
      * **`proofStatus`**:
        * Indicates the current status of the proof request. The possible statuses include:
          * `"request-sent"`: The proof request has been sent, but no further action has taken place.
          * `"done"`: The proof request has been completed (usually after the proof has been verified).
          * `"abandoned"`: The proof request was abandoned and is no longer being processed.
      * **`proofAutoVerify`**:
        * Indicates whether the proof request is set for automatic verification. For all the items, it is set to `false`, meaning that the verification process will not be automatic and must be manually handled.
      * **`authorityStatement`**:
        * This field holds any authority statement associated with the proof request. In this case, the value is `null` for all requests, indicating no authority statement is provided.
      * **`verified`**:
        * This field is only present for some requests. It indicates whether the proof has been successfully verified. For example, `"verified": true` for the proof request with `credProofId` `"38b0eb95-5608-4046-a648-a1831ed7bb93"`, which means that this proof has been verified.
  * **`meta`**:
    * This object contains metadata related to the pagination of the proof requests:
      * **`totalItems`**: The total number of proof requests available in the system (here, `35`).
      * **`itemCount`**: The number of proof requests returned in this response (in this case, `10`).
      * **`itemsPerPage`**: The number of items to be displayed per page (here, `10`).
      * **`totalPages`**: The total number of pages available based on the current pagination configuration (here, `4`).
      * **`currentPage`**: The current page number being displayed (here, `1`).

&#x20;

&#x20;



***

### <mark style="color:blue;">Test Scenario 7:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test deleting a specific proof request using a Proof ID</mark>_

**Objective**: Verify that a specific proof request, based on Proof ID, can be deleted

**Variables**:

&#x20;    credProofId:Set this to a valid proof request ID.

* **Testing Steps**:

1. **Create Request**:
   * Open Postman and create a new request.
   * Name the request "Delete Proof Request by ID".
   * Set the request type to DELETE.
   *   Set the URL to `{{baseUrl}}/api/lob/{{lob_id}}/proof-request`.

       \

2. **Add Authorization**:
   * Click on the **Authorization** tab.
   * Select **API Key** from the dropdown.
   * Set the **Key** to `api-key`.
   * Set the **Value** to `{{apiKey}}`.\

3. **Add Request Body**:

```
{
  "credProofId": "58e02d58-a762-469e-84ba-882a47345775"
}

```

1.  **Send Request**:

    * Click **Send**.
    * Verify the response with sample response below and check the status code to be 200 to ensure the proof request is defined successfully
    * `{ "success": true, "message": "Proof request proceed successfully.", "data": { "responseDetails": "Proof request with id '5' has been deleted successfully." } }`&#x20;


2. **Response Body**

{% code overflow="wrap" %}
```json
{"success":true,"message":"Proof request proceed successfully.","data":{"responseDetails":"Proof request with id '8b63b96d-5de1-4b72-aed6-13d749740443' has been deleted successfully.","proofDefineId":1019,"credProofId":"8b63b96d-5de1-4b72-aed6-13d749740443","proofStatus":"deleted"}}
```
{% endcode %}

1. **Detailed Breakdown :**

* **`success`**:
  * The value `true` indicates the operation was successful, meaning the proof request has been processed and deleted without any issues.
* **`message`**:
  * The message `"Proof request proceed successfully."` confirms that the proof request was handled successfully, including the deletion.
* **`data`**:
  * This object contains the data related to the proof request that was deleted.
  * **`responseDetails`**:
    * This provides a detailed message about the operation. The message `"Proof request with id '8b63b96d-5de1-4b72-aed6-13d749740443' has been deleted successfully."` indicates that the proof request with the specified `credProofId` was deleted successfully.
  * **`proofDefineId`**:
    * This is the unique identifier for the proof definition associated with the proof request. The value is `1019`, which corresponds to the proof definition under which the proof request was created.
  * **`credProofId`**:
    * This is the unique identifier for the proof request. The value `"8b63b96d-5de1-4b72-aed6-13d749740443"` corresponds to the proof request that has been deleted.
  * **`proofStatus`**:
    * The value `"deleted"` indicates that the proof request has been deleted successfully and is no longer available for processing.

####

&#x20;







***

### <mark style="color:blue;">Test Scenario 8:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to retrieve all defined proof requests</mark>_

**Objective**: Verify that all proof requests can be retrieved

**Testing Steps**:

1. **Create Request**:
   * Open Postman and create a new request.
   * Name the request "Get Defined Proof Requests".
   * Set the request type to GET.
   *   Set the URL to `{{baseUrl}}/api/lob/{{lob_id}}/define-proof-request`.

       \

2. **Add Authorization**:
   * Click on the **Authorization** tab.
   * Select **API Key** from the dropdown.
   * Set the **Key** to `api-key`.
   * Set the **Value** to `{{apiKey}}`.\

3.  **Send Request**:

    * Click **Send**.
    * Verify the response with sample response below and check the status code to be 200 to ensure the proof request is defined successfully
    * `Response Body`&#x20;



```json
{
  "success": true,
  "message": "define proof-request fetch successfully",
  "data": {
    "items": [
      {
        "proofDefineId": 1,
        "name": "bcovrin proof define",
        "attributes": {
          "attributes": [
            "full_name",
            "email_address"
          ],
          "proofValidTill": "2025-04-15T10:57:50.022Z",
          "proofValidFrom": "2025-04-15T10:57:50.026Z",
          "restrictions": [
            {
              "anoncredsSchemaId": "WgWxqztrNooG92RXvxSTWv:2:schema_name:1.0",
              "anoncredsSchemaIssuerDid": "WgWxqztrNooG92RXvxSTWv",
              "anoncredsSchemaName": "schema_name",
              "anoncredsSchemaVersion": "1.0",
              "anoncredsIssuerDid": "WgWxqztrNooG92RXvxSTWv",
              "anoncredsCredDefId": "WgWxqztrNooG92RXvxSTWv:3:CL:20:tag",
              "jsonldContextUrl": "https://w3id.org/citizenship/v1"
            }
          ]
        },
        "predicates": {
          "attributeName": "age",
          "pType": "<",
          "pValue": 0,
          "proofValidTill": "2025-04-15T10:57:50.027Z",
          "proofValidFrom": "2025-04-15T10:57:50.027Z",
          "restrictions": [
            {
              "anoncredsSchemaId": "WgWxqztrNooG92RXvxSTWv:2:schema_name:1.0",
              "anoncredsSchemaIssuerDid": "WgWxqztrNooG92RXvxSTWv",
              "anoncredsSchemaName": "schema_name",
              "anoncredsSchemaVersion": "1.0",
              "anoncredsIssuerDid": "WgWxqztrNooG92RXvxSTWv",
              "anoncredsCredDefId": "WgWxqztrNooG92RXvxSTWv:3:CL:20:tag"
            }
          ]
        },
        "proofType": "ANONCREDS",
        "purpose": "for verify anoncreds credential",
        "createdAt": "2024-07-19T11:55:33.799Z",
        "updatedAt": "2024-07-19T11:55:33.799Z"
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

1. **Detailed Breakdown :**

* **`success`**:
  * The value `true` indicates that the operation to fetch the proof request definitions was successful.
* **`message`**:
  * The message `"define proof-request fetch successfully"` confirms that the proof request definition data has been successfully retrieved.
* **`data`**:
  * This object contains the main data related to the fetched proof request definitions.
  * **`items`**:
    * This is an array containing the details of each proof request definition retrieved. In this case, it contains one proof request definition.
    * **`proofDefineId`**:
      * The unique identifier for the proof request definition. In this case, the value is `1`.
    * **`name`**:
      * This is the name of the proof request definition. In this case, the name is `"bcovrin proof define"`.
    * **`attributes`**:
      * This object contains the attributes required for the proof request.
      * **`attributes`**:
        * This is an array of attributes that are requested in the proof request. Here, the attributes are `"full_name"` and `"email_address"`.
      * **`proofValidTill`**:
        * The expiration date for the proof request validity, which is `"2025-04-15T10:57:50.022Z"`. This indicates when the proof request becomes invalid.
      * **`proofValidFrom`**:
        * The date from which the proof request is valid, which is `"2025-04-15T10:57:50.026Z"`.
      * **`restrictions`**:
        * This is an array of restrictions applied to the proof request. It contains information about the schema and credential definition used.
        * **`anoncredsSchemaId`**:
          * The schema identifier for the credential. In this case, `"WgWxqztrNooG92RXvxSTWv:2:schema_name:1.0"`.
        * **`anoncredsSchemaIssuerDid`**:
          * The issuer's DID (Decentralized Identifier) associated with the schema. Here, it is `"WgWxqztrNooG92RXvxSTWv"`.
        * **`anoncredsSchemaName`**:
          * The name of the schema, which is `"schema_name"`.
        * **`anoncredsSchemaVersion`**:
          * The version of the schema, `"1.0"`.
        * **`anoncredsIssuerDid`**:
          * The DID of the issuer for the credentials, `"WgWxqztrNooG92RXvxSTWv"`.
        * **`anoncredsCredDefId`**:
          * The credential definition ID for the credential, `"WgWxqztrNooG92RXvxSTWv:3:CL:20:tag"`.
        * **`jsonldContextUrl`**:
          * The URL for the JSON-LD context used, `"https://w3id.org/citizenship/v1"`.
    * **`predicates`**:
      * This object contains predicates associated with the proof request.
      * **`attributeName`**:
        * This is the name of the attribute involved in the predicate. Here, the attribute is `"age"`.
      * **`pType`**:
        * The predicate type, which is `" < "` (less than), meaning that the proof must satisfy a condition where the value of the attribute is less than a specific value.
      * **`pValue`**:
        * The value used for the predicate comparison. Here, it is `0`.
      * **`proofValidTill`**:
        * The expiration date for the predicate validity, which is `"2025-04-15T10:57:50.027Z"`.
      * **`proofValidFrom`**:
        * The start date for the predicate validity, which is `"2025-04-15T10:57:50.027Z"`.
      * **`restrictions`**:
        * The same restrictions are applied to the predicate as the ones for the attributes.
    * **`proofType`**:
      * The type of proof being defined. In this case, the value is `"ANONCREDS"`, indicating the proof uses anonymous credentials.
    * **`purpose`**:
      * This describes the purpose of the proof request. Here, the purpose is `"for verify anoncreds credential"`, indicating that the proof request is meant to verify anonymous credentials.
    * **`createdAt`**:
      * The timestamp of when the proof request definition was created. In this case, it was created on `"2024-07-19T11:55:33.799Z"`.
    * **`updatedAt`**:
      * The timestamp of when the proof request definition was last updated. It was last updated on `"2024-07-19T11:55:33.799Z"`.
* **`meta`**:
  * This object provides pagination information about the retrieved data.
  * **`totalItems`**:
    * The total number of proof request definitions available, which is `100`.
  * **`itemCount`**:
    * The number of items returned in the current page, which is `10`.
  * **`itemsPerPage`**:
    * The number of items displayed per page, which is `10`.
  * **`totalPages`**:
    * The total number of pages available, which is `10`.
  * **`currentPage`**:
    * The current page being viewed, which is `1`.











***

### <mark style="color:blue;">Test Scenario 9:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to verify the proof presentation received</mark>_

### **Objective**: Verify the proof  presentation received&#x20;

**Testing Steps**:

1. **Create Request**:
   * Open Postman and create a new request.
   * Name the request "Verify Proof presentation".
   * Set the request type to POST.
   *   Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/proof/verify.

       \

2. **Add Authorization**:
   * Click on the **Authorization** tab.
   * Select **API Key** from the dropdown.
   * Set the **Key** to `api-key`.
   * Set the **Value** to `{{apiKey}}`.\

3. Request Body&#x20;

```
{
  "credProofId": "58e02d58-a762-469e-84ba-882a47345775",
  "createClaim": false
}
```

1. **Detailed Breakdown**
2.
   * **`credProofId`**:
     * The unique identifier for the proof request. In this case, it is `"58e02d58-a762-469e-84ba-882a47345775"`. This ID is used to refer to a specific proof request in the system.
   * **`createClaim`**:
     * A boolean flag indicating whether a claim should be created for this proof request. Here, the value is `false`, meaning that no claim will be created for this proof request.
3. **Send Request**:
   * Click **Send**.
   * Verify the response with sample response below and check the status code to be 201 to ensure the proof request is defined successfully
4. Response Body

```

{
  "success": true,
  "message": "Proof request verified successfully.",
  "data": {
    "status": "success",
    "data": {
      "credProofId": "58e02d58-a762-469e-84ba-882a47345775",
      "updatedAt": "2024-11-25T12:34:56Z",
      "createdAt": "2024-11-25T12:34:56Z",
      "proofStatus": "done",
      "proofAutoVerify": true,
      "comment": "Proof successfully verified.",
      "contactId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "verified": true,
      "errorMsg": "abandoned"
    },
    "proofAttributes": {
      "HiNg6sdwNYwPRTTP9VkwpT:3:CL:2535708:Aadhar_card": [
        {
          "credentialName": "HiNg6sdwNYwPRTTP9VkwpT:3:CL:2545708:Aadhar_card",
          "attributes": [
            {
              "full_name": "John Doe"
            }
          ]
        }
      ]
    }
```

&#x20;Detailed Breakdown

* **`success`**:
  * Indicates the overall status of the operation. Here, it is `true`, meaning the proof request has been successfully processed.
* **`message`**:
  * A message that gives additional context about the result. In this case, `"Proof request verified successfully."` indicates that the proof request has been successfully verified.

**Data:**

* **`status`**:
  * Indicates the result of the verification process. Here, it is `"success"`, meaning the verification was successful.
* **`credProofId`**:
  * The unique identifier for the proof request, which is `"58e02d58-a762-469e-84ba-882a47345775"`. This ID links the proof request to the specific verification process.
* **`updatedAt`** and **`createdAt`**:
  * Timestamps indicating when the proof request was created and when it was last updated. Both values are `"2024-11-25T12:34:56Z"`, indicating the proof request was created and updated at the same time.
* **`proofStatus`**:
  * The current status of the proof request. It is `"done"`, meaning the proof request was successfully completed and verified.
* **`proofAutoVerify`**:
  * Indicates whether the proof was automatically verified. It is set to `true`, meaning the proof was verified automatically.
* **`comment`**:
  * A comment associated with the proof request verification. Here, it is `"Proof successfully verified."`, indicating the successful completion of the verification.
* **`contactId`**:
  * A unique identifier for the contact associated with the proof request, `"3fa85f64-5717-4562-b3fc-2c963f66afa6"`. This ID links the proof to a specific contact.
* **`verified`**:
  * A boolean value indicating whether the proof was successfully verified. In this case, it is `true`, indicating that the proof has been successfully verified.
* **`errorMsg`**:
  * A message indicating any errors encountered during the verification process. Here, `"abandoned"` could imply that the proof was either not completed or abandoned at some stage.

**Proof Attributes:**

* **`proofAttributes`**:
  * Contains the attributes of the proof. In this case, the proof includes attributes related to an Aadhar card.
  * **`HiNg6sdwNYwPRTTP9VkwpT:3:CL:2535708:Aadhar_card`**:
    * This is the unique identifier for a credential related to the Aadhar card.
    * **`credentialName`**:
      * The name of the credential being referenced, `"HiNg6sdwNYwPRTTP9VkwpT:3:CL:2545708:Aadhar_card"`.
    * **`attributes`**:
      * An array of attributes associated with this credential. In this case, the attribute `"full_name": "John Doe"` is provided, indicating the full name of the individual for the Aadhar card credential.



