# Testing The Chat API

### Pre-Requisites:

1. The NB Orbit Enterprise Connection API has been downloaded in your system.
2. POSTMAN has been installed in your system

**Environment Setup in Postman:**

1. **Create a Global Environment**:
   * Go to **Environments** on the top right corner of Postman.
   * Click on **Add**.
   * Name the environment (e.g., "Chat API Environment").
   * Add the following variables:
     * `baseUrl`: `https://testapi-connection.nborbit.ca`
     * `Sender_apiKey`: GOrx\_-zseD3yN5MGKQLemhF4dawcX9\_f
     * `Sender_lobId`:18545c09-c144-43f3-9239-146f3b083d88
     * Receiver\_api\_key: ru04t0PD3Hq\_5ddOUdXagmwEh2AWntn6
     * Receiver\_lob\_id: 4461a984-1dfd-4c59-a974-eddc5f64f519



### <mark style="color:blue;">Test Scenario 1:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test response when sender LOB send message to receiver LOB</mark>_

**Objective**: Verify the response _<mark style="color:blue;">when sender LOB send message to receiver LOB</mark>_

**Testing Steps:**

1. **Create Request**:

* Open Postman and create a new request.
  * Name the request "Send a Message.
  * Set the request type to POST.
  *   Set the URL to `{{baseUrl}}/api/lob/{{lob_id}}`/chat/lob/{lob\_id}/contact/{contact\_id}/send.



2. **Add Authorization**:

* Click on the **Authorization** tab.
  * Select **API Key** from the dropdown.
  * Set the **Key** to `api-key`.
  * Set the **Value** to `{{sender_apiKey}}`.

3. Set Path Parameter :\
   a. Lob\_id   — Enter lob Id of sender\
   b. Connection\_id  —  Connection ID from Sender to Receiver
4. **Add Request Body**:

```json
{
  "content": "Hello"
}
```

Detailed Breakdown : \


* **Content Field**:\
  `"content": "Hello"`\
  This field carries a plain text message with the value `"Hello"`. It could be used in various contexts such as:
  * A chat or messaging system to transmit user messages
  * A test or placeholder payload to confirm message formatting
  * A lightweight notification or greeting message in an API

5. Send the Request Button.

Response Body :&#x20;

```json
{
  "success": true,
  "data": {
    "message": "Hello",
    "isRead": false,
    "contactId": "e4973c8e-c3fd-4260-85f4-80f558fb4f03",
    "chatId": 1
  }
}
```

Detailed Breakdown:&#x20;

* **`success: true`**\
  Indicates that the operation (likely fetching or posting a message) was completed successfully without any errors. This is a standard way of signaling the status of an API call.



* **`message: "Hello"`**\
  The content of the message. In this case, the message is a simple greeting: **"Hello"**. This could represent either a message received or sent in a chat.
* **`isRead: false`**\
  A boolean flag that shows the **read status** of the message:
  * `false` means the message **has not been read** yet.
  * This flag could be used to trigger visual indicators like notifications, unread badges, or styling differences in the chat UI.
* **`contactId: "e4973c8e-c3fd-4260-85f4-80f558fb4f03"`**\
  This is a **unique identifier** (UUID format) representing the contact or participant involved in the message exchange.\
  It helps map this message to the corresponding contact in the chat system (e.g., a user profile or device).
* **`chatId: 1`**\
  This refers to the **chat thread or conversation ID**.\
  In a chat application, multiple messages belong to a specific chat or conversation. The `chatId` groups this message with others in that same thread.



\


### <mark style="color:blue;">Test Scenario 2:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test response  when Fetch All Message from all contacts API is called</mark>_

**Objective**: Verify the response <mark style="color:blue;">when sender LOB send message to receiver LOB</mark>

**Testing Steps:**

1. **Create Request**:

* Open Postman and create a new request.
  * Name the request "Get  all Message.
  * Set the request type to GET.
  *   Set the URL to `{{baseUrl}}`/chat/lob/{lob\_id}



2. **Add Authorization**:

* Click on the **Authorization** tab.
  * Select **API Key** from the dropdown.
  * Set the **Key** to `api-key`.
  * Set the **Value** to `{{receiver_keys_apiKey}}`.

3. Set Path Parameter :\
   a. Lob\_id   — Enter lob Id of Receiver
4. **Send The Request**&#x20;
5. **Response Body**

