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
    "stateOrProvinceName":"STATE",
    "localityName":"CITY",
    "organizationName":"COMPANY",
    "commonName":"NAME OR ALIAS",
    "emailAddress":"MAIL",
    "userID":"USER ID FOR OTHER APLICATIONS OR SYSTEMS",
    "PassPhrase":"PASSWORD FOR PRIVATE KEY"
 }
```
The action that will permit you create certificates has the name "create-certificate". It has some parameters that it needs to create the files that contains certificate, private and public keys.

The parameters that you need to send are the next:

| Call Parameter  | Mandatory | Description |
| ------------- | ------------- | ------------- |
| action  | Yes  | This parameter contains the action that will do the Api. In this case the action is create a certificate with public and private keys  |
| countryName  | Yes  | This parameter needs to be the name of country in two characteres. Is not permitted more than two Characteres. This parameter is to identify the country for the final user by certificate  |
| stateOrProvinceName  | Yes  | This parameter is to describe the state that the final user will be identify by certificate  |
| localityName  | Yes  | This parameter is to describe the city that the final user will be identify by certificate  |
| organizationName  | Yes  | This parameter is to describe the organization that the final user will be identify by certificate  |
| commonName  | Yes  | This parameter is to describe the name or alias that the final user will be identify by certificate  |
| emailAddress  | Yes  | This parameter is to describe the mail that the final user will be identify by certificate  |
| userID  | Yes  | This parameter is to create the certificate, public key and private key in files with the name of user id of other systems in order to create a link between them  |
| PassPhrase  | Yes  | This parameter is to assign a password for private key that will be created  |

Once the information was sended to the api, it will send you the next structure.

```javascript
{
  "data": {
    "private-key": "The string for private key encrypted",
    "public-key": "The string for public key",
    "certificate": "The string for certificate",
  },
  "health": {
    "status": "success",
    "descriptionStatus": ""
  }
}
```

About Data information:

| Callback Health  | Description |
| ------------- | ------------- |
| data.private-key  | This callback variable returns the string for private key encrypted  |
| data.public-key  | This callback variable returns the string for public key  |
| data.certificate  | This callback variable returns the string for certificate in pem format  |

About Health information:

| Callback Health  | Description |
| ------------- | ------------- |
| health.status  | This callback variable returns if the action was executed correctly or not. It only can be success or error  |
| health.descriptionStatus  | This callback variable returns in blank always the status is 'success', if the status is 'error' this will have the description about the issue  |

About health.descriptionStatus information:

| Callback health.status  | Description |
| ------------- | ------------- |
| success  | The description always will be empty  |
| error  | Parameter countryName must be two letters  |
| error  | Missing required parameters, please check documentation about this Api  |
| error  | You do not have permissions to see this content  |
