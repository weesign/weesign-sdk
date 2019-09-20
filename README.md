
## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Usage Examples](#usage-examples)
  - [Create Access Token](#Create-Access-Token)
  - [Add New Document](#Add-New-Document)
  - [Update an existing Document](#Update-an-existing-Document)
  - [Delete Document](#Delete-Document)
  - [Get All document assiciated with a user](#Get-All-document-assiciated-with-a-user)
  - [Get a particular Document](#Get-All-document-assiciated-with-a-user)
  - [Add Signatory of a document](#Add-Signatory-of-a-document)
  - [Share a completed document through a mail](#Share-a-completed-document-through-a-mail)
  - [Validate Document](#Validate-Document)
  - [Add WebHook](#Add-WebHook)
  - [Update WebHook](#Update-WebHook)
  - [Get WebHook](#Get-WebHook)
  - [Delete WebHook](#Delete-WebHook)

## Features

- Create Access Token 
- Add New Document
- Update an existing Document
- Delete Document
- Get All document assiciated with a user
- Get a particular Document
- Add Signatory of a document
- Share a completed document through a mail
- Validate Document
- Add WebHook
- Update WebHook
- Get WebHook
- Delete WebHook


## Installation

```bash
# With npm
npm install --save @weesign/weesign-sdk

```


## Usage Examples

### Create Access Token

_This example Create Access Token._

<!-- prettier-ignore -->
```js
let weesign = require('weesign-sdk');

// data to be passed for create access token
let data = {
   'user-id':"avwxQxnm3sh5Y61WxRohhWmdZsb2",
   'api-key':"d5e6287a556a72ef9db209e1b878b8a6bghj2",
}

// where 'user-id' is userID of user and 'api-key' is a key used for using weesign
//'user-id' and 'api-key' can get using the following steps:
//   Sign up and login on https:www.weesign.mx and choose a subscription plan
//   Note userID and ApiKey from the profile section (if apiKey not available then you can Generate by   clicking on Generate API key button)

// Create access token
// (Note: this access token is valid up to 5 minutes)

let response = await demo.accessToken(data);

// and the reponse will be look like this
// { responseData: { accessToken: 'f1a664ea710062baae92bc59d5bd8560d2c4929b' },
//  message: 'Token generated Successfully',
//  success: true,
//  responseCode: 200 }

```

### Add New Document

_This example Add New Document._

<!-- prettier-ignore -->
```js
let weesign = require('weesign-sdk');

// data to be passed for Add New Document
let firstPath = path.normalize(__dirname + '/dummy.pdf');
     let file = await fs.createReadStream(firstPath);

let data = {
   'user-id':"avwxQxnm3sh5Y61WxRohhWmdZsb2",
   'token':"d5e6287a556a72ef9db209e1b878b8a6bghj2",
   'file':file,
   'documentSignType':"ELECTRONIC_SIGNATURE",
   'country':"Mexico",
   'language':"es"
};
// 'user-id' is userID of document Owner/Creater
// 'token' is acces token which is generated using accessToken()
// 'file' can be file Object or ReadStream Object
// 'documentSignType' Type of signature can be ELECTRONIC_SIGNATURE or E_FIRMA
// 'country' country  is country name For example Mexico, United States, Canada, New Zealand, Australia, Afghanistan, Aland Islands, Albania
// 'language' language for sending mail format in spanish or english. For spanish language is 'es' and For english language is 'en'

let response = await weesign.addDocument(data);


// and the reponse will be look like this
// { "responseData": {
//     "documentID": "5d4adeac1d6391bc05d13be",
//      "documentType": "OTHER",
//      "status": "DRAFT",
//      "country": "Mexico",
//      "documentSignType": "ELECTRONIC_SIGNATURE",
 //     "addedOn": 1565188066047,
 //     "documentFileObj": {
 //       "url": "https://signing-file.s3.amazonaws.com/sample.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIXB7WAVV4G_7T142236Z&X-Amz-Expires=518400&X-Amz-Signature=eb6938817d3e0be20c7ca23b16991fb90b6e65f9aabf22ca3d4d4f01a4548241&X-Amz-SignedHeaders=host",
  //      "size": "2.6 MB"
  //    },
  //    "signatory": []
  //  },
//  "message": "Document added successfully",
// "success": true,
//  "responseCode": 200
//}
```

### Update an existing Document

_This example for Update an existing Document._

<!-- prettier-ignore -->
```js
let weesign = require('weesign-sdk');

// Prerequisite: User needs to have a userID, access token and document should exit and status have DRAFT

// data to be passed for update Document
let data = {
   'user-id':"avwxQxnm3sh5Y61WxRohhWmdZsb2",
   'token':"d5e6287a556a72ef9db209e1b878b8a6bghj2",
   'documentID':"d5e6287a556a72ef9db209e1b",
   'documentSignType':"ELECTRONIC_SIGNATURE",
   'country':"United States",

}
// 'user-id' is userID of document Owner/Creater
// 'token' is acces token which is generated using accessToken()
// 'documentID' is Id of od document which to be update
// "documentSignType" is type of signature for sign the document. documentSignType either "ELECTRONIC_SIGNATURE" or "E_FIRMA"
// "country" is country name for example United States, Mexico etc
let reponse = await weesign.updateDocument(data);

// and the reponse will be look like this
// { "responseData": {
//     "documentID": "5d4adeac1d6391bc05d13be",
//      "documentType": "OTHER",
//      "status": "DRAFT",
//      "country": "United States",
//      "documentSignType": "ELECTRONIC_SIGNATURE",
 //     "addedOn": 1565188066047,
 //     "documentFileObj": {
 //       "url": "https://signing-file.s3.amazonaws.com/sample.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIXB7WAVV4G_7T142236Z&X-Amz-Expires=518400&X-Amz-Signature=eb6938817d3e0be20c7ca23b16991fb90b6e65f9aabf22ca3d4d4f01a4548241&X-Amz-SignedHeaders=host",
  //      "size": "2.6 MB"
  //    },
  //    "signatory": []
  //  },
//  "message": "Document updated Successfully",
// "success": true,
//  "responseCode": 200
//}

```

### Delete Document

_This example for Delete Document._

<!-- prettier-ignore -->
```js
let weesign = require('weesign-sdk');

// Prerequisite: User needs to have a userID, access token and document should exit and document status either DRAFT Pending(none of the signatories has signed)

// data to be passed for update Document
let data = {
   'user-id':"avwxQxnm3sh5Y61WxRohhWmdZsb2",
   'token':"d5e6287a556a72ef9db209e1b878b8a6bghj2",
   'documentID':"d5e6287a556a72ef9db209e1b"

}
// 'user-id' is userID of document Owner/Creater
// 'token' is acces token which is generated using accessToken()
// 'documentID' is Id of od document which to be update

let reponse = await weesign.deleteDocument(data);

// and the reponse will be look like this
// { responseData: {},
//  message: 'Document Deleted successfully',
//  success: true,
//  responseCode: 200 }
```

### Get All document assiciated with a user

_This example for Get All document assiciated with a user._

<!-- prettier-ignore -->
```js
let weesign = require('weesign-sdk');

// Prerequisite: User needs to have a userID, access token and document should exit and document status either DRAFT Pending(none of the signatories has signed)

// data to be passed for get all Document
let data = {
   'user-id':"avwxQxnm3sh5Y61WxRohhWmdZsb2",
   'token':"d5e6287a556a72ef9db209e1b878b8a6bghj2",
   'status':"ALL",
   'limit':1,
   'skip':0
}
// 'user-id' is userID of document Owner/Creater
// 'token' is acces token which is generated using accessToken()
// 'status' status of document which can either DRAFT, PENDING, and COMPLETED. Default value : ALL for getting all document.
// 'limit' limit the number of document for getting
// 'skip' skip the number of previous document list 

let response = await weesign.getDocuments(data);


// and the reponse will be look like this
// { "responseData": [
//    {
//     "documentID": "5d4adeac1d6391bc05d13be",
//      "documentType": "OTHER",
//      "status": "DRAFT",
//      "country": "United States",
//      "documentSignType": "ELECTRONIC_SIGNATURE",
 //     "addedOn": 1565188066047,
 //     "documentFileObj": {
 //       "url": "https://signing-file.s3.amazonaws.com/sample.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIXB7WAVV4G_7T142236Z&X-Amz-Expires=518400&X-Amz-Signature=eb6938817d3e0be20c7ca23b16991fb90b6e65f9aabf22ca3d4d4f01a4548241&X-Amz-SignedHeaders=host",
  //      "size": "2.6 MB"
  //    },
  //    "signatory": []
  //  }
//  ],
//  "message": "Document Gets Successfully",
// "success": true,
//  "responseCode": 200
//}
```


### Get a particular Document

_This example for Get a particular Document._

<!-- prettier-ignore -->
```js
let weesign = require('weesign-sdk');

// Prerequisite: User needs to have a userID, access token and document should exit 

// data to be passed for get a particular Document
let data = {
   'user-id':"avwxQxnm3sh5Y61WxRohhWmdZsb2",
   'token':"d5e6287a556a72ef9db209e1b878b8a6bghj2",
   'documentID':"a556a72ef9db209e1b878b8a6b"
}
// 'user-id' is userID of document Owner/Creater
// 'token' is acces token which is generated using accessToken()
// 'documentID' id of document which you want to get.

let response = await weesign.getDocumentByID(data);


// and the reponse will be look like this
// { "responseData": {
//     "documentID": "a556a72ef9db209e1b878b8a6b",
//      "documentType": "OTHER",
//      "status": "DRAFT",
//      "country": "United States",
//      "documentSignType": "ELECTRONIC_SIGNATURE",
 //     "addedOn": 1565188066047,
 //     "documentFileObj": {
 //       "url": "https://signing-file.s3.amazonaws.com/sample.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIXB7WAVV4G_7T142236Z&X-Amz-Expires=518400&X-Amz-Signature=eb6938817d3e0be20c7ca23b16991fb90b6e65f9aabf22ca3d4d4f01a4548241&X-Amz-SignedHeaders=host",
  //      "size": "2.6 MB"
  //    },
  //    "signatory": []
  //  },
//  "message": "Document Get Successfully",
// "success": true,
//  "responseCode": 200
//}
```


### Add Signatory of a document

_This example for Add Signatory of a document._

<!-- prettier-ignore -->
```js
let weesign = require('weesign-sdk');

// Prerequisite: User needs to have a userID, access token and document should exit 

// data to be passed for Add signatory of a Document
let data = {
   'user-id':"avwxQxnm3sh5Y61WxRohhWmdZsb2",
   'token':"d5e6287a556a72ef9db209e1b878b8a6bghj2",
   'documentID':"a556a72ef9db209e1b878b8a6b",
   'message':"hello",
   'title':"sign the document"
   'signatory':[
      {
        "emailID": "info@example.com",
        "name":"name of user"
      }
   ]
}
// 'user-id' is userID of document Owner/Creater
// 'token' is acces token which is generated using accessToken()
// 'documentID' id of document which you want to get.
// 'message' message is text that will we  send in the mail to the signatories.
// 'title' title is text that will we send in the mail to the signatories.
// 'signatory' signatory is a array of object and each object contain email address and name of signatory.
// (Note: The signatory of document can add if document status is DRAFT.)

let response = await weesign.addSignatory(data);


// and the reponse will be look like this
// { "responseData": {
//     "documentID": "a556a72ef9db209e1b878b8a6b",
//      "documentType": "OTHER",
//      "status": "DRAFT",
//      "country": "United States",
//      "documentSignType": "ELECTRONIC_SIGNATURE",
 //     "addedOn": 1565188066047,
 //     "documentFileObj": {
 //       "url": "https://signing-file.s3.amazonaws.com/sample.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIXB7WAVV4G_7T142236Z&X-Amz-Expires=518400&X-Amz-Signature=eb6938817d3e0be20c7ca23b16991fb90b6e65f9aabf22ca3d4d4f01a4548241&X-Amz-SignedHeaders=host",
  //      "size": "2.6 MB"
  //    },
  //    "signatory": [
 // {
  //        "isSigned": 0,
 //       "signatoryID": "346fg7j65787uhgui76"
 //       "emailID": "info@example.com",
 //       "name":"name of user"
 //     }]
  //  },
//  "message": "Signatory added successfully",
// "success": true,
//  "responseCode": 200
//}
```



### Share a completed document through a mail

_This example for Share a completed document through a mail._

<!-- prettier-ignore -->
```js
let weesign = require('weesign-sdk');

// Prerequisite: User needs to have a userID, access token and document should exit 

// data to be passed for Share a completed document through a mail
let data = {
   'user-id':"avwxQxnm3sh5Y61WxRohhWmdZsb2",
   'token':"d5e6287a556a72ef9db209e1b878b8a6bghj2",
   'documentID':"a556a72ef9db209e1b878b8a6b",
   'postedTo':"info@example.com"
}
// 'user-id' is userID of document Owner/Creater
// 'token' is acces token which is generated using accessToken()
// 'documentID' id of document which you want to get.
// 'postedTo' postedTo is email address who will receive this document.
// (Note: the document ony can share to someone  if document status is COMPLETED.)

let response = await weesign.shareDocument(data);


// and the reponse will be look like this
// { "responseData": {},
//  "message": "Document sent successfully",
// "success": true,
//  "responseCode": 200
//}
```



### Validate Document

_This example for Validate a completed Document._

<!-- prettier-ignore -->
```js
let weesign = require('weesign-sdk');

// Prerequisite: User needs to have a userID, access token and document should exit 

// data to be passed for Validate Document

let firstPath = path.normalize(__dirname + '/dummy.pdf');
     let file = await fs.createReadStream(firstPath);

let data = {
   'user-id':"avwxQxnm3sh5Y61WxRohhWmdZsb2",
   'token':"d5e6287a556a72ef9db209e1b878b8a6bghj2",
   'file':file
};
// 'user-id' is userID of document Owner/Creater
// 'token' is acces token which is generated using accessToken()
// 'file' can be file Object or ReadStream Object

let response = await weesign.validateDocument(data);


// and the reponse will be look like this
// { "responseData": {},
//  "message": "Document Validated successfully",
// "success": true,
//  "responseCode": 200
//}
```


### Add WebHook

_This example for Add WebHook._

<!-- prettier-ignore -->
```js
let weesign = require('weesign-sdk');

// Prerequisite: User needs to have a userID, access token and document should exit 

// data to be passed for Add WebHook

let data = {
   'user-id':"avwxQxnm3sh5Y61WxRohhWmdZsb2",
   'token':"d5e6287a556a72ef9db209e1b878b8a6bghj2",
   'url':"https://example.com",
   'type':"completedDocument"
};
// 'user-id' is userID of document Owner/Creater
// 'token' is acces token which is generated using accessToken()
// 'url' url of the hook which will be htted on particular action For Example signDocument, completedDocument.
//  'type' type define the type webHook and type can be either completedDocument, or signDocument

let response = await weesign.addWebHook(data);


// and the reponse will be look like this
// { "responseData": {
//      "type": "completedDocument",
//      "webHookID": "h4nitekddgtgStllates",
//      "webHookUrl": "https://example.com",
 //     "addedOn": 1565188066047,
 // },
//  "message": "WebHook added successfully",
// "success": true,
//  "responseCode": 200
//}
```


### Update WebHook

_This example for Update WebHook._

<!-- prettier-ignore -->
```js
let weesign = require('weesign-sdk');

// Prerequisite: User needs to have a userID, access token and document should exit 

// data to be passed for Update WebHook

let data = {
   'user-id':"avwxQxnm3sh5Y61WxRohhWmdZsb2",
   'token':"d5e6287a556a72ef9db209e1b878b8a6bghj2",
   'url':"https://example.com",
   'webHookID':"6287a556a72ef9db209e1b878b"
};
// 'user-id' is userID of document Owner/Creater
// 'token' is acces token which is generated using accessToken()
// 'url' 'url' url is webHook url to be update
//  'webHookID' webHookID a particular webHook to be update.

let response = await weesign.updateWebHook(data);


// and the reponse will be look like this
// { "responseData": {
//      "type": "completedDocument",
//      "webHookID": "6287a556a72ef9db209e1b878b",
//      "webHookUrl": "https://example.com",
 //     "addedOn": 1565188066047,
 // },
//  "message": "WebHook updated successfully",
// "success": true,
//  "responseCode": 200
//}
```



### Get WebHook

_This example for Get WebHook._

<!-- prettier-ignore -->
```js
let weesign = require('weesign-sdk');

// Prerequisite: User needs to have a userID, access token and document should exit 

// data to be passed for Get WebHook

let data = {
   'user-id':"avwxQxnm3sh5Y61WxRohhWmdZsb2",
   'token':"d5e6287a556a72ef9db209e1b878b8a6bghj2",
   'webHookID':"6287a556a72ef9db209e1b878b"
};
// 'user-id' is userID of document Owner/Creater
// 'token' is acces token which is generated using accessToken()
//  webHookID' webHookID is Optional for getting a particular webHook.

let response = await weesign.getWebHook(data);


// and the reponse will be look like this
// { "responseData": [{
//      "type": "completedDocument",
//      "webHookID": "6287a556a72ef9db209e1b878b",
//      "webHookUrl": "https://example.com",
 //     "addedOn": 1565188066047,
 // }],
//  "message": "WebHook get successfully",
// "success": true,
//  "responseCode": 200
//}
```


### Delete WebHook

_This example for Delete WebHook._

<!-- prettier-ignore -->
```js
let weesign = require('weesign-sdk');

// Prerequisite: User needs to have a userID, access token and document should exit 

// data to be passed for Delete WebHook

let data = {
   'user-id':"avwxQxnm3sh5Y61WxRohhWmdZsb2",
   'token':"d5e6287a556a72ef9db209e1b878b8a6bghj2",
   'webHookID':"6287a556a72ef9db209e1b878b"
};
// 'user-id' is userID of document Owner/Creater
// 'token' is acces token which is generated using accessToken()
//  'webHookID' webHookID a particular webHook to be delete.

let response = await weesign.deleteWebHook(data);


// and the reponse will be look like this
// { "responseData": {},
//  "message": "WebHook deleted successfully",
// "success": true,
//  "responseCode": 200
//}
```
