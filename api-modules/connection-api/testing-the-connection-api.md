# Testing the Connection API

### Pre-Requisites:

1. The NB Orbit Enterprise Connection API has been downloaded in your system.
2. POSTMAN has been installed in your system

**Environment Setup in Postman:**

1. **Create a Global Environment**:
   * Go to **Environments** on the top right corner of Postman.
   * Click on **Add**.
   * Name the environment (e.g., "Connection API Environment").
   * Add the following variables:
     * `baseUrl`: `https://testapi-connection.nborbit.ca`
     * `Issuer_apiKey`: GOrx\_-zseD3yN5MGKQLemhF4dawcX9\_f
     * `Issuer_lobId`:18545c09-c144-43f3-9239-146f3b083d88
     * Holder\_api\_key: ru04t0PD3Hq\_5ddOUdXagmwEh2AWntn6
     * Holder\_lob\_id: 4461a984-1dfd-4c59-a974-eddc5f64f519



### <mark style="color:blue;">Test Scenario 1:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test did- exchange connection</mark>_

**Objective**: Verify the did exchange connection API from issuer to holder

**Testing Steps:**

1. **Create Request**:

* Open Postman and create a new request.
* Name the request "DID Exchange Connection.
* Set the request type to POST.
*   Set the URL to `{{baseUrl}}/api/lob/{{lob_id}}`/api/lob/{lob\_id}/did-exchange/invitation.



2. **Add Authorization**:

* Click on the **Authorization** tab.
* Select **API Key** from the dropdown.
* Set the **Key** to `api-key`.
* Set the **Value** to `{{issuer_apiKey}}`.

3. **Add Request Body**:\


```json
{
                    "givenName": "holder_test_new",
                    "publicDID": "did:sov:3uvkkhAoXaMjbN9SZumFHv"
                   }
```

Detailed Breakdown:

* **`givenName`**: `"holder_test_new"`
  * This is the name or label given to the holder. It could be a test identity or user for development or QA purposes.
* **`publicDID`**: `"did:sov:3uvkkhAoXaMjbN9SZumFHv"`
  * This is the public **Decentralized Identifier (DID)** associated with the holder.
  * `did:sov:` indicates the DID method (Sovrin in this case).
  * The long string after that is the unique identifier for the holder on the Sovrin ledger.

4.  **Send Request**:

    * Click **Send**.
    * Verify the response with sample response below and check the status code to be 201 to ensure the proof request is defined successfully



Response Body:

```json
{"success":true,"message":"did-exchange connection request send successfully.","data":{"givenName":"holder_test_new","publicDID":"did:sov:3uvkkhAoXaMjbN9SZumFHv","messageProtocol":"AIP2_0"}}
```

**Detailed Breakdown :**

* **`success`**: `true`\
  → Indicates that the connection request was **successfully sent**.
* **`message`**: `"did-exchange connection request send successfully."`\
  → A confirmation message for your request.

***

#### &#x20;**Data Details**

* **`givenName`**: `"holder_test_new"`\
  → The label or name assigned to the **holder agent** initiating the connection.
* **`publicDID`**: `"did:sov:3uvkkhAoXaMjbN9SZumFHv"`\
  → The **Decentralized Identifier** of the holder (the one trying to connect).
* **`messageProtocol`**: `"AIP2_0"`\
  → Specifies that the connection request is using **Aries Interop Profile 2.0**, which is a modern standard for agent communication (DIDComm v2-based typically).

***

### <mark style="color:blue;">Test Scenario 2:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test prepare URL invitation (OOB)</mark>_

**Objective**: Verify that Connection requests can be sent ( Out of Band)

**Testing Steps**:

1. **Create Request**:
   * Open Postman and create a new request.
   * Name the request "prepare OOB invitation URL".
   * Set the request type to POST.
   * Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/oob/prepare-url-invitation.
2. **Add Authorization**:
   * Click on the **Authorization** tab.
   * Select **API Key** from the dropdown.
   * Set the **Key** to `api-key`.
   * Set the **Value** to `{{issuer_apiKey}}`.
3. **Add Request Body**:

```json
{
                    "givenName": "akv-bob",
                    "messageProtocol": "AIP2_0"
                  }
```

