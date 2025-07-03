# Verify A Credential Presentation

The _**Verify API**_ enables the LOB to verify the credential presentation received from a Wallet, or Credential Holder, in response to a proof request. The Verify API call confirms that the credential presented by the Holder has not been tampered with and meets the restrictions placed on the proof request.\
\


{% openapi-operation spec="enterpriseapi-verifier" path="/api/lob/{lob_id}/proof/verify" method="post" %}
[OpenAPI enterpriseapi-verifier](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/331b7c3100ddd55448b1badaba450b08f53a172d4f1d9ebc1b13438fec9fe950.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250703%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250703T134428Z&X-Amz-Expires=172800&X-Amz-Signature=b8f46165757a3d4a2addfbe635a680bbf3ac50ab77c82bff9989b6d0937ba77f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
