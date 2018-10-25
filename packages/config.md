# Config

This is the responsible package for managing the runtime configurations in `src/apps/{appName}/components/config.js` file. 

# Package info

Package: `core/config`.

Parent Package: [core](./core.md).

Required: **Yes**.

Dependencies: N/a.

Alias: `N/a`.

# Table of contents
- [Config](#config)
- [Package info](#package-info)
- [Table of contents](#table-of-contents)
- [How does it work](#how-does-it-work)
- [Getting values from the config](#getting-values-from-the-config)
- [Get](#get)
- [Has](#has)
- [Set](#set)

# How does it work
First, let's talk about few things about the `Config` class before we see how the configurations flow work.

- It's a full static class, that means you can't `resolve` it using [DI](./dependency-injection.md) or create new instance of it.
- The Config handle configurations in the runtime, so it has nothing to do with the framework configurations in the `config.json` file in the `root` directory.
- All of the packages in the framework itself or in the plugins are set in that file so it will be easier to modify it 

Now let's see how to use it.

It's very simple to handle the application configurations in the `config.js` file.

Using the `Config.extend` method is mandatory here to set the configurations.

In a fresh installation, the `config.js` file is created automatically with basic configurations.

```javascript
// runtime configurations
Config.extend({
    layout: {
        basePath: 'layout/layout/layout-structure',
    },
    form: {
        validatable: true,
        freeze: {
            onSubmit: true,
            buttons: FormHandler.FREEZE_ALL,
        },
        plugins: [],
    },
    http: {
        endpoint: {
            baseUrl: '',
            apiKey: '', // used with the `key` for Authorization header 
        }
    }
});
```

Now let's see how to get any values from that config file.

# Getting values from the config

The `Config` class has [Config.get](#get) method which makes it easy for you to get any value from it.


# Get
This method is used to get any value from the `config.js` file using the **object dot notation syntax**.

`static get(key: string, defaultValue: any = null): any`

The **object dot notation syntax** means that the configurations is marked as `namespaces` which means you can get the object value of a primary key in the configurations.

Let's see what does it mean in action.

```javascript

let httpOptions = Config.get('http');
// the returned value will be: 
httpOptions = {
    endpoint: {
        baseUrl: '',
        apiKey: '', // used with the `key` for Authorization header 
    }
```

Now let's say that you want only the value of  the `apiKey`, here we will use the **object dot notation syntax**


```javascript
let endPointApiKey = Config.get('http.endpoint.apiKey');
```
That's it!, so if we want to get a certain value for a key from any of configurations you can write the key name like this `mainKey.subKey.subSubKey.key`.

# Has
`static has(key: string): boolean`

To check if the given key exists in the configurations file.

```javascript

if (Config.has('form.validatable')) {
    // do something
}

```

# Set
`static set(key: string, value: mixed): void`

Set/Replace the value for the given key

```javascript
Config.set('app.name', 'My New App Name!');
```