# What are GET & POST Methods?

The **GET** and **POST** methods are two of the most commonly used HTTP methods in REST APIs. Here’s a breakdown of each:

***

### GET Method

Purpose: The GET method is used to retrieve data from a server.

\
Characteristics:

* Safe: Since it only requests data, it doesn’t modify or affect any data on the server.
* Idempotent: Calling the same GET request multiple times will always produce the same result without side effects.
* URL-based: Data is sent to the server through the URL, often using query parameters to filter or customize the data (e.g., /products?category=books).
* Caching: GET requests can be cached by the browser, which can improve performance for frequently accessed data.\


Example:

* Request: GET /products/123
* Purpose: This retrieves product details with the ID 123.



### POST Method

Purpose: The POST method is used to send data to the server, often to create a new resource or submit data for processing.

Characteristics:

* Not Idempotent: Calling the same POST request multiple times may create multiple resources or cause multiple actions (e.g., adding the same product multiple times).
* Body-based: Unlike GET, the data is sent in the request body rather than the URL, which allows for sending complex and secure data.
* No Caching: POST requests are typically not cached since they often change server data.\


Example:

* Request: POST /products
* Request Body: { "name": "Laptop", "price": 1200, "category": "electronics" }
* Purpose: This creates a new product with the given details.

***



### Comparison of GET and POST

| **Feature**   | **GET**                       | **POST**                                 |
| ------------- | ----------------------------- | ---------------------------------------- |
| Purpose       | Retrieve data from the server | Send data to the server to create/submit |
| Data Location | In the URL (query parameters) | In the request body                      |
| Caching       | Can be cached                 | Typically not cached                     |
| Safe          | Yes                           | No                                       |
| Idempotent    | Yes                           | No                                       |



### When to Use GET vs. POST

* Use GET when you need to fetch or retrieve data without affecting any server state.
* Use POST when you need to send new data, create a resource, or submit a form with potentially sensitive data.

This distinction is important in RESTful API design, ensuring data integrity and proper use of server resources.
