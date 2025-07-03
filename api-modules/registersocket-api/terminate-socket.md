# Terminate Socket

_**Terminate Socket**_ is a socket event and is called by the LOB's front-end application to terminate or close the established web socket the client has established with Orbit Enterprise API. This event can occur due to various reasons, including normal termination by the application, errors, or network issues. Please note that no API is called, this is handled by the socket package and is called automatically when the socket is disconnected.\


Common Scenarios for Socket Termination:

*   **Normal Termination**

    * Application-initiated closure (e.g., when a user logs out or a task completes)
    * Timeout: If a socket remains idle for a specified period, the server may terminate it


* **Forced Termination**
  * By a network administrator (e.g., to troubleshoot issues or enforce security policies)\

* **Error Conditions**
  * Network failures (e.g., link failure, congestion)
  * Protocol violations (e.g., invalid data format)
  * Application-specific errors (e.g., authentication failure, resource exhaustion)\


