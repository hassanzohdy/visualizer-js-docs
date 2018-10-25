# Package
The Visualizer JS framework is a set of packages **components**.

# Table of contents
- [Package](#package)
- [Table of contents](#table-of-contents)
- [Package structure](#package-structure)
- [Package.json](#packagejson)
    - [file structure](#file-structure)
- [Newly created packages](#newly-created-packages)

# Package structure

Each package contains the following directories/files.


```
Package
└─── assets // package assets files and folders
└─── html // views file here
└─── js // logic code here which is javascript files
└─── scss // sass files here
│   └─── common create common styling files for both directions
│   └─── rtl // create only sass files that will affect only on the rtl direction
│   └─── ltr // create only sass files that will affect only on the rtl direction
└─── package.json // package settings
```

# Package.json
The `package.json` is the package configurations file where we define the package dependencies, components(**child packages**), vendor files...etc

## file structure
This is the full schema of the `package.json` file 

```json
{
    "name": "",
    "version": "",
    "favicon": "",
    "type": "",
    "dependencies": [],
    "plugins": [],
    "components": [],
    "assets": [],
    "externals": {
        "js": [],
        "css": {
            "common": [],
            "ltr": [],
            "rtl": []
        }
    },
    "vendor": {
        "js": [],
        "css": {
            "common": [],
            "ltr": [],
            "rtl": []
        }
    }
}
```

| Key | Required | Type | Description |
|---|---|---|---|
| name | Yes | `String` | Package name, which should be the equivalent to its path, i.e: `core/views`  |
| version | No | `Float` - `String`  | Package version |
| favicon | No | `String` | **App package only** Set the favicon of the application, works only with apps. |
| type | No | `String` | Package type. Available types are: **framework** , **plugin**, **app** the package type is determined based on the package location, i.e any package in the `plugins` directory will be treated automatically as a **plugin** type.  |
| dependencies | No | `Array` | List of the required packages from the `framework` to be loaded before the package is loaded. |
| plugins | No | `Array` | List of the required packages from the `plugins` directory to be loaded before the package is loaded. |
| assets | No | `Array` | List of assets directories/files where are **MUST** be located in the `assets` directory inside the package directory, **Note**: only the listed directories in this array will be copied even if the `assets` directory has more directories or files. |
| externals | No | `Object` | To load any external javascript or css files. **This is Recommended** when the files won't affect on the application when it starts. The external files are loaded when the app is ready. |
| vendor | No | `Object` | Load javascript/css files from the `vendor` directory. Any path from that will be loaded will start after the `vendor` path. i.e: to load `/ui/vendor/jquery/jquery/js/jquery.min.js`, then we will set the path like this: `jquery/jquery/js/jquery.min.js`. |

# Newly created packages

After creating your package, you need to rebuild your application again if you are not running the `serve` command.

i.e: `php visualize build blog`.

Adding new javascript files to the package will require another build to be cached in the javascript files list.

> New Html and scss files don't need a rebuild for the application.

> If the server is already running it will rebuild the application automatically so you won't have to rebuild it again.
