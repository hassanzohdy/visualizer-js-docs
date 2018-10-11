# Pre Compiled Configurations
Before we getting started with our application(s), we need first to set some configurations for it.

in the `config.json` file, we will put the main configurations for the entire applications.

### Here is how the `config.json` looks like:

```json
{
    "baseUrl": "https://sitename.com", 
    "apps": [ 
        {
            "route": "/", 
            "env": "development", 
            "locale": "ar", 
            "appName": "MyApp", 
            "version": 1.0 
        },
        {
            "route": "/admin", 
            "env": "development", 
            "locale": "en", 
            "appName": "AdminApp", 
            "version": 1.0 
        }
    ]
}
```

# Description

### baseUrl
It will be the base url of all apps and can be used in the framework it self using the `url` function as we will explain it later.

### apps
An array of objects that contains all of the applications list that will be used.
> You can add as many as possible of applications for same domain, every app will separated from each other and will be compiled on its on.

### App configurations

| Key     | Description                                                                                                                                                                             |
| ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| route   | The base route of the app.                                                                                                                                                              |
| env     | the current status of the application environment, it could be `development` or `production` which is automatically switched to on running the production command line.                 |
| locale  | the locale code that will be added after the route so it could be used easily for multilingual applications.                                                                            |
| appName | the name of the application MUST be the same as of its directory name in the `ui/apps` directory, for example: `appName`: 'MyApp' which will make the directory name `ui/apps/appName`. **Please note that the appName is required in every app configurations as it will be used for compiling the code.** |
| version | The version of the application which will be incremented on the production compiling and will be added to all of the css and js files on production mode.                               |


# Next Step

- [Framework Structure](./framework-structure.md)