* **Detailed Breakdown**\

  * **`givenName`**: `"akv-bob"`\
    → The name/label of the agent that is sending this connection request.
  * **`messageProtocol`**: `"AIP2_0"`\
    → You're continuing to use **Aries Interop Profile 2.0**, which is great for current Aries implementations (supports DIDComm v2).

4. **Send Request**:

* Click **Send**.
* Verify the response with sample response below and check the status code to be 201 to ensure the proof request is defined successfully

Response Body

{% code overflow="wrap" %}
```json
{"success":true,"message":"Out-Of-Band invitation prepared successfully.","data":{"state":"initial","longUrl":"https://issuertestapp.test-eapi.nborbit.ca?oob=eyJAdHlwZSI6ICJodHRwczovL2RpZGNvbW0ub3JnL291dC1vZi1iYW5kLzEuMS9pbnZpdGF0aW9uIiwgIkBpZCI6ICI5ODAxODM2Mi04MTUyLTQ0NDctODcwZi1lZDMzZTI3M2JmN2UiLCAibGFiZWwiOiAiSXNzdWVyIFRlc3QgQXBwIEFnZW50IiwgImhhbmRzaGFrZV9wcm90b2NvbHMiOiBbImh0dHBzOi8vZGlkY29tbS5vcmcvZGlkZXhjaGFuZ2UvMS4wIl0sICJhY2NlcHQiOiBbImRpZGNvbW0vYWlwMjtlbnY9cmZjMTkiXSwgInNlcnZpY2VzIjogW3siaWQiOiAiI2lubGluZSIsICJ0eXBlIjogImRpZC1jb21tdW5pY2F0aW9uIiwgInJlY2lwaWVudEtleXMiOiBbImRpZDprZXk6ejZNa3Q1YVg4aUZtenR4TmE5ZHJ0a1NkNGg4U3VKWWNhNGdmUHpGb2VoYzk4QWFQI3o2TWt0NWFYOGlGbXp0eE5hOWRydGtTZDRoOFN1SlljYTRnZlB6Rm9laGM5OEFhUCJdLCAic2VydmljZUVuZHBvaW50IjogImh0dHBzOi8vaXNzdWVydGVzdGFwcC50ZXN0LWVhcGkubmJvcmJpdC5jYSJ9XX0","shortUrl":"https://testapi-connection.nborbit.ca/url/98018362-8152-4447-870f-ed33e273bf7e"}}
```
{% endcode %}

**Detailed Breakdown**&#x20;

* **State**:
  * `initial` — This indicates that the invitation has been generated but not yet acted upon by the receiving agent.
* **Long URL**:
  * `https://issuertestapp.test-eapi.nborbit.ca?...`
  * This is a fully encoded invitation URL containing all necessary DIDComm metadata. It includes identifiers such as:
    * `@type`: The protocol type (`https://didcomm.org/out-of-band/1.1/invitation`)
    * `@id`: A unique ID (`98018362-8152-4447-870f-ed33e273bf7e`)
    * `label`: The agent label (`Issuer Test App Agent`)
    * `handshake_protocols`: Specifies supported protocols (e.g., `https://didcomm.org/didexchange/1.0`)
    * `accept`: Lists acceptable MIME types (`didcomm/aip2;env=rfc19`)
    * `services`: Includes the agent’s recipient keys and service endpoint used to establish the connection.
* **Short URL**:
  * `https://testapi-connection.nborbit.ca/url/98018362-8152-4447-870f-ed33e273bf7e`
  * This is a condensed version of the long URL. It provides a user-friendly link, ideal for sharing via email, QR codes, or direct messaging.



***

### <mark style="color:blue;">Test Scenario 3:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test  OOB invitation</mark>_&#x20;

**Objective**: Verify the response when an OOB request is sent

**Testing Steps:**

1. **Create Request**:
   * Open Postman and create a new request.
   * Name the request "send OOB Invitation".
   * Set the request type to POST.
   * Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/oob/invitation\

2. **Add Authorization**:
   * Click on the **Authorization** tab.
   * Select **API Key** from the dropdown.
   * Set the **Key** to `api-key`.
   * Set the **Value** to `{{issuer_apiKey}}`.\

3. **Add Request Body**:

```
{
                   "givenName": "akv-bob",
                    "messageProtocol": "AIP2_0",
                    "recipientEmail": "newtest4@getnada.com"
                    }
```

