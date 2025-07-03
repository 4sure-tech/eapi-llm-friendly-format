# Import An External Credential Definition

The _**Import An External Credential Definition API**_ enables the LOB to import, into the Orbit Enterprise API, a single credential definition that has been created by a third party and registered on the public registry. This will include all details related to the credential definition. \
\
By importing an external credential definition, a Verifier on the Orbit Enterprise environment can use that credential definition to create proof requests.

{% openapi-operation spec="enterpriseapi-credential-management" path="/api/lob/{lob_id}/cred-def/store" method="post" %}
[OpenAPI enterpriseapi-credential-management](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/857b5f5066c243a265a913bb8ab9da6f1ca46443a1cf17ecd20a117e8aef2599.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250703%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250703T134427Z&X-Amz-Expires=172800&X-Amz-Signature=6a8b8917665c43ebcda75e5ca8011d2b46b4a3363844b693bcbfc65cab13680a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
