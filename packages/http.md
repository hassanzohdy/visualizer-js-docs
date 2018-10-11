# Http

The http component is responsible for handling remote `AJAX` || `XHR` requests either for API requests or for any 3d party requests.

# Package info

Package: `core/http`.

Parent Package: [core](./core.md).

Required: **Yes**.

Dependencies: [Events](./events.md).

# Table of contents
- [Http](#http)
- [Package info](#package-info)
- [Table of contents](#table-of-contents)
- [Sub components](#sub-components)
- [Http package](#http-package)
    - [Methods](#methods)
        - [Send](#send)
            - [Arguments](#arguments)
            - [Return type](#return-type)
            - [Example](#example)
        - [Get](#get)
            - [Arguments](#arguments-1)
        - [Post](#post)
            - [Arguments](#arguments-2)
            - [Data types](#data-types)
        - [Put](#put)
            - [Arguments](#arguments-3)
        - [Patch](#patch)
            - [Arguments](#arguments-4)
        - [Delete](#delete)
            - [Arguments](#arguments-5)
        - [Scripts](#scripts)
            - [Example](#example-1)
        - [Stylesheets](#stylesheets)
            - [Example](#example-2)
        - [Assets](#assets)
            - [Example](#example-3)
    - [Configurations](#configurations)
    - [Events](#events)
        - [Example](#example-4)
- [Endpoint package](#endpoint-package)
    - [Endpoint Configurations](#endpoint-configurations)
        - [Examples](#examples)

# Sub components
This package contains three components:

- [Http](#http-package)
- [Endpoint](#endpoint-package)
- [Endpoint Service](#endpoint-service-package)


# Http package

Package: `core/http/http`.

Parent Package: [core/http](#http).

Required: **Yes**.

Dependencies: [Events](./events.md).

Alias: `http`

The Http component is the main component in the `core/http` package as its the responsible one for sending requests.

## Methods
- [send](#send)
- [get](#get)
- [post](#post)
- [put](#put)
- [patch](#patch)
- [delete](#delete)
- [scripts](#scripts)
- [styleSheets](#stylesheets)
- [assets](#assets)


### Send
`send(Object options): Promise`

This method will send an Ajax `XHR` request based on the given options.

#### Arguments

`options`: Type **Object**

Basically, the `send` method is using [jQuery.ajax() method](http://api.jquery.com/jquery.ajax/) to send an `XHR` request so options will be much the same except for few things.

`options.progress`: callback

If you want to calculate the progress of the request, i.e when uploading the file, this option will give you the current progress percentage value.

For example

```javascript
http.send({
    type: 'POST',
    data: new FormData(document.getElementById('my-form')),
    progress: function (percentageValue) {
        echo(percentage); // it will be changed frequently based on the current percentage value of the uploading/sending process. 
    }
})
```

By default, for sending data in `POST`, `PATCH` or `PUT` requests, the proper content type and processing data will be set automatically so it won't be needed to send any extra options like: `contentType`, `processData` or `cache`. 

#### Return type
This method returns a [Promise Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) which follows the standard of [Promises/A+](https://promisesaplus.com/) so the response of the request will be used in `then` method and the error will be in the `catch` method.

#### Example

```javascript
http.send({
    url: 'https://google.com',
}).then((response, statusCode, xhr) => {
    // on success request
}).catch((responseError, statusCode, errorThrown, xhr) => {
    // response with other status than 200
});
```

### Get

This is a shorthand method for [send](#send) method for creating `GET` method

`get(string url, Object Options = {}): Promise`

#### Arguments

`url` Type: **String** `Required`
`options` Type: **Object** `Optional`, this parameter is used more options than the `url` parameter.

```javascript
http.get('https://google.com').then(response => {
    // do something
});
```

### Post
This is a shorthand method for [send](#send) method for creating `POST` method

`post(string url, mixed data): Promise`


#### Arguments

`url`: Type: **String** `Required`
`data`: Type: **mixed** `Required`
`options` Type: **Object** `Optional`, this parameter is used more options than the `url` and `data` parameters.

#### Data types

The `data` parameter could be many types as follows:

- **Plain Object**

```javascript
http.post('https://my-backend.com/api/register', {
    name: 'Hasan',
    email: 'hassanzohdy@gmail.com',
}).then(response => {
    // do something
});
```

- **FormData Object**

```javascript
http.post('https://my-backend.com/api/register', new FormData(document.getElementById('my-form'))).then(response => {
    // do something
});
```

- **jQuery Object**

```javascript
http.post('https://my-backend.com/api/register', $('#my-form')).then(response => {
    // do something
});
```

- **String**

```javascript
http.post('https://my-backend.com/api/register', 'name=hasan&email=hassanzohdy@gmail.com').then(response => {
    // do something
});
```

- [FormHandler Object](./forms/form-handler.md)

```javascript
let myForm = forms.get('#my-form');
http.post('https://my-backend.com/api/register', myForm).then(response => {
    // do something
});
```

### Put
This is a shorthand method for [send](#send) method for creating `PUT` method

`put(string url, mixed data): Promise`

#### Arguments

`url`: Type: **String** `Required`
[data](#data-types): Type: **mixed** `Required`
`options` Type: **Object** `Optional`, this parameter is used more options than the `url` and `data` parameters.

### Patch
This is a shorthand method for [send](#send) method for creating `PATCH` method

`patch(string url, mixed data): Promise`

#### Arguments

`url`: Type: **String** `Required`
[data](#data-types): Type: **mixed** `Required`
`options` Type: **Object** `Optional`, this parameter is used more options than the `url` and `data` parameters.

### Delete

This is a shorthand method for [send](#send) method for creating `DELETE` method.

`delete(string url, Object Options = {}): Promise`

#### Arguments

`url` Type: **String** `Required`

```javascript
http.delete('https://my-backend.com/api/posts/12').then(response => {
    // do something
});
```

### Scripts
This method is used to load javascript files.

`scripts(array scripts): Promise`

#### Example
```javascript
http.scripts([
    'https://cdn.my-site.com/js/my-js-file.js',
    'https://cdn.my-site.com/js/my-js-file-2.js',
    'https://cdn.my-site.com/js/my-js-file-3.js',
]).then(() => {
    // do something after loading all scripts
});
```

### Stylesheets
This method is used to load css files.

`stylesheets(array styleSheets): Promise`

#### Example
```javascript
http.stylesheets([
    'https://cdn.my-site.com/css/my-css-file.css',
    'https://cdn.my-site.com/css/my-css-file-2.css',
    'https://cdn.my-site.com/css/my-css-file-3.css',
]).then(() => {
    // do something after loading all stylesheets
});
```

### Assets
This method is used to load javascript and css files in same time.

`assets(array scripts, array styleSheets): Promise`

#### Example
```javascript
http.assets([
    'https://cdn.my-site.com/js/my-js-file.js',
    'https://cdn.my-site.com/js/my-js-file-2.js',
    'https://cdn.my-site.com/js/my-js-file-3.js',
], [
    'https://cdn.my-site.com/css/my-css-file.css',
    'https://cdn.my-site.com/css/my-css-file-2.css',
    'https://cdn.my-site.com/css/my-css-file-3.css',
]).then(() => {
    // do something after loading all javascript and css files
});
```

## Configurations

In your application `config.json`, these are the available options for this component.

Main Configuration key: `http`

| key | Type | Default value | Description | 
|---|---|---|---|
| uploadablePut | `Boolean` | **true** | As most browsers don't `support` uploading files in the `PUT` requests, If this option is set to true, then when sending new `PUT` request it will be changed to `POST` request with a hidden field `_method`  = **PUT** as `PUT` requests don't allow uploading files. [Click here for more details.](https://github.com/laravel/framework/issues/13457)  |


## Events

| Event | callback parameters | Description |
|---|---|---|
| `http.loading-url` | `Request url`, `ajax options list` | This event is triggered before sending any request, if the return value of the callback is `false`, then the request will not be sent. |

### Example

```javascript
class HomePage extends Layout.Page {
    bootstrap(events, http) {
        events.on('http.loading-url', function (url, options) {
            // do something here before loading that url

            // to prevent calling that request return false 
            return false;
        });

        // send a request to google.
        http.get('https://google.com');
    }
}
```

# Endpoint package

Package: `core/http/endpoint`.

Parent Package: [core/http](#http-package).

Required: **Yes**.

Dependencies: [core/http/http](#http-package).

Alias: `endpoint`

The **Endpint** component is a sub component of the `core/http` package as its used to handle requests directly with your backend without setting the full url each time you want to send a new request to your backend API.

By default, this component is loaded under the `core/http` main package so you don't need to include it manually if you already included the `core` or the `core/http` package.

The idea here is that you set a `baseUrl` for your backend in your [Configurations](./../configurations.md) the `config.js` file in your application directory and all you've to do is just to call a `routes` or `endpoints` directly using this component.

## Endpoint Configurations
Configuration main key: `http.endpoint`


| key | Type | Default value | Description | 
|---|---|---|---|
| baseUrl | `String`, `Object` | `''` | The base url to your `Restful API`. It could be a string with the baseUrl api for your backend or it could be an object with `development` key for local backend and `production` for the production backend. If the backend is the same in both cases then put it as a `String` not as an `Object`.  | 
| apiKey | `String` | `''` | If this option is set, then any request that doesn't require the user login will be sent with an `Authorization: key {apIKey}` header.| 

This component have all the required methods for performing a full `Restful API` with your backend, which are:

- [get](#get)
- [post](#post)
- [put](#put)
- [delete](#delete)
- [patch](#patch)

However, there are little more bit here than the above methods.

If you're going to send an `authorized` request for the backend, which means the user is already logged in and you want to send a request that indicates the user is logged in, in this case we will use the `authorizable()` method to tell the endpoint that the user is authorized to send a request while logging in.

In that case, the `Authorization` header will be sent but this time with different key `Bearer` and the value will be the `accessToken` which could be sent as the second argument of the `authorizable()` method or it will be taken from the [user component](./user.md).


### Examples
```javascript
// config.js file
Config.extend({
    http: {
        endpoint: {
            baseUrl: 'https://my-backend.com/api',
            apiKey: 'ADAS58HAS9125YBXZC9TQWPTYPQES5122ASFPTES',
        },
    },
});

// Home page

class HomePage extends Layout.Page {
    bootstrap(endpoint) {
        // first send a non-logged in user request
        endpoint.get('/posts').then(response => {
            // iin this case the following header will be sent
            // Authorization: key ADAS58HAS9125YBXZC9TQWPTYPQES5122ASFPTES
            // do something with the success response 
        });

        // now let's tell the endpoint that the user from now is authorizable
        // if the second argument is not sent, then the endpoint will try to get it
        // from the `user` component using the `accessToken` method
        endpoint.authorizable(true, 'user-access-token');

        // send another request but this time it is an authorized request
        endpoint.get('/posts').then(response => {
            // iin this case the following header will be sent
            // Authorization: Bearer user-access-token
            // do something with the success response 
        });
    }
}
```