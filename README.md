# php-cert-api
This Api provide you create, validate and sign documents through OpenSSL

## Prerequisites

* Apache 2.4.7
* PHP
* OpenSSL

## Supported Platforms

* Windows
* Linux

## Web Service to use the Api
Through any language, connect to the next server

    http://gohmo.cloudapp.net:8080/api-cert.php

Send infomation through POST method.

    HTTP Method: POST

Send JSON parameters.

##### Create certificate
In order to create certificates throgh this api, you need to send information in POST method with the next json data:

```javascript
 {  
    "action":"create-certificate",
    "countryName":"MX",
    "stateOrProvinceName":"SONORA",
    "localityName":"HERMOSILLO",
    "organizationName":"QUANTUMBIT",
    "commonName":"JESUS ALBERTO ABOYTIA",
    "emailAddress":"jesus.aboytia@quantumbit.com",
    "userID":"AOFJ870922JG4",
    "PassPhrase":"Control#001"
 }
```
The action that will permit you create certificates has the name "create-certificate". It has some parameters that it needs to create the files that contains certificate, private and public keys.

The parameters that you need to send are the next:

| Call Parameter  | Mandatory | Description |
| ------------- | ------------- | ------------- |
| action  | Yes  | This parameter contains the action that will do the Api. In this case the action is create a certificate with public and private keys  |
| action  | Yes  | This parameter contains the action that will do the Api. In this case the action is create a certificate with public and private keys  |
| action  | Yes  | This parameter contains the action that will do the Api. In this case the action is create a certificate with public and private keys  |
| action  | Yes  | This parameter contains the action that will do the Api. In this case the action is create a certificate with public and private keys  |
| action  | Yes  | This parameter contains the action that will do the Api. In this case the action is create a certificate with public and private keys  |
| action  | Yes  | This parameter contains the action that will do the Api. In this case the action is create a certificate with public and private keys  |
| action  | Yes  | This parameter contains the action that will do the Api. In this case the action is create a certificate with public and private keys  |
| action  | Yes  | This parameter contains the action that will do the Api. In this case the action is create a certificate with public and private keys  |
| action  | Yes  | This parameter contains the action that will do the Api. In this case the action is create a certificate with public and private keys  |




