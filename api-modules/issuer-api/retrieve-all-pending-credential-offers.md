# Retrieve All Pending Credential Offers

The _**Retrieve All Credential Offers API**_ enables the LOB to retrieve all pending credential offers that have been sent. The credential offers will be returned with their most recent state that has been issued, along with the date of time of the most recent state.

Pending credential offers will be listed in chronological order, with the credential offer whose state was most recently created/updated at the top of the list.

The status values returned can be:

* offer-sent
* request-received
* credential-issued
* done

{% openapi-operation spec="enterpriseapi-issuer" path="/api/lob/{lob_id}/offers" method="get" %}
[OpenAPI enterpriseapi-issuer](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/72a00ed1d7027de054a3d66fdb14c2a1143e4d0d4abb61fad19279cb38abda44.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250703%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250703T134428Z&X-Amz-Expires=172800&X-Amz-Signature=319a189a033824aaed9afc04ff1830e8c3bb9c640f04f2ae6a5253543a5c6870&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}





