# What are Rest APIs?

**REST** (Representational State Transfer) is an architectural style for designing networked applications. REST APIs (Application Programming Interfaces) follow REST principles to allow systems to communicate over the web by enabling applications to read, create, update, and delete resources in a server.

***

### Key Concepts of REST APIs

\
**- Resources**

* A resource is an object or data that the API exposes to clients, such as a user profile, blog post, or product information. Each resource is identified by a URL (Uniform Resource Locator).
* Example: In a blogging platform API, a blog post might have the URL /posts/123, where /posts is the endpoint, and 123 is the ID for a specific post.



**- HTTP Methods**

* REST APIs rely on standard HTTP methods to perform actions on resources. Here’s a summary of the main HTTP methods used:
  * GET: Retrieves data from the server without modifying it.
  * POST: Sends data to the server, often to create a new resource.
  * PUT: Updates an existing resource with new data.
  * DELETE: Removes a resource from the server.

\
**- Statelessness**

* In REST, each request from the client to the server must contain all the information needed to understand and process the request. This makes the server stateless, meaning it does not retain client information between requests.

\
\- **JSON and XML**

* REST APIs typically use JSON (JavaScript Object Notation) as the data format because it is lightweight and easy to parse. However, XML can also be used.

\
\- **Status Codes**

* Each API response includes an HTTP status code to inform the client about the result of the request:
  * 200 OK: Success.
  * 201 Created: New resource was created.
  * 400 Bad Request: Client error in the request.
  * 401 Unauthorized: Authentication required.
  * 404 Not Found: Resource not found.
  * 500 Internal Server Error: Server encountered an error.
