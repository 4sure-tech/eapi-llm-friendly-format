# Emit Socket Event

The _**Emit Socket Event API**_ is called by Orbit Enterprise API to send payloads to the LOB's front-end application over the established web socket. Please note that this is an internal API called by the _Notify API_ and no external API will call the _Emit Socket Event_ API.

Events are emitted by the _Notify API_ during the following interactions between two parties:

* Establishing connections between two parties
* Issuance of verifiable credentials
* Verification of verifiable credentials

\
Note: Both parties have to register a socket to receive relevant notifications.\
\
In the above three events, the notification response payload data structure is:

```json
{   
     "payloadType": enum,
     "payload": {}
}
```

### Establishing Connections Between Two Parties

When establishing a connection between two parties, the Invited and the Inviter receive a notification.

The notification response payload data structure received by both parties is:

```json
{    
     "payloadType": enum,
     "payload": {
                    "contactId": string,
                    "state": string,
                    "message": string
               }
}
```

The Inviter (Faber) receives notification during the following events:&#x20;

<table><thead><tr><th width="130.77081298828125">Event Recipient</th><th width="200.4305419921875">Event</th><th>Description</th></tr></thead><tbody><tr><td>Inviter</td><td>accepted-invitation</td><td>Invitation accepted by Invited</td></tr></tbody></table>

\
\
**You will find examples below of notification responses received by the Inviter.**\
\
1\. When the Invited has accepted the invitation:

<pre class="language-json"><code class="lang-json">{    
<strong>     "payloadType": "CONNECTION_RESPONSE",
</strong>     "payload": {
                    "contactId": "843adb07-c0f3-4ad2-b08a-7680fe7eed8f",
                    "state": "accepted-invitation",
                    "message": "You are now connected to Alice"              
               }
}
</code></pre>



2. When the Invited has declined the invitation:

```json
{    
     "payloadType": "CONNECTION_RESPONSE",
     "payload": {
                    "contactId": "843adb07-c0f3-4ad2-b08a-7680fe7eed8f",
                    "state": "declined-invitation",
                    "message": "Alice has declined your connection invitation"              
               }
}
```

The Invited (Alice) receives notification during the following events:&#x20;

<table><thead><tr><th width="141.9383544921875">Event Recipient</th><th width="204.94873046875">Event</th><th>Description</th></tr></thead><tbody><tr><td>Invited</td><td>received-invitation</td><td>Invitation received by Invited</td></tr></tbody></table>

\
**You will find an example below of a notification response received by the Invited.**\
\
1\. When a connection invitation has been received from the Inviter:

```json
{    
     "payloadType": "CONNECTION_RESPONSE",
     "payload": {
                    "contactId": "843adb07-c0f3-4ad2-b08a-7680fe7eed8f",
                    "state": "received-invitation",
                    "message": "You have received an invitation from Faber"              
               }
}
```

### Issuance of Verifiable Credentials

During the issuance of verifiable credentials, the credential Issuer and credential Holder receive notifications.\
\
The notification response payload data structure received by the Issuer and Holder is:

```json
{    
     "payloadType": "ISSUANCE_RESPONSE",
     "payload": {
        "credOfferId": string,
        "credentialStatus": string,
        "contactDetail": "{
           "contactId": string,
           "givenName": string,
           "email": string,
           "phone": string,
           "logo": string,
           "state": string,
           "createdAt": date,
           "updatedAt": date
       }
    }
}
```

The credential Issuer receives notification during the following events:

<table><thead><tr><th width="174.58587646484375">Event Recipient</th><th width="192.002685546875">Event</th><th>Description</th></tr></thead><tbody><tr><td>Credential Issuer</td><td>credential-issued</td><td>Issuer has offered a credential to the Holder</td></tr><tr><td>Credential Issuer</td><td>credential-accepted</td><td>Holder has accepted the credential offer by the Issuer</td></tr><tr><td>Credential Issuer</td><td>stored-in-wallet</td><td>Credential is stored in the Holder's wallet</td></tr></tbody></table>



**You will find an example below of the notification response received by the Issuer.**\
\
1\. When the credential is stored in the holder’s wallet:

```json
{    
     "payloadType": "ISSUANCE_RESPONSE",
     "payload": {
        "credOfferId": "EJTPoBll5jgl6okglkkklli48T",
        "credentialStatus": "stored-in-wallet",
        "contactDetail": "{
           "contactId": "56d501ce-2bec-4433-89a1-93b7ee820987",
           "givenName": "Alice Agent",
           "email": null,
           "phone": null,
           "logo": null,
           "state": "active",
           "createdAt": "2025-04-02T13:57:47.124Z",
           "updatedAt": "2025-04-02T13:59:13.931Z"
       }
    }
}

```

The credential Holder receives notification during the following events:&#x20;

