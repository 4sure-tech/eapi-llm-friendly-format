# What is a Socket?

A socket is an endpoint for sending or receiving data across a computer network. It acts as a communication channel between two machines or processes, allowing them to exchange data over protocols like TCP/IP (Transmission Control Protocol/Internet Protocol) or UDP (User Datagram Protocol). Here’s a deeper look into what sockets are and how they work:

### Key Concepts of Sockets

Socket Types:

* Stream Sockets (TCP): These use the Transmission Control Protocol (TCP) for reliable, connection-oriented communication. They ensure that data packets arrive in order and without errors.
* Datagram Sockets (UDP): These use the User Datagram Protocol (UDP) for connectionless communication. They are faster but do not guarantee the delivery, order, or integrity of the packets.

Components of a Socket:

* IP Address: Identifies a machine on a network.
* Port Number: Identifies a specific process or service on the machine. Each service (like HTTP, FTP, etc.) typically uses a specific port number.
* Together, the IP address and port number form a socket address (e.g., 192.168.1.10:80).

Client-Server Model:

* In a typical client-server architecture, one socket acts as the server socket that listens for incoming connections, while one or more client sockets initiate connections to the server. Once a connection is established, they can send and receive data.

Socket Lifecycle:

* Creation: A socket is created using system calls provided by programming languages (e.g., socket() in Python or C).
* Binding: A server binds its socket to a specific IP address and port to listen for incoming connections.
* Listening: The server socket listens for incoming connection requests.
* Accepting: When a client requests a connection, the server accepts it, establishing a connection between the two sockets.
* Communication: Data can then be exchanged between the client and server through the sockets.
* Closing: Once the communication is complete, the sockets are closed.

### Example Use Cases

* Web Servers: A web server uses sockets to listen for HTTP requests from clients (web browsers). When a request is received, it processes it and sends back the appropriate response.
* Chat Applications: Chat applications use sockets to establish real-time communication between users.
* File Transfer Protocol (FTP): FTP servers use sockets to transfer files between clients and servers.
