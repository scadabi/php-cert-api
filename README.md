# php-cert-api
This Api provide you create, validate and sign documents through OpenSSL

## Prerequisites

* Apache 2.4.7
* PHP
* OpenSSL

## Supported Platforms

* Windows
* Linux

## Instalation
Clone this proyect by Git from the next URL

    https://github.com/scadabi/php-cert-api.git

## Web Service to use the Api
Through any language, connect to the next server

    http://gohmo.cloudapp.net:8080/api-cert.php

Send infomation through POST method.

    HTTP Method: POST

Send JSON parameters.

## Create certificate
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
    "PassPhrase":"PASSWORD FOR PRIVATE KEY",
    "daysToExpire":"Number of days that you want to be available"
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
| daysToExpire  | No  | This parameter is optional, it needs to be an integer value, that value represents the number of days that you want to be active, after that time the certificate will be expired. If you put a bad value (not integer) or you do not send it, it will be 360 days by default  |

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

### About Data information:

| Callback Health  | Description |
| ------------- | ------------- |
| data.private-key  | This callback variable returns the string for private key encrypted  |
| data.public-key  | This callback variable returns the string for public key  |
| data.certificate  | This callback variable returns the string for certificate in pem format  |

### About Health information:

| Callback Health  | Description |
| ------------- | ------------- |
| health.status  | This callback variable returns if the action was executed correctly or not. It only can be success or error  |
| health.descriptionStatus  | This callback variable returns in blank always the status is 'success', if the status is 'error' this will have the description about the issue  |

### About health.descriptionStatus information:

| Callback health.status  | Description |
| ------------- | ------------- |
| success  | The description always will be empty  |
| error  | Parameter countryName must be two letters  |
| error  | Missing required parameters, please check documentation about this Api  |
| error  | You do not have permissions to see this content  |

## Sign Document
In order to use our certificate, public and private key to sign a documen we need to send the next information to the api

```javascript
 {  
      "action":"sign-document",
      "documentType":"if is url or string",
      "private-key":"file name or string in pem format",
      "public-key":"file name or string in pem format",
      "documentInfo":"content document that you want to sign",
      "PassPhrase":"password for encryptation"
 }
```
The action that will permit you sign document has the name "sign-document". It has some parameters that it needs to sign the documen using your private and public keys.

The parameters that you need to send are the next:

| Call Parameter  | Mandatory | Description |
| ------------- | ------------- | ------------- |
| action  | Yes  | This parameter contains the action that will do the Api. In this case the action is sign a document with public and private keys  |
| documentType  | Yes  | This parameter is to identify what type of data will send in parameters private-key and public-key. It has only two options, those are the next: 'url' is to specify a name of certificate, always it is the ID of user from other systems or Apps. the other one is 'string' and that is to specify the string of public-key and private-key in pem format  |
| private-key  | Yes  | This parameter is to put the private-key. It can be string in pem format or filename depending of documentType parameter  |
| public-key  | Yes  | This parameter is to put the public-key. It can be string in pem format or filename depending of documentType parameter  |
| documentInfo  | Yes  | This parameter is to define the document that you want to sign  |
| passPhrase  | Yes  | This parameter is to put the password of your private-key  |

Once the information was sended to the api, it will send you the next structure.

```javascript
{
  "data": {
    "digital-sign": "The string of your base64 sign",
    "validation-result": "The document was signed and validate. The result was successfully"
  },
  "health": {
    "status": "success",
    "descriptionStatus": ""
  }
}
```

### About Data information:

| Callback Health  | Description |
| ------------- | ------------- |
| data.digital-sign  | This callback variable returns the string of your document signed  |
| data.validation-result  | This callback variable returns the text of the success result  |

### About Health information:

| Callback Health  | Description |
| ------------- | ------------- |
| health.status  | This callback variable returns if the action was executed correctly or not. It only can be success or error  |
| health.descriptionStatus  | This callback variable returns in blank always the status is 'success', if the status is 'error' this will have the description about the issue  |

### About health.descriptionStatus information:

| Callback health.status  | Description |
| ------------- | ------------- |
| success  | The description always will be empty  |
| error  | The document was validate and the result was unsuccessfully  |
| error  | Unknow value documentType, please check documentation about this Api  |
| error  | The passphrase that was sended does not match with the original encrypted passphrase or the private key file or content is invalid or does not exist  |
| error  | The public key file or content is invalid or does not exist  |
| error  | Missing required parameters, please check documentation about this Api  |
| error  | You do not have permissions to see this content  |

## Validate Document
In order to validate if the document was signed with an specific public key and certificate, you can send to the api the next structure:

