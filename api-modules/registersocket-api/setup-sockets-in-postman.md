# Setup Sockets In Postman

### Follow the steps below to setup a socket connection using Postman.

#### Step 1:

Click on "New Collection"

<figure><img src="../../.gitbook/assets/image 1.png" alt=""><figcaption></figcaption></figure>

#### Step 2:

Select socket.io

<figure><img src="../../.gitbook/assets/image 2.png" alt=""><figcaption></figcaption></figure>

#### Step 3:

Add the EAPI Socket base URL in the address bar and hit the _Connect_ button.

<figure><img src="../../.gitbook/assets/image 3.png" alt=""><figcaption></figcaption></figure>

#### Step 4:

In the _Message_ section, add the `lobID`.

<figure><img src="../../.gitbook/assets/image 4.png" alt=""><figcaption></figcaption></figure>

#### Step 5:

Select the event as _REGISTER\_SOCKET_.

<figure><img src="../../.gitbook/assets/image 5.png" alt=""><figcaption></figcaption></figure>

#### Step 6:

Go to the _Events_ tab and ensure that all socket events are enabled to receive events from the server. Make sure the _Event Listen_ toggle is turned on.

1. REGISTER\_SOCKET\_RESPONSE
2. CONNECTION\_RESPONSE
3. ISSUANCE\_RESPONSE
4. VERIFICATION\_RESPONSE

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

#### Step 7:

Lastly, go to the _Message_ tab, ensure that you have entered the `lobID` as shown in the image below, and hit _Send_. Your lob is now connected with the socket server.

<figure><img src="../../.gitbook/assets/image 7.png" alt=""><figcaption></figcaption></figure>













