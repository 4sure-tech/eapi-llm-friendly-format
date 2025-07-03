# Create Schema Draft

The _**Create Schema Draft API**_ enables the LOB to create and register a new schema on a public registry. Schema details to be included are name, version, credential format, attribute details, as well as a governance URL.&#x20;

The LOB may decide to create and save or create and register the schema on a public registry using this API. If the LOB wishes to register the schema at a future point in time, the _**Register Draft Schema API**_ will be used.\
\


{% openapi-operation spec="enterpriseapi-credential-management" path="/api/lob/{lob_id}/schema/draft" method="post" %}
[OpenAPI enterpriseapi-credential-management](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/857b5f5066c243a265a913bb8ab9da6f1ca46443a1cf17ecd20a117e8aef2599.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250703%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250703T134427Z&X-Amz-Expires=172800&X-Amz-Signature=6a8b8917665c43ebcda75e5ca8011d2b46b4a3363844b693bcbfc65cab13680a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}