Detailed Breakdown

* **`givenName: "akv-bob"`**
  * This identifies the alias or label for the **recipient** (or holder agent) to whom the OOB invitation is being sent.
  * It's used for internal display or identification in the system logs/UI.
* **`messageProtocol: "AIP2_0"`**
  * This specifies the version of the **Aries Interop Profile** (AIP) that will be used in the communication.
  * `AIP2_0` refers to Aries Interop Profile 2.0, which supports newer DIDComm v1.0/2.0 standards and is compatible with protocols like `didexchange/1.0`.
* **`recipientEmail: "newtest4@getnada.com"`**
  * The **email address** where the OOB invitation will be sent.
  * In this case, the invitation is being delivered to a disposable inbox at [getnada.com](https://getnada.com/), likely for testing purposes.



1.  **Send Request**:

    * Click **Send**.
    * Verify the response with sample response below and check the status code to be 201 to ensure the proof request is defined successfully
    *   `Response Body`

        ```json
        {
          "success": true,
          "message": "out-of-band invitation send successfully.",
          "data": {
            "responseDetails": "Mail successfully sent to john@yopmail.com"
          }
        }
        ```

    **Detailed Breakdown**&#x20;

* **`success: true`**
  * Indicates that the request to send the Out-Of-Band (OOB) invitation was successful.
  * The backend completed all necessary operations, such as generating the invitation and delivering it.
* **`message: "out-of-band invitation send successfully."`**
  * A descriptive confirmation that the OOB invitation was processed and dispatched as intended.
* **`data.responseDetails: "Mail successfully sent to john@yopmail.com"`**
  * Confirms the **invitation email** was sent to the intended recipient’s inbox.
  * The email address here, `john@yopmail.com`, suggests usage of [YOPmail](https://yopmail.com/), a disposable email provider often used for testing.



***

### <mark style="color:blue;">Test Scenario 4:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test the OOB details API</mark>_

**Objective**: Verify the response when OOB details API is requested

**Testing Steps:**

1. **Create Request**:
   * Open Postman and create a new request.
   * Name the request "fetch OOB invitation Details".
   * Set the request type to POST.
   * Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/oob/details\

2. **Add Authorization**:
   * Click on the **Authorization** tab.
   * Select **API Key** from the dropdown.
   * Set the **Key** to `api-key`.
   * Set the **Value** to `{{Issuer_apiKey}}`.\

3. **Add Request Body**:

```json
{
  "longUrl": "http://192.168.1.10:9013?oob=eyJAdHlwZSI6ICJodHRwczovL2RpZGNvbW0ub3JnL291dC1vZi1iYW5kLzEuMS9pbnZpdGF0aW9uIiwgIkBpZCI6ICI0MGE3MjNhNS03MWU0LTRhNTgtYmY1YS05MTVhZDY4NDNhNDIiLCAibGFiZWwiOiAiYnJpaiBvcmcgQWdlbnQiLCAiaGFuZHNoYWtlX3Byb3RvY29scyI6IFsiaHR0cHM6Ly9kaWRjb21tLm9yZy9kaWRleGNoYW5nZS8xLjAiXSwgImFjY2VwdCI6IFsiZGlkY29tbS9haXAxIl0sICJzZXJ2aWNlcyI6IFt7ImlkIjogIiNpbmxpbmUiLCAidHlwZSI6ICJkaWQtY29tbXVuaWNhdGlvbiIsICJyZWNpcGllbnRLZXlzIjogWyJkaWQ6a2V5Ono2TWtrRWNDVkU2RG1tdThUTXRVUjhvWng2cnZTc3NiQUdFYmRxeFZ3TG9jR0t6NiN6Nk1ra0VjQ1ZFNkRtbXU4VE10VVI4b1p4NnJ2U3NzYkFHRWJkcXhWd0xvY0dLejYiXSwgInNlcnZpY2VFbmRwb2ludCI6ICJodHRwOi8vMTkyLjE2OC4xLjEwOjkwMTMifV19"
}
```

&#x20;Detailed Breakdown

*   **`long_url`**: This url is received from an OOB prepare URL api.





1.  **Send Request**:

    * Click **Send**.
    * Verify the response with sample response below and check the status code to be 201 to ensure the proof request is defined successfully

    `Response Body`

```json
{
  "success": true,
  "message": "Invitation saved successfully.",
  "data": {
    "messageProtocol": "AIP2_0",
    "theirLabel": "Faber",
    "invitationId": 1
  }
}
```

**Detailed Breakdown**&#x20;

* **`success: true`**
  * The operation to **save the received invitation** was successfully executed.
* **`message: "Invitation saved successfully."`**
  * A simple confirmation message indicating that the system has persisted the invitation information.
* **`data.messageProtocol: "AIP2_0"`**
  * Specifies the protocol used in the message exchange.
  * `AIP2_0` refers to **Aries Interop Profile 2.0**, a standard for DIDComm messaging and connection protocols.
* **`data.theirLabel: "Faber"`**
  * The label/name of the other party (in this case, **Faber**), usually the **issuer or inviter**.
  * Useful for identifying the relationship or agent involved.
* **`data.invitationId: 1`**
  * Internal identifier used to track or reference this saved invitation within the system or database.

***

### <mark style="color:blue;">Test Scenario 5:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test the Accept invitation API  request is sent</mark>_

**Objective**: Verify that the accept invitation API &#x20;

**Testing Steps:**

1. **Create Request**:
   * Open Postman and create a new request.
   * Name the request "Accept invitation".
   * Set the request type to POST.
   * Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/accept-invitation\

2.  **Add Authorization**:

    * Click on the **Authorization** tab.
    * Select **API Key** from the dropdown.
    * Set the **Key** to `api-key`.
    * Set the **Value** to `{{holder_apiKey}}`.

    \

3. Request\_body

```json
 {
        "invitationId": 133,
        "givenName": "amarjeet_verifier"
    }
```

**Detailed Breakdown**

* **`invitationId: 133`**
  * This is the unique identifier for a **saved or received invitation** in the system.
  * Likely used to **initiate a connection** or continue a specific Out-Of-Band or DIDComm protocol flow (e.g., accepting an invitation).
* **`givenName: "amarjeet_verifier"`**
  * Refers to the name or label of the **verifier agent** or participant involved in this communication.
  * It helps distinguish between different agents (like holder, issuer, verifier) in decentralized identity workflows.

4. **Send Request**:

* Click **Send**.
* Verify the response with sample response below and check the status code to be 200 to ensure the proof request is defined successfully

**Response Body:**&#x20;

{% code overflow="wrap" %}
```json
{"success":true,"message":"connection request accepted successful.","data":{"givenName":"amarjeet_verifier","messageProtocol":"AIP2_0","publicDID":"did:sov:6YXT2jddYg1TZarJjbKGng"}}
```
{% endcode %}

**Detailed Breakdown**&#x20;

* **`success: true`**\
  Indicates that the connection request was processed without errors.
* **`message: "connection request accepted successful."`**\
  A confirmation message from the system, though grammatically it should be _"connection request accepted successfully."_

***

#### &#x20;**Data Breakdown**

* **`givenName: "amarjeet_verifier"`**\
  The name of the **verifier agent** that accepted the connection request. It identifies the party taking part in the DIDComm interaction.
* **`messageProtocol: "AIP2_0"`**\
  The protocol version used in the interaction.
  * AIP 2.0 is based on **DIDComm v2** and supports **Out-of-Band 2.0**, **DID Exchange 1.1**, and other features from Aries RFCs.
* **`publicDID: "did:sov:6YXT2jddYg1TZarJjbKGng"`**\
  The **Decentralized Identifier** (DID) of the **verifier agent**.
  * This DID is used to uniquely identify the agent in the network and is essential for establishing secure, peer-to-peer communication.



***

### <mark style="color:blue;">Test Scenario 6:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test retrieving the list of pending connection API</mark>_

**Objective**: Verify the response of Pending connection API

**Testing Steps**:

1. **Create Request**:
   * Open Postman and create a new request.
   * Name the request "Get Pending connection invitation".
   * Set the request type to GET.
   *   Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/pending-connections

       \

2. **Add Authorization**:
   * Click on the **Authorization** tab.
   * Select **API Key** from the dropdown.
   * Set the **Key** to `api-key`.
   * Set the **Value** to `{{holder_apiKey}}`.\

3.  **Send Request**:

    Click **Send**.

    Verify the response with sample response below and check the status code to be 200 to ensure the proof request is defined successfully

Response Body

{% code overflow="wrap" %}
```json
{"success":true,"message":"pending connection record fetched successfully.","data":{"items":[{"invitationId":1148,"connectionId":"6fdcd938-48f4-4612-9292-2aa469245663","lobName":"Holder test app","givenName":"Issuer Test App Agent","messageProtocol":"AIP2_0","theirDid":"6YXT2jddYg1TZarJjbKGng","myRole":"inviter","theirRole":"invitee","recipientEmail":null,"createdAt":"2025-04-17T11:26:38.888Z","updatedAt":"2025-04-17T11:26:38.888Z"}],"meta":{"totalItems":1,"itemCount":1,"itemsPerPage":10,"totalPages":1,"currentPage":1}}}
```
{% endcode %}

**Detailed Breakdown:**

* **`success: true`**\
  The request was successful, and the pending connection record was retrieved.
* **`message: "pending connection record fetched successfully."`**\
  A confirmation message indicating that the connection record is available for further action.

***

#### 📘 **Data Breakdown**

* **`invitationId: 1148`**\
  The **invitation ID** associated with this connection. It is a unique identifier for the invitation.
* **`connectionId: "6fdcd938-48f4-4612-9292-2aa469245663"`**\
  The **connection ID** is the unique identifier for the connection request.
* **`lobName: "Holder test app"`**\
  The name of the application or agent that is involved in the connection request.\
  In this case, it appears to be a **holder test application**.
* **`givenName: "Issuer Test App Agent"`**\
  The name of the agent sending the invitation. It is labeled as the **Issuer Test App Agent**.
* **`messageProtocol: "AIP2_0"`**\
  The protocol version used in the connection request, **AIP2\_0**, which is part of the Aries Interoperability Protocols (AIP) suite.
* **`theirDid: "6YXT2jddYg1TZarJjbKGng"`**\
  The **DID** (Decentralized Identifier) of the invitee (the other party in the connection). This is the identifier of the agent that is being invited.
* **`myRole: "inviter"`**\
  The role of the party requesting the connection. Here, it’s an **inviter**.
* **`theirRole: "invitee"`**\
  The role of the party receiving the invitation. Here, it’s an **invitee**.
* **`recipientEmail: null`**\
  The **recipient's email** is not provided, indicating that it may not be needed for this specific connection or may be optional.
* **`createdAt: "2025-04-17T11:26:38.888Z"`**\
  The timestamp when the connection invitation was created.
* **`updatedAt: "2025-04-17T11:26:38.888Z"`**\
  The timestamp when the connection record was last updated.



***

### <mark style="color:blue;">Test Scenario 7:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test deleting a specific pending connection</mark>_

**Objective**: Verify that a specific connection is deleted using DELETE APIn be deleted

**Variables**:



* **Testing Steps**:

1. **Create Request**:
   * Open Postman and create a new request.
   * Name the request "Delete Pending connection.
   * Set the request type to DELETE.
   *   Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/pending-connection.

       \

2. **Add Authorization**:
   * Click on the **Authorization** tab.
   * Select **API Key** from the dropdown.
   * Set the **Key** to `api-key`.
   * Set the **Value** to `{{apiKey}}`.\

3. **Add Request Body**:

```
{
  "invitationId": 1148
}

```

1.  **Send Request**:

    * Click **Send**.
    * Verify the response with sample response below and check the status code to be 200 to ensure the proof request is defined successfully

    &#x20;


2. **Response Body**

{% code overflow="wrap" %}
```json
 {"success":true,"message":"Invitation record deleted successfully.","data":{"responseDetails":"Invitation record with id '1148' is deleted successfully!"}}
```
{% endcode %}

1. **Detailed Breakdown :**

* **`success: true`**\
  The deletion operation was successful.
* **`message: "Invitation record deleted successfully."`**\
  A confirmation message indicating that the invitation record has been deleted.

***

#### &#x20;**Data Breakdown**

* **`responseDetails: "Invitation record with id '1148' is deleted successfully!"`**\
  The **invitation record** with ID **1148** has been successfully deleted from the system.

####

&#x20;







***

### <mark style="color:blue;">Test Scenario 8:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the Get Contact Using Id API to get the details of any Contact</mark>_

**Objective**: Verify the repsone of the API to display the details of any Contact

**Testing Steps**:

1. **Create Request**:
   * Open Postman and create a new request.
   * Name the request "Get details of a contact.
   * Set the request type to GET.
   *   Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/contact/{contact\_id}.

       \

2. **Add Authorization**:
   * Click on the **Authorization** tab.
   * Select **API Key** from the dropdown.
   * Set the **Key** to `api-key`.
   * Set the **Value** to `{{holder_apiKey}}`.\

3.  **Send Request**:

    * Click **Send**.
    * Verify the response with sample response below and check the status code to be 200 to ensure the proof request is defined successfully
    * `Response Body`&#x20;



```json
```

1. **Detailed Breakdown :**









***

### <mark style="color:blue;">Test Scenario 9:</mark>  <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the Get Contact  API to get the details of all  Contact</mark>_

### **Objective**: Verify the API response of Get Contact API

**Testing Steps**:

1. **Create Request**:
   * Open Postman and create a new request.
   * Name the request "Get COntact".
   * Set the request type to POST.
   *   Set the URL to `{{baseUrl}}`//api/lob/{lob\_id}/contacts.

       \

2. **Add Authorization**:
   * Click on the **Authorization** tab.
   * Select **API Key** from the dropdown.
   * Set the **Key** to `api-key`.
   * Set the **Value** to `{{_holder_apiKey}}`.\

3. **Send Request**:
   * Click **Send**.
   * Verify the response with sample response below and check the status code to be 201 to ensure the proof request is defined successfully
4. Response Body

```
{
  "success": true,
  "message": "contact list fetched successful.",
  "data": {
    "items": [
      {
        "id": "0343e6db-7a41-4392-842f-c654b8a3870d",
        "givenName": "amarjeet_verifier",
        "email": null,
        "phone": null,
        "logo": null,
        "state": "active",
        "createdAt": "2025-04-17T11:06:54.822Z",
        "updatedAt": "2025-04-17T11:24:22.692Z"
      },
      {
        "id": "ac4a6421-92f1-4baa-8c4a-c560913981a2",
        "givenName": "Issuer Test App Agent",
        "email": null,
        "phone": null,
        "logo": null,
        "state": "active",
        "createdAt": "2025-04-16T12:49:36.856Z",
        "updatedAt": "2025-04-16T12:49:37.295Z"
      },
      {
        "id": "b0a964f8-3d45-4f5f-a359-6a161d7537c3",
        "givenName": "amarjeet_verifier",
        "email": null,
        "phone": null,
        "logo": null,
        "state": "active",
        "createdAt": "2025-04-08T10:40:26.294Z",
        "updatedAt": "2025-04-08T11:50:50.687Z"
      },
      {
        "id": "cd853956-422d-4ddd-99f8-c8e63e8c0634",
        "givenName": "amarjeet_verifier",
        "email": null,
        "phone": null,
        "logo": null,
        "state": "active",
        "createdAt": "2025-04-04T12:25:38.013Z",
        "updatedAt": "2025-04-04T12:26:22.078Z"
      },
      {
        "id": "d58423cf-835a-48d6-824e-6ec5acdb6261",
        "givenName": "amarjeet_verifier",
        "email": null,
        "phone": null,
        "logo": null,
        "state": "active",
        "createdAt": "2025-04-04T10:53:08.440Z",
        "updatedAt": "2025-04-04T10:54:13.610Z"
      }
    ],
    "meta": {
      "totalItems": 5,
      "itemCount": 5,
      "itemsPerPage": 10,
      "totalPages": 1,
      "currentPage": 1
    }
  }
}
```

&#x20;Detailed Breakdown

* **Success:** The request was successful (`"success": true`).
* **Message:** A confirmation message that the contact list was fetched successfully: `"contact list fetched successful."`

***

#### **Data:**

* **Items:** The main part of the response contains a list of **5 active contacts**. Each contact has detailed information such as ID, given name, email, phone, logo, state, creation date, and update date.

***

#### **Individual Contacts:**

1. **First Contact:**
   * **ID:** `"0343e6db-7a41-4392-842f-c654b8a3870d"`
   * **Given Name:** `"amarjeet_verifier"`
   * **Email:** `null` (No email provided)
   * **Phone:** `null` (No phone provided)
   * **Logo:** `null` (No logo provided)
   * **State:** `"active"`
   * **Created At:** `"2025-04-17T11:06:54.822Z"`
   * **Updated At:** `"2025-04-17T11:24:22.692Z"`
2. **Second Contact:**
   * **ID:** `"ac4a6421-92f1-4baa-8c4a-c560913981a2"`
   * **Given Name:** `"Issuer Test App Agent"`
   * **Email:** `null`
   * **Phone:** `null`
   * **Logo:** `null`
   * **State:** `"active"`
   * **Created At:** `"2025-04-16T12:49:36.856Z"`
   * **Updated At:** `"2025-04-16T12:49:37.295Z"`
3. **Third Contact:**
   * **ID:** `"b0a964f8-3d45-4f5f-a359-6a161d7537c3"`
   * **Given Name:** `"amarjeet_verifier"`
   * **Email:** `null`
   * **Phone:** `null`
   * **Logo:** `null`
   * **State:** `"active"`
   * **Created At:** `"2025-04-08T10:40:26.294Z"`
   * **Updated At:** `"2025-04-08T11:50:50.687Z"`
4. **Fourth Contact:**
   * **ID:** `"cd853956-422d-4ddd-99f8-c8e63e8c0634"`
   * **Given Name:** `"amarjeet_verifier"`
   * **Email:** `null`
   * **Phone:** `null`
   * **Logo:** `null`
   * **State:** `"active"`
   * **Created At:** `"2025-04-04T12:25:38.013Z"`
   * **Updated At:** `"2025-04-04T12:26:22.078Z"`
5. **Fifth Contact:**
   * **ID:** `"d58423cf-835a-48d6-824e-6ec5acdb6261"`
   * **Given Name:** `"amarjeet_verifier"`
   * **Email:** `null`
   * **Phone:** `null`
   * **Logo:** `null`
   * **State:** `"active"`
   * **Created At:** `"2025-04-04T10:53:08.440Z"`
   * **Updated At:** `"2025-04-04T10:54:13.610Z"`

***

#### **Meta Information:**

* **Total Items:** 5
* **Items per Page:** 10 (There are 5 items fetched in total, so only 1 page is needed)
* **Total Pages:** 1 (Only one page of contact data)
* **Current Page:** 1 (The first page is being displayed)







### <mark style="color:blue;">Test Scenario 10:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test deleting a specific contact</mark>_

**Objective**: Verify that a specific contact is deleted using DELETE API&#x20;

**Variables**:



* **Testing Steps**:

1. **Create Request**:
   * Open Postman and create a new request.
   * Name the request "Delete Contact.
   * Set the request type to DELETE.
   *   Set the URL to `{{baseUrl}}`/api/lob/{lob\_id}/contact.

       \

2. **Add Authorization**:
   * Click on the **Authorization** tab.
   * Select **API Key** from the dropdown.
   * Set the **Key** to `api-key`.
   * Set the **Value** to `{{holder_apiKey}}`.\

3. **Add Request Body**:

```
{
  "contactId": 1148
}

```

1.  **Send Request**:

    * Click **Send**.
    * Verify the response with sample response below and check the status code to be 200 to ensure the proof request is defined successfully

    &#x20;


2. **Response Body**

{% code overflow="wrap" %}
```json
{"success":true,"message":"Contact record deleted successfully.","data":{"responseDetails":"Contact record with id 'bdcbf5ec-79f5-43b2-a49f-d98ea8f35b7a' is deleted successfully."}}
```
{% endcode %}

1. **Detailed Breakdown :**

* **Success:**
  * The operation was completed successfully, as indicated by `"success": true`.
* **Message:**
  * A general confirmation message: `"Contact record deleted successfully."`
* **Data:**
  * **Response Details:**
    * A more specific message confirming the deletion:\
      `"Contact record with id 'bdcbf5ec-79f5-43b2-a49f-d98ea8f35b7a' is deleted successfully."`
    * This indicates that the contact identified by the UUID `bdcbf5ec-79f5-43b2-a49f-d98ea8f35b7a` has been removed from the system database.

####
