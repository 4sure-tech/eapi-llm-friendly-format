# Prepare URL for Connection Invitation

The _**Prepare URL for Connection Invitation API**_ is called to prepare a connection invitation as a URL. The URL is then returned to the LOB, who can use the URL in the way that best meets business needs. For example, the URL can be emailed to a recipient or can be posted on a website to be scanned.\
\
The invitation is prepared based on AIP 2.0 protocol. \
\


{% openapi src="../../.gitbook/assets/swagger-spec-connection.json" path="/api/lob/{lob_id}/oob/prepare-url-invitation" method="post" %}
[swagger-spec-connection.json](../../.gitbook/assets/swagger-spec-connection.json)
{% endopenapi %}