```json
{
  "success": true,
  "message": "Messages fetched successfully",
  "data": {
    "items": [
      {
        "contact": "2fb4cd7a-c9e3-436c-ab00-6c1cf0d6f605",
        "messages": [
          {
            "id": 61,
            "message": "Hello testing amarjeet",
            "state": "received",
            "isRead": false,
            "createdAt": "2025-06-12T11:51:30.603Z",
            "updatedAt": "2025-06-12T11:51:30.603Z"
          },
          {
            "id": 59,
            "message": "Hello testing amarjeet",
            "state": "received",
            "isRead": false,
            "createdAt": "2025-06-10T11:52:19.768Z",
            "updatedAt": "2025-06-10T11:52:19.768Z"
          }
        ]
      },
      {
        "contact": "9e1340c7-6b97-46c6-8cf5-701df7ac36e1",
        "messages": [
          {
            "id": 55,
            "message": "Hello testing amarjeet",
            "state": "received",
            "isRead": true,
            "createdAt": "2025-06-03T13:36:00.470Z",
            "updatedAt": "2025-06-03T13:36:04.497Z"
          },
          {
            "id": 53,
            "message": "Hello testing amarjeet",
            "state": "received",
            "isRead": true,
            "createdAt": "2025-06-03T12:48:14.817Z",
            "updatedAt": "2025-06-03T12:48:19.572Z"
          },
          {
            "id": 51,
            "message": "Hello testing amarjeet i am sender from Postman",
            "state": "received",
            "isRead": true,
            "createdAt": "2025-06-02T10:41:50.343Z",
            "updatedAt": "2025-06-02T10:45:15.281Z"
          },
          {
            "id": 48,
            "message": "Hello i have recievd",
            "state": "sent",
            "isRead": false,
            "createdAt": "2025-06-02T10:38:21.710Z",
            "updatedAt": "2025-06-02T10:38:21.710Z"
          },
          {
            "id": 47,
            "message": "Hello testing amarjeet i am sender",
            "state": "received",
            "isRead": false,
            "createdAt": "2025-06-02T10:36:25.675Z",
            "updatedAt": "2025-06-02T10:36:25.675Z"
          },
          {
            "id": 45,
            "message": "Hello testing amarjeet",
            "state": "received",
            "isRead": true,
            "createdAt": "2025-05-30T13:02:01.011Z",
            "updatedAt": "2025-05-30T13:40:36.098Z"
          },
          {
            "id": 43,
            "message": "Hello testing amarjeet",
            "state": "received",
            "isRead": true,
            "createdAt": "2025-05-30T11:02:23.316Z",
            "updatedAt": "2025-05-30T11:03:29.456Z"
          }
        ]
      }
    ],
    "meta": {
      "totalItems": 9,
      "itemCount": 9,
      "itemsPerPage": 10,
      "totalPages": 1,
      "currentPage": 1
    }
  }
}
```

Detailed Breakdown : \


* **ID (`id: 61`)**:\
  This is the unique identifier for the message. It helps in tracking, referencing, or updating this specific message in the database or UI.
* **Message Content (`"message": "Hello testing amarjeet"`)**:\
  This is the text content of the message. In this case, it simply reads: _"Hello testing amarjeet"_ — likely part of a chat or test messaging session.
* **State (`"state": "received"`)**:\
  The `"state"` indicates the status of the message in the communication lifecycle.
  * `"received"` typically means the message was **received by the recipient**, but not necessarily read.
  * Other possible states in such systems could be `"sent"`, `"delivered"`, or `"failed"`.
* **Read Status (`"isRead": false`)**:\
  This boolean indicates whether the recipient has read the message:
  * `false` means it is **unread**.
  * This can be used to show notifications, badge counts, or change message appearance (e.g., bold for unread).
* **Timestamps**:
  * **`createdAt: "2025-06-12T11:51:30.603Z"`**\
    This marks when the message was originally created or received by the system, in **ISO 8601 UTC format**.
  * **`updatedAt: "2025-06-12T11:51:30.603Z"`**\
    This represents when the message was last modified (e.g., marked as read, edited).\
    In this case, since it's identical to the creation time, the message likely hasn't been modified since its creation.



### <mark style="color:blue;">Test Scenario 3:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test response  when Fetch All Message from a contacts API is called</mark>_

**Objective**: Verify the response <mark style="color:blue;">when sender LOB send message to receiver LOB</mark>

**Testing Steps:**

1. **Create Request**:

* Open Postman and create a new request.
  * Name the request "Get  all Message.
  * Set the request type to GET.
  *   Set the URL to `{{baseUrl}}`/chat/lob/{lob\_id}/contact/{contact\_id}



2. **Add Authorization**:

* Click on the **Authorization** tab.
  * Select **API Key** from the dropdown.
  * Set the **Key** to `api-key`.
  * Set the **Value** to `{{receiver_keys_apiKey}}`.

3. Set Path Parameter :\
   a. Lob\_id   — Enter lob Id of Receiver\
   b.Contact\_id -  Enter Contact Id to Sender
4. **Send The Request**&#x20;
5. **Response Body**