```javascript
 {  
      "action":"validate-document",
      "documentType":"if is url or string",
      "signature":"this is to put the signature that you want to validate",
      "public-key":"file name or string in pem format",
      "documentToValidate":"content document that you want to compare with the signature"
 }
```

The action that will permit you validate a signature has the name "validate-document". It has some parameters that it needs to validate the documen using your public key.

The parameters that you need to send are the next:

| Call Parameter  | Mandatory | Description |
| ------------- | ------------- | ------------- |
| action  | Yes  | This parameter contains the action that will do the Api. In this case the action is validate a document with public  keys  |
| documentType  | Yes  | This parameter is to identify what type of data will send in parameter public-key. It has only two options, those are the next: 'url' is to specify a name of certificate, always it is the ID of user from other systems or Apps. the other one is 'string' and that is to specify the string of public-key and private-key in pem format  |
| signature  | Yes  | This parameter is to put the signature that you want to validate in base64 format  |
| public-key  | Yes  | This parameter is to put the public-key. It can be string in pem format or filename depending of documentType parameter  |
| documentToValidate  | Yes  | This parameter is to define the content of the document that you want to validate with signature  |

Once the information was sended to the api, it will send you the next structure.

```javascript
{
  "data": {
    "validation-result": "The document was validated successfully"
  },
  "health": {
    "status": "success",
    "descriptionStatus": ""
  }
}
```

### About Data information:

| Callback Health  | Description |
| ------------- | ------------- |
| data.validation-result  | This callback variable returns the text of the success result  |

### About Health information:

| Callback Health  | Description |
| ------------- | ------------- |
| health.status  | This callback variable returns if the action was executed correctly or not. It only can be success or error  |
| health.descriptionStatus  | This callback variable returns in blank always the status is 'success', if the status is 'error' this will have the description about the issue  |

### About health.descriptionStatus information:

| Callback health.status  | Description |
| ------------- | ------------- |
| success  | The description always will be empty  |
| error  | The document was validated successfully  |
| error  | Unknow value documentType, please check documentation about this Api  |
| error  | The public key file or content is invalid or does not exist  |
| error  | Missing required parameters, please check documentation about this Api  |
| error  | You do not have permissions to see this content  |

## Login using a certificate and private and public keys
In order to login a user using certificate and private and public keys you need to send the next information to the api.

```javascript
 {  
      "action":"login-user-with-signature",
      "documentType":"if is url or string",
      "private-key":"file name or string in pem format",
      "public-key":"file name or string in pem format",
      "PassPhrase":"password for encryptation"
 }
```
The action that will permit you login a user has the name "login-user-with-signature". It has some parameters that it needs to validate login using your private and public keys.

The parameters that you need to send are the next:

| Call Parameter  | Mandatory | Description |
| ------------- | ------------- | ------------- |
| action  | Yes  | This parameter contains the action that will do the Api. In this case the action is login a user with public and private keys  |
| documentType  | Yes  | This parameter is to identify what type of data will send in parameters private-key and public-key. It has only two options, those are the next: 'url' is to specify a name of certificate, always it is the ID of user from other systems or Apps. the other one is 'string' and that is to specify the string of public-key and private-key in pem format  |
| private-key  | Yes  | This parameter is to put the private-key. It can be string in pem format or filename depending of documentType parameter  |
| public-key  | Yes  | This parameter is to put the public-key. It can be string in pem format or filename depending of documentType parameter  |
| passPhrase  | Yes  | This parameter is to put the password of your private-key  |

Once the information was sended to the api, it will send you the next structure.

```javascript
{
  "data": {
    "login-result": "The user was validated successfully"
  },
  "health": {
    "status": "success",
    "descriptionStatus": ""
  }
}
```

### About Data information:

| Callback Health  | Description |
| ------------- | ------------- |
| data.login-result  | This callback variable returns the text of the success result  |

### About Health information:

| Callback Health  | Description |
| ------------- | ------------- |
| health.status  | This callback variable returns if the action was executed correctly or not. It only can be success or error  |
| health.descriptionStatus  | This callback variable returns in blank always the status is 'success', if the status is 'error' this will have the description about the issue  |

### About health.descriptionStatus information:

| Callback health.status  | Description |
| ------------- | ------------- |
| success  | The description always will be empty  |
| error  | Unknow value documentType, please check documentation about this Api  |
| error  | The passphrase that was sended does not match with the original encrypted passphrase or the private key file or content is invalid or does not exist  |
| error  | The public key file or content is invalid or does not exist  |
| error  | Missing required parameters, please check documentation about this Api  |
| error  | You do not have permissions to see this content  |
