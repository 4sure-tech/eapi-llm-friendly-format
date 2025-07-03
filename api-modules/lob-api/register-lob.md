# Register LOB

The _**Register LOB API**_ registers your Line of Business, or LOB, with the Northern Block Orbit Enterprise API. After a successful POST request, you will receive a Transaction ID and an API Key via email. The response status code should be 201 (Created) or a relevant success code. See other codes [here](../../additional-information/http-codes.md).

&#x20;\
**Steps for Registering Your LOB**

1. Registration request initiated.
2. A Northern Block Admin will review and approve / reject the registration request.
3. The status of the LOB request is updated.
4. If the LOB is approved, a Transaction ID and an API Key is sent to the LOB Requestor via email.\


\*NOTE: Please refer to the [Supported Ledgers](../../additional-information/supported-ledgers.md) page for additional information.



{% openapi-operation spec="enterpriseapi-lob" path="/api/lob/register" method="post" %}
[OpenAPI enterpriseapi-lob](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/107c5bc2628d39f58c94b4bc9e6cfc13dd3c9aab011a8013320eab67aba430b3.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250703%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250703T134427Z&X-Amz-Expires=172800&X-Amz-Signature=5809897210b2f82a425973089eb1542a643229463086f92fca23084d4085af18&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

\
