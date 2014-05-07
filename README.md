
# HiDrive JavaScript SDK #
## Introduction ##

The [HiDrive JavaScript SDK](https://dev.strato.com/hidrive/) lets you easily integrate HiDrive into your website or web app.

##Installation##

This section describes the basic steps for installing the HiDrive SDK for JavaScript.

### Get the HiDrive SDK for JavaScript
To get the source code of the SDK via git just type:

    git clone https://github.com/HiDrive/hidrive-js-sdk.git
    cd ./hidrive-js-sdk
    
### Use the HiDrive SDK for JavaScript components on your web page
To use the components from the HiDrive SDK for JavaScript on your web page, just include the **sdk.js** or **sdk.min.js** file in
your code.

For example, include one of the following tags in your code:

    <script type="text/javascript" src="/yourpath/sdk.js"></script>

Or:

    <script type="text/javascript" src="/yourpath/sdk.min.js"></script>

##Browser Usage##

###Getting Started

You can find a getting started guide at:

https://dev.strato.com/hidrive/getstarted

###OAuth Requests

For documentation on how to, please see the HiDrive developer portal https://dev.strato.com/hidrive/

Set the following parameters before requesting API for authorization.

```js
HD.options({ 'appId': YOUR_APP_ID });
HD.options({ 'responseType': 'token' });
HD.options({ 'grantScope': 'admin,rw' });
HD.options({ 'redirectUrl': 'http://localhost:12345/' });
HD.options({ 'language': 'en' });
```

After authorization process you get an access_token. Store the access_token in options:
```js
HD.options({ 'accessToken': YOUR_ACCESS_TOKEN });
```
This access_token will be used for all further API requests.

###Basic use

hidrive-js-sdk is exposed as a global variable `HD`.

### Configuration options

When this method is called with no parameters it will return all of the current options

```js
var options = HD.options();
```

When this method is called with a string it will return the value of the option 
if exists, null if it does not. 

```js
var options = HD.options();
```

When this method is called with an object it will merge the object onto the previous 
options object.  

```js
HD.options({appId: '123456'});
//will set userName and accessToken options
HD.options({userName: 'ABC', accessToken: 'XYZ'});
//will get the accessToken of 'XYZ' 
var accessToken = HD.options('accessToken'); 
```

The existing options are:

* `'accessToken'`: Access token.
* `'appId'`: Application id.
* `'userScope'`: User scope.
* `'grantScope'`: Grant scope.
* `'type'`: Grant type.
* `'redirectUrl'`: Login redirect url for oAuth e.g. 'http://localhost:12345/'.
* `'language'`: Language for the login dialog.
* `'user'`: The path to the file to download.
* `'userName'`: User name.
* `'accountId'`: Account id.

### API

#### Obtaining API Request URL

##### Get API URL
Makes a call to get the url for the API calls GET, POST, PUT and DELETE.

```js
var url = HD.getApiUrl();
```

##### Get API File Transaction URL
Returns a url for a background upload or download operation:

```js
var properties = {dir: 'root/public', name: 'foo.jpg', on_exist: 'autoname'};
var url = HD.getFileTransactionUrl(properties);
```

##### Get API Login URL
Makes a call to get the url for the login process. 

```js
var url = HD.getLoginUrl();
```

##### Get URL for oAuth
Makes a call to get the url for access token request.

```js
var url = HD.getOAuthUrl();
```

#### Post

```js
HD.post(path, parameters, cbSuccess, cbError, cbProgress);
```

For example, create a new directory 

```js
var parameters = {path: root/users/foobar/existingDir/newDir};
HD.post("/dir", parameters, function(response){
  //do something with response
}, function(){
  //error
}, function(){
  //progress
});
```

#### Get

```js
HD.get(path, parameters, cbSuccess, cbError, cbProgress);
```

For example, get directory members 

```js
var parameters = {path: 'root/public/XYZ'};
HD.get("/dir", parameters, function(response){
  //do something with response
}, function(){
  //error
}, function(){
  //process
});
```
Or get corresponding sharelink:
```js
var parameters = { id: '123456' };
HD.get("/sharelink", parameters, function(response){
  //do something with response
}, function(){
  //error
}, function(){
  //process
});
```

#### Delete

```js
HD.get(path, parameters, cbSuccess, cbError, cbProgress);
```

For example, delete a file

```js
var parameters = {path: 'root/public/foo.txt'};
HD.delete("/file", parameters, function(response){
  //do something with response
}, function(){
  //error
}, function(){
  //process
});
``` 

#### Put

```js
HD.put(path, parameters, cbSuccess, cbError, cbProgress);
```

For example, change user data 

```js
var parameters = {account: '1234', alias: 'XYZ', pasword: '******'};
HD.put("/user", parameters, function(response){
  //do something with response
}, function(){
  //error
}, function(){
  //process
});
``` 

#### Get token info
Makes a call to get information about your current access_token.

```js
   HD.getTokenInfo(function(response){
      //do something with response.access_token
   }, function(){
      //error
   });
```

#### Session Clear
Makes a call to clear session configuration options.

```js
HD.sessionClear();
```

The following parameters are deleted:
* accessToken
* userName
* accountId
* userScope

#### Check authorization
Makes a call to verify whether the current user is authorized or not.

```js
HD.isAuthorized();
```

#### Logout
Makes a call to clear the session data(access token, user name, accound id, user scope).

```js
HD.logout();
```

#### Clear session
Makes a call to clear session configuration options. The following parameters are deleted:

```js
HD.sessionClear();
```

###Learn More
For more details see the HiDrive API Documentation https://dev.strato.com/hidrive/documentation/