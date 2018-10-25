# Application class

This is the base class of the entire framework as your application `app.js` file **MUST** extend this class to make the application ready.

# Package info

Package: `core/application`.

Parent Package: [core](./core.md).

Required: **Yes**.

Dependencies: [Support](./support.md).

Alias: `app`.

# Table of contents
- [Application class](#application-class)
- [Package info](#package-info)
- [Table of contents](#table-of-contents)
- [Available methods](#available-methods)
- [AutoLoad](#autoload)

# Available methods
- [autoLoad](#autoLoad)

# AutoLoad

`static autoLoad(className: string): void`

This method is useful for plugins that needs to be auto started once the application is **ready**.

As this method is static, you can it from anywhere in the framework without the application instance.

i.e
```javascript
Application.autoload('MyClassName');
```