```json
{
  "success": true,
  "message": "Messages fetched succesfully ",
  "data": {
    "items": [
      {
        "id": 63,
        "contact": "2fb4cd7a-c9e3-436c-ab00-6c1cf0d6f605",
        "message": "Hello testing amarjeet date june 12",
        "state": "received",
        "isRead": false,
        "createdAt": "2025-06-12T12:36:31.019Z",
        "updatedAt": "2025-06-12T12:36:31.019Z"
      },
      {
        "id": 61,
        "contact": "2fb4cd7a-c9e3-436c-ab00-6c1cf0d6f605",
        "message": "Hello testing amarjeet",
        "state": "received",
        "isRead": false,
        "createdAt": "2025-06-12T11:51:30.603Z",
        "updatedAt": "2025-06-12T11:51:30.603Z"
      },
      {
        "id": 59,
        "contact": "2fb4cd7a-c9e3-436c-ab00-6c1cf0d6f605",
        "message": "Hello testing amarjeet",
        "state": "received",
        "isRead": false,
        "createdAt": "2025-06-10T11:52:19.768Z",
        "updatedAt": "2025-06-10T11:52:19.768Z"
      }
    ],
    "meta": {
      "totalItems": 3,
      "itemCount": 3,
      "itemsPerPage": 10,
      "totalPages": 1,
      "currentPage": 1
    }
  }
}
```

Detailed Breakdown : \


* **ID (`id: 61`)**:\
  This is the unique identifier for the message. It helps in tracking, referencing, or updating this specific message in the database or UI.
* **Message Content (`"message": "Hello testing amarjeet"`)**:\
  This is the text content of the message. In this case, it simply reads: _"Hello testing amarjeet"_ — likely part of a chat or test messaging session.
* **State (`"state": "received"`)**:\
  The `"state"` indicates the status of the message in the communication lifecycle.
  * `"received"` typically means the message was **received by the recipient**, but not necessarily read.
  * Other possible states in such systems could be `"sent"`, `"delivered"`, or `"failed"`.
* **Read Status (`"isRead": false`)**:\
  This boolean indicates whether the recipient has read the message:
  * `false` means it is **unread**.
  * This can be used to show notifications, badge counts, or change message appearance (e.g., bold for unread).
* **Timestamps**:
  * **`createdAt: "2025-06-12T11:51:30.603Z"`**\
    This marks when the message was originally created or received by the system, in **ISO 8601 UTC format**.
  * **`updatedAt: "2025-06-12T11:51:30.603Z"`**\
    This represents when the message was last modified (e.g., marked as read, edited).\
    In this case, since it's identical to the creation time, the message likely hasn't been modified since its creation.





### <mark style="color:blue;">Test Scenario 4:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test response of the API when the receiver reads the message.</mark>_

**Objective**: Verify the response _<mark style="color:blue;">when sender LOB send message to receiver LOB</mark>_

**Testing Steps:**

1. **Create Request**:

* Open Postman and create a new request.
  * Name the request "Read a Message.
  * Set the request type to PATCH.
  *   Set the URL to `{{baseUrl}}`/chat/lob/{lob\_id}/contact/{contact\_id}/read



2. **Add Authorization**:

* Click on the **Authorization** tab.
  * Select **API Key** from the dropdown.
  * Set the **Key** to `api-key`.
  * Set the **Value** to `{{sender_apiKey}}`.

3. Set Path Parameter :\
   a. Lob\_id   — Enter lob Id of sender\
   b. Connection\_id  —  Connection ID from Sender to Receiver\

4. Add a Query Parameter:\
   a. Message\_Id = Enter the message Id to read it.
5. Send The request .
6. Verify the response&#x20;
7. Response Body :&#x20;

```json

  "success": true,
  "message": "message status updated succesfully",
  "data": {
    "isRead": true,
    "contactId": "e4973c8e-c3fd-4260-85f4-80f558fb4f03",
    "messageId": 2
  }
}
```

Detailed Breakdown: \


* **`success: true`**\
  This indicates that the API request—likely an update to the message status—was processed **successfully** without any errors.
* **`message: "message status updated succesfully"`**\
  A human-readable confirmation stating that the **message status was updated**, probably changing its read/unread state. Note the small typo in “succesfully” (should be “successfully”).
* **`isRead: true`**\
  This field confirms that the **message has now been marked as read**.\
  The previous state (e.g., `false`) is now updated to `true`, indicating the recipient has viewed the message.
* **`contactId: "e4973c8e-c3fd-4260-85f4-80f558fb4f03"`**\
  This is the **UUID of the contact** involved in this message exchange. It helps the system know which contact this message belongs to or who the message was from/to.
* **`messageId: 2`**\
  This represents the **unique identifier** of the message whose status was updated. It allows tracking or referencing the specific message in logs, UI, or follow-up actions.
