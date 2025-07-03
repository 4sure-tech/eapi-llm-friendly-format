# Testing Register Socket API

### Pre-Requisites:

1. The NB Orbit Enterprise Connection API has been downloaded in your system.
2. POSTMAN has been installed in your system

**Environment Setup in Postman:**

1.  **Create a Global Environment**:

    * Go to **Environments** on the top right corner of Postman.
    * Click on **Add**.
    * Name the environment (e.g., "Register Socket API Environment").
    * Add the following variables:
      * `baseUrl`: `https://testapi-connection.nborbit.ca`
      * `apiKey`: GOrx\_-zseD3yN5MGKQLemhF4dawcX9\_f
      * `lobId`:18545c09-c144-43f3-9239-146f3b083d88



    ### <mark style="color:blue;">Test Scenario 1:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to Emit a Socket event</mark>_

    **Objective**: Verify the socket event emition  for a LOB

    **Testing Steps:**

    1. **Create Request**:
    2. Open Postman and create a new request.
    3. Name the request "Emit Socket Event.
    4. Set the request type to POST.
    5. Set the URL to `{{baseUrl}}/api/lob/{{lob_id}}`/api/lob/{lob\_id}/event/emit



    1. **Add Authorization**:
    2. Click on the **Authorization** tab.
    3. Select **API Key** from the dropdown.
    4. Set the **Key** to `api-key`.
    5. Set the **Value** to `{{issuer_apiKey}}`.
    6. **Add Request Body**:

```json
{
  "payloadType": "REGISTER_SOCKET",
  "payload": {}
}
```

Detailed Breakdown: &#x20;

* **Payload Type**:\
  `"payloadType": "REGISTER_SOCKET"` indicates the type of action or event being communicated. In this case, the system is attempting to **register a socket connection**, likely as part of a WebSocket-based communication protocol.\
  This could be used in real-time systems where clients (e.g., browsers, apps, or agents) need to establish a persistent connection to receive live updates, notifications, or messages.
* **Payload**:\
  `"payload": {}` is currently an **empty object**, meaning no additional data is being sent along with the registration message.\
  In a typical implementation, this payload might include:
  * A unique identifier such as `lob_id`, `user_id`, or `session_token`
  * Metadata about the client or session
  * Authorization tokens

**Send Request**:

* Click **Send**.
* Verify the response with sample response below and check the status code to be 201 to ensure the proof request is defined successfully

Response Body :&#x20;

```json
{
  "success": true,
  "message": "socket event successfully submitted.",
  "data": {
    "responseDetails": "DID_COMM_CONNECTION_RESPONSE event successfully submitted for lob b012349b-4ab8-414f-a285-6fce86a1e41c"
  }
}
```

Detailed Breakdown:&#x20;

* **Success Flag**:\
  `"success": true` indicates that the socket event was processed and submitted successfully without any errors. This flag confirms the overall positive outcome of the operation.
* **Message**:\
  `"message": "socket event successfully submitted."` is a user-friendly confirmation that the system has accepted and handled the socket event correctly.
* **Data Object – Response Details**:\
  Under the `"data"` key, we have the field `"responseDetails"` containing a descriptive message:\
  `"DID_COMM_CONNECTION_RESPONSE event successfully submitted for lob b012349b-4ab8-414f-a285-6fce86a1e41c"`.\
  This message conveys the following:
  * The type of event submitted is **`DID_COMM_CONNECTION_RESPONSE`**, which typically relates to the response in a DIDComm connection protocol (e.g., Step 2 of the connection handshake where the invitee responds to an invitation).
  * The event is associated with a specific **LOB (Line of Business) identifier**, in this case: `b012349b-4ab8-414f-a285-6fce86a1e41c`. This ID likely tracks the business or session context for which the event was submitted.
