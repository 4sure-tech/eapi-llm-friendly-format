# Testing the LOB API

### <mark style="color:blue;">Test Scenario 1:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test the registration of your LOB</mark>_

**Objective**: Verify that a User can register an LOB and receive a Transaction ID and API Key via email.

**Testing Steps:**

1. **Create Request:**
   * Open Postman and create a new request.
   * Name the request "Register for LOB".
   * Set the request type to `POST`.
   * Set the URL to [`https://devapi-lob.nborbit.ca/api/lob/register`](https://devapi-lob.nborbit.ca/api/lob/register).
2. **Add Authorization:**
   * Click on the `Authorization` tab.
   * Select `API Key` from the dropdown.
   * Set the Key to `api-key`.
   * Set the Value to `{{apiKey}}` (replace with the actual API key if not using environment variables).
3. **Add Request Body:**
   * In the `Body` tab, select `raw` and set the format to `JSON`.
   *   Add the following JSON structure as the request body:

       `{ "lobDisplayName": "AkvVer", "lobEmail": "amarjeetver28@yopmail.com", "lobOrganizationName": "akv org Ver" }`
   *   **Detailed Breakdown :**\
       **lobDisplayName**: "AkvTest40" - The display name for the user or entity.

       **lobEmail**: "[akv40@getnada.com](mailto:akv40@getnada.com)" - The email address for receiving the transaction ID and API key.

       **loborganizationName**: "akv Org37" - The name of the organization registering for the LOB.


4. **Send Request:**
   * Click `Send`.
5. **Verify Response:**
   * Check the response status code.
   * Expected Result: The response status code should be `201 Created` or a relevant success code.
   * Verify that the Transaction ID and API Key are received in the email specified.

**Verification:**

* Confirm the email contains both the Transaction ID and API Key.
* Ensure the status code is as expected.

***

### <mark style="color:blue;">Test Scenario 2:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test the creation of your LOB</mark>_

**Objective**: Verify that a User can create an LOB ID using the Transaction ID and API Key.

**Testing Steps:**

1. **Create Request:**
   * Open Postman and create a new request.
   * Name the request "Create LOB Id".
   * Set the request type to `POST`.
   * Set the URL to [`https://devapi-lob.nborbit.ca/api/lob/create`](https://devapi-lob.nborbit.ca/api/lob/create.)
2. **Add Authorization:**
   * Click on the `Authorization` tab.
   * Select `API Key` from the dropdown.
   * Set the Key to `api-key`.
   * Set the Value to `{{apiKey}}` (replace with the actual API key if not using environment variables).
3. **Add Request Body:**
   * In the `Body` tab, select `raw` and set the format to `JSON`.
   *   Add the following JSON structure as the request body, replacing `<transactionId>` with the actual transaction Id received:

       `{ "transactionId": "ac1ca380-b8d5-4723-bd0b-4032616a5904", "lobRole": "VERIFIER", "lobTenancy": "SINGLE", "didMethod": "did:web", "lobProtocol": "AIP2_0", "writeLedgerId": 1 }`
   * **Detailed Breakdown :**
     * **transactionId**: "\<transactionId>" - Placeholder for the unique identifier received during registration.
     * **lobrole**: "ISSUER" - Specifies the role of the entity, indicating it will issue credentials.
     * **lobTenancy**: "SINGLE" - Denotes a single agent type configuration for the LOB.
     *   **didMethod**: "did

         " - Indicates the DID (Decentralized Identifier) method used.
     * **lobProtocol**: "AIP2\_0" - Refers to the protocol version for the service.
     * **writeLedgerId**: 1 - A flag indicating whether to write to the ledger (1 for true)
4. **Send Request:**
   * Click `Send`.
5. **Verify Response:**
   * Check the response status code.
   * Expected Result: The response status code should be `201 Created` or a relevant success code.
   * Verify that the LOB ID is received in the email.

**Verification:**

* Confirm the email contains the LOB ID.
* Ensure the status code is as expected.



#### <mark style="color:blue;">Test Scenario 3:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">Use the details below to test the update the LOB</mark>_ <a href="#test-scenario-3-use-the-details-below-to-test-the-update-the-lob" id="test-scenario-3-use-the-details-below-to-test-the-update-the-lob"></a>

**Objective**: Verify that a User can create an LOB ID using the Transaction ID and API Key.

**Testing Steps:**

1. **Create Request:**
   * Open Postman and create a new request.
   * Name the request "Update LOB Id".
   * Set the request type to `PATCH`.
   * Set the URL to `https://devapi-lob.nborbit.ca/api/lob/{lob_id}/update`
2. **Add Authorization:**
   * Click on the `Authorization` tab.
   * Select `API Key` from the dropdown.
   * Set the Key to `api-key`.
   * Set the Value to `{{apiKey}}`
3. **Add Request Body:**
   * In the `Body` tab, select `raw` and set the format to `JSON`.
   * Add the following JSON structure as the request body

```json
{
"lobTrustUrl": "
https://iata-api.trustregistry.nborbit.io
",
"lobTrustAPIKey": "12345678"
}
```

* **Detailed Breakdown :**
  * **lobTrustUrl**: This field specifies the **URL endpoint** of the Line of Business (LOB) Trust Registry API that the system will communicate with. In this example, the URL is `"https://iata-api.trustregistry.nborbit.io"`. This is the base address where all trust registry-related operations are directed. It ensures that the request is routed to the correct environment or service.
  * **lobTrustAPIKey**: This field contains the **API key** used to authenticate and authorize the request to the LOB Trust Registry API. The value `"12345678"` is a placeholder example. This key is required to verify that the requester has the necessary permissions to access and perform operations on the Trust Registry service. Without a valid API key, the server will typically reject the request.
* **Send Request:**
  * Click `Send`.
* **Response Body**&#x20;

```json
{
"success": true,
"message": "LOB updated successfully.",
"data": {
"lobTrustUrl": "
https://iata-api.trustregistry.nborbit.io
",
"lobTrustAPIKey": "12345678"
}
}
```

* Check the response status code.
* Expected Result: The response status code should be `200`.

**Detailed Breakdown :**

1. **success**: This field is a **boolean flag** indicating whether the API request was successful or not. In this response, the value is `true`, which means that the operation (in this case, updating the LOB — Line of Business configuration) was completed successfully without any errors or failures.
2. **message**: This is a **human-readable message** returned by the API to give additional context about the result of the operation. Here, the message is `"LOB updated successfully."`, which clearly informs the user or developer that the Line of Business (LOB) details were updated correctly on the server. This message is useful for logging, debugging, or displaying in the UI to inform end users of the outcome.
3. **data**: This is an **object** that contains additional information or the payload relevant to the operation. In this case, it returns the updated LOB details to confirm what values were stored or modified.
   * **lobTrustUrl**: Within the `data` object, this field echoes back the **LOB Trust Registry API URL** that was updated. The value `"https://iata-api.trustregistry.nborbit.io"` confirms that this URL is now configured or stored in the system as the endpoint for the LOB Trust Registry.
   * **lobTrustAPIKey**: This field within `data` shows the **API key** that was updated or associated with the LOB Trust Registry. The value `"12345678"` (which is an example placeholder) confirms that this key is currently active and configured for authenticating API calls to the specified `lobTrustUrl`.

