# Register Socket

The _**Register Socket API**_ is a socket event and is called by the LOB's front-end application to register and establish a web socket connection with the Orbit Enterprise API. This web socket is used by Orbit Enterprise API to notify the LOB's front-end application of relevant events.&#x20;

The client should add the [socket.io](http://socket.io/) library to register the socket with Orbit Enterprise API.

```
import { io } from 'socket.io-client';

// "undefined" means the URL will be computed from the `window.location` object
const URL = process.env.NODE_ENV === 'production' ? undefined : 'https://devapi-register-socket.nborbit.ca';

export const socket = io(URL);

io.on('connection', (socket) => {
  console.log('a user connected');
});

io.emit('REGISTER_SOCKET', (<lob_id: string>) => {
  console.log('Request for registering socket.')
});

io.on('REGISTER_SOCKET_RESPONSE', (<Response Body>) => {
    "success": true,
    "lobId": "316fe5e0-0738-4117-b9ce-00b3fd954c6d",
    "socketId": "ZOoOYEyBpZj7haV8AAAH",
    "message": "socket successfully registered"
});

```

**Base URL:** As per the base URL of NB Orbit Enterprise API environment (Refer to the sub-section Endpoints in this section below)

**Message (request body):**

* lob\_id

**Event Name**:

REGISTER\_SOCKET

**Response body:**

```
{
    "success": true,
    "lobId": "316fe5e0-0738-4117-b9ce-00b3fd954c6d",
    "socketId": "ZOoOYEyBpZj7haV8AAAH",
    "message": "socket successfully registered"
}
```
