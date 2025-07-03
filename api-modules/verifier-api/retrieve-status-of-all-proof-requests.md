# Retrieve Status of All Proof Requests

The _**Retrieve Status of All Proof Requests API**_ retrieves all proof requests that have been sent to a Wallet, or Credential Holder, but the Holder has not yet responded with either a decline or a credential presentation. The proof requests are listed in chronological order, with the proof request whose state was created/updated most recently appearing at the top if the list. \
\
If you include a specific 'state' in the Request Body, you can also retrieve all pending proof requests that match only the state(s) you included.&#x20;

Descriptions of each state are included below:

* generated: Indicates that the proof request has been created and shared with the requesting LOB
* scanned: QR code has been scanned by the holder’s wallet
* proof-recd: Proof has been received by the Verifier Agent from the holder’s wallet
* success: Verification of the proof shared by the holder’s wallet has been successfully verified by the Verifier Agent.
* revoked: Verification of the proof shared by the holder’s wallet has failed as the credential shared by the holder has been revoked by the Issuer.
* verification-failed: Verification of the proof shared by the holder’s wallet failed due to an error.\




{% openapi-operation spec="enterpriseapi-verifier" path="/api/lob/{lob_id}/proof-requests" method="get" %}
[OpenAPI enterpriseapi-verifier](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/331b7c3100ddd55448b1badaba450b08f53a172d4f1d9ebc1b13438fec9fe950.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250703%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250703T134428Z&X-Amz-Expires=172800&X-Amz-Signature=b8f46165757a3d4a2addfbe635a680bbf3ac50ab77c82bff9989b6d0937ba77f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}





