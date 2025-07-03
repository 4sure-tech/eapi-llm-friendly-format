# Verifier Mobile Application Interacts With Mobile Wallet

Northern Block’s Digital Credential Verification API solution enables the sharing and verification of standards-based digital credentials within third-party applications. One such use case involves IATA’s One ID initiative, which will use digital identity to enable passengers to share credentials, such as proof of Frequent Flyer status, with airlines.\


Owners, or holders, of these digital credentials can store their credentials locally in digital identity wallets and present them to any third-party that accepts those types of credentials, removing the need for call-homes to verify the credentials’ authenticity. This offers enormous privacy-preserving benefits for the holders of credentials, while allowing relying parties to digitally transform business processes, since high-integrity data can now be easily consumed.\


The diagram below will detail the steps of this use case including those of the Line of Business’ (the Organization) Verifier Mobile Application, the Orbit Verifier APIs used in the process, and the Mobile Wallet/Credential Holder.\


<figure><img src="../.gitbook/assets/Screenshot 2024-08-30 at 12.57.49 PM.png" alt=""><figcaption></figcaption></figure>

One example of the verification process using the detailed steps above involves an airline passenger who is checking in for a flight online, via an airline’s mobile application. During this online check in process, the airline requires authentic and untampered information from the airline passenger and can verify the passenger’s digital credentials as proof of identity. After consuming the credential, the airline can then store this data or use it to populate other applications based on the organization’s business processes. Information pulled from the digital credential will then become non-editable, ensuring privacy and data integrity.\
\
The participants included in the above interaction are:

* Holder / Airline Passenger: An airline passenger who holds a Frequent Flyer Status credential issued by the Airline.
* LOB’s Verifier Mobile App: A Line of Business, in this case the Airline, who would like to streamline business processes by consuming an airline passenger’s credential, in this case the Frequent Flyer status. The LOB will consume the Holder’s credential using a mobile application.
* Mobile Wallet: The Holder’s mobile wallet that holds digital credentials.
* Orbit Verifier API: The Northern Block technology that enables interaction between the above participants. The Verifier API only interacts with the Holder and the LOB’s Verifier Mobile App during the transaction. Beyond the life-cycle of the transaction, the Verifier Agent maintains no information about the Holder or the LOB’s Verifier Mobile App and cannot initiate any transactions.\