<table><thead><tr><th width="179.681396484375">Event Recipient</th><th width="171.02685546875">Event</th><th>Description</th></tr></thead><tbody><tr><td>Credential Holder</td><td>offer-received</td><td>Holder has received a credential offer from the Issuer</td></tr><tr><td>Credential Holder</td><td>credential-revoked</td><td>Issuer has revoked the credential issued to the Holder</td></tr><tr><td>Credential Holder</td><td>done</td><td>Credential is stored in the Holder's wallet</td></tr></tbody></table>



**You will find an example below of the notification responses received by the credential Holder.**\
\
1\. When a Holder has received a credential offer from the Issuer:

```json
{
    "payloadType": "ISSUANCE_RESPONSE",
     "payload": {
        "credOfferId": "EJTPoBll5jgl6okglkkklli48T",
        "credentialStatus": "offer-received",
        "contactDetail": "{
           "contactId": "56d501ce-2bec-4433-89a1-93b7ee820987",
           "givenName": "Alice Agent",
           "email": null,
           "phone": null,
           "logo": null,
           "state": "active",
           "createdAt": "2025-04-02T13:57:47.124Z",
           "updatedAt": "2025-04-02T13:59:13.931Z"
        }
    }
}
```

### Verification of Verifiable Credentials

During the verification of verifiable credentials, the credential Verifier and credential Holder receive notifications.\
\
The notification response payload data structure received by the Verifier and Holder is:

```json
{    
     "payloadType": "VERIFICATION_RESPONSE",
     "payload": {
        "credProofId": string,
        "proofRequestStatus": string,
        "contactDetail": "{
           "contactId": string,
           "givenName": string,
           "email": string,
           "phone": string,
           "logo": string,
           "state": string,
           "createdAt": date,
           "updatedAt": date
        }
    },
    "verified": string
}
```

The credential Verifier receives notification during the following events:&#x20;

<table><thead><tr><th width="181.64752197265625">Event Recipient</th><th width="213.078125">Event</th><th>Description</th></tr></thead><tbody><tr><td>Credential Verifier</td><td>request-sent / generated</td><td>Verifier has requested the credential Holder to share verifiable credentials</td></tr><tr><td>Credential Verifier</td><td>proof-received</td><td>Verifier has received the verifiable credential shared by the Holder</td></tr><tr><td>Credential Verifier</td><td>success / revoked</td><td>Verifier has verified the verifiable credential shared by the Holder</td></tr></tbody></table>



**You will find examples below of the notification responses received by the Verifier.**\
\
1\. When the Verifier has requested the Holder to share a verifiable credential:

```json
{    
     "payloadType": "VERIFICATION_RESPONSE",
     "payload": {
        "credProofId": "58e02kljkdk58i",
        "proofRequestStatus": "request-sent",
        "contactDetail": {
           "contactId": "843adb07-c0f3-4ad2-b08a-7680fe7eed8f",
           "givenName": "Alice Agent",
           "email": null,
           "phone": null,
           "logo": null,
           "state": "active",
           "createdAt": "2025-04-02T13:17:48.988Z",
           "updatedAt": "2025-04-02T13:21:32.976Z"
        },
        "ledgerName": "bcCovrinTest"
    }
    "verified": "null"
}
```

2. When the Verifier has verified the credential shared by the credential Holder:

```json
{     
     "payloadType": "VERIFICATION_RESPONSE",
     "payload": {
        "credProofId": "58e02kljkdk58i",
        "proofRequestStatus": "success",
        "contactDetail": {
          "contactId": "843adb07-c0f3-4ad2-b08a-7680fe7eed8f",
          "givenName": "Alice Agent",
          "email": null,
          "phone": null,
          "logo": null,
          "state": "active",
          "createdAt": "2025-04-02T13:17:48.988Z",
          "updatedAt": "2025-04-02T13:21:32.976Z"
        },
        "ledgerName": "bcCovrinTest"
    },
    "verified": "true"
}
```

The credential Holder receives notification during the following events:

<table><thead><tr><th width="169.42535400390625">Event Recipient</th><th width="204.6336669921875">Event</th><th>Description</th></tr></thead><tbody><tr><td>Credential Holder</td><td>presentation-requested</td><td>Holder has received a request to share credential with the Verifier</td></tr></tbody></table>

\
**You will find an example below of the notification response received by a credential Holder.**\
\
1\. When a Holder has received a request to share credentials with a Verfier:

```json
{
     "payloadType": "VERIFICATION_RESPONSE",
     "payload": {
        "credOfferId": "EJTPoBll5jgl6okglkkklli48T",
        "credentialStatus": "presentation-requested",
        "contactDetail": {
           "contactId": "56d501ce-2bec-4433-89a1-93b7ee820987",
           "givenName": "Alice Agent",
           "email": null,
           "phone": null,
           "logo": null,
           "state": "active",
           "createdAt": "2025-04-02T13:57:47.124Z",
           "updatedAt": "2025-04-02T13:59:13.931Z"
        },
        "ledgerName": "bcCovrinTest"
    }
    "verified": "null"
}
```





