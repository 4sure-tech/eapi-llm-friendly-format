# Create LOB

The _**Create LOB API**_ is used to spin-up an agent for your LOB. During the spin-up of the agent, the API will also create a Wallet and DID for the LOB. Successful registration of the LOB, with a Transaction ID, is a prerequisite before using this API. Upon successful spin-up of the agent, the API will email you the LOB ID for the LOB.\
\
**Steps for Creating Your LOB**

1. The LOB Requestor calls the LOB Create API using the provided Transaction ID.&#x20;
2. Agent for the LOB is started.
3. Upon a successful API call, the LOB ID will be sent via email.

\


{% openapi-operation spec="enterpriseapi-lob" path="/api/lob/create" method="post" %}
[OpenAPI enterpriseapi-lob](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/107c5bc2628d39f58c94b4bc9e6cfc13dd3c9aab011a8013320eab67aba430b3.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250703%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250703T134427Z&X-Amz-Expires=172800&X-Amz-Signature=5809897210b2f82a425973089eb1542a643229463086f92fca23084d4085af18&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

\






\
