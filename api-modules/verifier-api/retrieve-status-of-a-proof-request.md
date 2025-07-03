# Retrieve Status of A Proof Request

The _**Retrieve Status of a Proof Request API**_ retrieves a specific proof request (based on the proof request ID) that has been sent to a Wallet, or Credential Holder, but the Holder has not yet responded with either a decline or a credential presentation.\
\
The Credential Holder can decide not to scan the QR code or can scan the QR code at any time. After scanning the QR code, the Credential Holder can then choose to share a credential, decline to share, or choose not to continue with the transaction.

Included in the proof request transaction, the Verifier Agent will provide the transaction’s current status to the LOB. This information can be provided due to the implementation of a polling process in which the LOB polls the Verifier Agent for the current status.

API polling is the process of sending continuous requests to the same endpoint and comparing the responses received to determine if the status of the transaction has changed (i.e. the Wallet has presented proof, declined, etc). Northern Block recommends that polling occurs every 5-10 seconds to determine if the Wallet Holder has presented the credential requested. The LOB can decide when the polling should be terminated and the transaction should be discontinued. If the transaction is discontinued, we recommend that the Wallet Holder be notified of this and given the opportunity to restart the credential exchange process.

As new information is presented by the Wallet Holder, the response status will change, per the State Diagram below.



<figure><img src="../../.gitbook/assets/proof-state-diagram.png" alt=""><figcaption></figcaption></figure>

{% openapi-operation spec="enterpriseapi-verifier" path="/api/lob/{lob_id}/proof-request/{cred_proof_id}" method="get" %}
[OpenAPI enterpriseapi-verifier](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/331b7c3100ddd55448b1badaba450b08f53a172d4f1d9ebc1b13438fec9fe950.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250703%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250703T134428Z&X-Amz-Expires=172800&X-Amz-Signature=b8f46165757a3d4a2addfbe635a680bbf3ac50ab77c82bff9989b6d0937ba77f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

