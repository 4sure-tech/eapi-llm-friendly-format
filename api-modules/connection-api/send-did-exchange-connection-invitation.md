# Send DID-Exchange Connection Invitation

The _**Send DID-Exchange Connection Invitation API**_ enables the LOB to send a DID Exchange-based connection invitation to a peer. This API can only be used if the LOB knows the public DID of the recipient. The connection invitation is prepared based on AIP 2.0 protocol.\


{% openapi src="../../.gitbook/assets/swagger-spec-connection.json" path="/api/lob/{lob_id}/did-exchange/invitation" method="post" %}
[swagger-spec-connection.json](../../.gitbook/assets/swagger-spec-connection.json)
{% endopenapi %}



