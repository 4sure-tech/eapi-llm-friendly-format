# Retrieve All Pending Connection Invitations

The _**Retrieve All Pending Connection Invitations API**_ is called to retrieve pending connection invitations. When calling this API, the following records can be retrieved:

1. All pending connection invitations that have been sent but the recipient has not responded, along with most recent state
2. All connection invitations that have been saved as drafts
3. All DID-Exchange connection requests that have been received from peers, along with date, time, and most recent state

Pending connection invitations will be listed in chronological order, with the invitation sent/received whose state was most recently created/updated at the top of the list.\


{% openapi src="../../.gitbook/assets/swagger-spec-connection.json" path="/api/lob/{lob_id}/pending-connections" method="get" %}
[swagger-spec-connection.json](../../.gitbook/assets/swagger-spec-connection.json)
{% endopenapi %}





