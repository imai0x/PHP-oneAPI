OneApi php client
============================
<p align="center">
 <img width="100px" src="https://res.cloudinary.com/anuraghazra/image/upload/v1594908242/logo_ccswme.svg" align="center" alt="GitHub Readme Stats" />
 <h2 align="center">GitHub Readme Stats</h2>
 <p align="center">Get dynamically generated GitHub stats on your readmes!</p>
</p>
<p align="center">
  <img src="https://img.shields.io/badge/Supported%20by-VS%20Code%20Power%20User%20%E2%86%92-gray.svg?colorA=655BE1&colorB=4F44D6&style=for-the-badge"/>
</p>

Basic messaging example
-----------------------

First initialize the messaging client using your username and password:

    $smsClient = new SmsClient(USERNAME, PASSWORD);


An exception will be thrown if your username and/or password are incorrect.

Prepare the message:

    $smsMessage = new SMSRequest();
    $smsMessage->senderAddress = SENDER_ADDRESS;
    $smsMessage->address = DESTINATION_ADDRESS;
    $smsMessage->message = 'Test message';


Send the message:

    $smsMessageSendResult = $smsClient->sendSMS($smsMessage);
    // The client correlator is a unique identifier of this api call:
    $clientCorrelator = $smsMessageSendResult->clientCorrelator;


Later you can query for the delivery status of the message:

    // You can use $clientCorrelator or $smsMessageSendResult as an method call argument here:
    $smsMessageStatus = $smsClient->queryDeliveryStatus($smsMessageSendResult);
    $deliveryStatus = $smsMessageStatus->deliveryInfo[0]->deliveryStatus;


Possible statuses are: **DeliveredToTerminal**, **DeliveryUncertain**, **DeliveryImpossible**, **MessageWaiting** and **DeliveredToNetwork**.

Messaging with notification push example
-----------------------

Same as with the standard messaging example, but when preparing your message:

    $smsMessage = new SMSRequest();
    $smsMessage->senderAddress = SENDER_ADDRESS;
    $smsMessage->address = DESTINATION_ADDRESS;
    $smsMessage->message = 'Test message';
    $smsMessage->notifyURL = NOTIFY_URL;


When the delivery notification is pushed to your server as a HTTP POST request, you must process the body of the message with the following code:

    $result = SmsClient::unserializeDeliveryStatus();


HLR example
-----------------------

Initialize and login the data connection client:

    $client = new DataConnectionProfileClient(USERNAME, PASSWORD);
    $client->login();


Retrieve the roaming status (HLR):

    $response = $client->retrieveRoamingStatus(DESTINATION_ADDRESS);


HLR with notification push example
-----------------------

Similar to the previous example, but this time you must set the notification url where the result will be pushed:

    $response = $client->retrieveRoamingStatus(DESTINATION_ADDRESS, NOTIFY_URL);


When the roaming status notification is pushed to your server as a HTTP POST request, you must process the body of the message with the following code:

    $result = DataConnectionProfileClient::unserializeRoamingStatus();


Retrieve inbound messages example
-----------------------

With the existing sms client (see the basic messaging example to see how to start it):

    $inboundMessages = $smsClient->retrieveInboundMessages();
    
    foreach($inboundMessages->inboundSMSMessage as $message) {
        echo $message;
    }


Inbound message push example
-----------------------

The subscription to recive inbound messages can be set up on our site.
When the inbound message notification is pushed to your server as a HTTP POST request, you must process the body of the message with the following code:

    $inboundMessages = SmsClient::unserializeInboundMessages();


License
-------

This library is licensed under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0)

## ???? Technologies and Frameworks
<p>
    <!-- PHP -->
    <img src="https://img.shields.io/badge/PHP-777bb4?flat=plastic&logo=php&logoColor=white" height="32" alt="PHP" />
    &nbsp;
    <!-- Shell -->
    <img src="https://img.shields.io/badge/Shell-ffd500?flat=plastic&logo=shell&logoColor=black" height="32" alt="Shell" />
    &nbsp;
</p>

