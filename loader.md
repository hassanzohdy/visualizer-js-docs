# Loader.json
OK, now we are going to dive into the most important file in Visualizer JS

# File structure

```json
{
    "externals": {
        "css": {
            "common": [],
            "ltr": [],
            "rtl": []
        },
        "js": []
    },
    "vendor": {
        "css": {
            "common": [],
            "ltr": [],
            "rtl": []
        },
        "assets": [],
        "js": []
    },
    "framework": [],
    "apps": {
        "myAppName": {
            "externals": {
                "css": {
                    "common": [],
                    "rtl": [],
                    "ltr": []
                },
                "js": []
            },
            "vendor": {
                "css": {
                    "common": [],
                    "rtl": [],
                    "ltr": []
                },
                "assets": [],
                "js": []
            },
            "framework": [],
            "app": {
                "favicon": "",
                "assets": [],
                "components": []
            }
        }
    }
}
```

That was the entire file structure for the loader.

Now let's go to the details the loader.

First off, we've 4 main **section** as follows:
- [**externals**](#external-files): External Files.
- [**vendor**](#vendor): 3rd party plugins.
- [**framework**](#framework): Visualizer Components.
- [**apps**](#apps): List of all applications.

> Any section above the apps section will be called in every application as they all treated as common sections/components

# External Files
For sure you may want to include some external stylesheets or javascript files, that's where the **externals** sections comes in hand.

External files are divided into two types:
- css: for stylesheets files
- js: for javascript files

# Css structure

As most of the web applications these days are multilingual applications so we may need to include some stylesheets for `rtl` direction and `ltr` direction and some files will be common in both directions, we're dividing the `css` section into three sections
- **common**: Array of external urls that will be included in all directions.
- **ltr**: Array of external urls that will be included in `ltr` direction only.
- **rtl**: Array of external urls that will be included in `rtl` direction only.

For example, assume we will use the [animator](./components/animator.md) component, that component requires the animate.css file so we need to include it in the `common` section as we will use it in all apps.

For the `ltr` and `rtl` directions, let's say we  will use `Open Sans font` in the `ltr` direction and `Cairo font` in the `rtl` direction.

> Please note that the css section structure will be the same in the entire file

for the `js` section, it will be an array of urls for script files

Let's wrap it all in the file and see how it will look like:

```json
{
    "externals": {
        "css": {
            "common": [
                "https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.5.2/animate.min.css"
            ],
            "ltr": [
                "https://fonts.googleapis.com/css?family=Open+Sans:300,400,600,700"
            ],
            "rtl": [
                "https://fonts.googleapis.com/css?family=Cairo:200,300,400,600,700,900"
            ]
        },
        "js": [
            "http://sitename.com/js-file.js"
        ]
    }
}
``` 

> Please note that all external files are loaded unsynchronized

> Please note that the **externals** section info will be included in all applications.

# Vendor
In the vendor section, any 3rd party plugin can be injected and compiled to the application.

This vendor section is separated into three sections
- [css](#css-structure): will be same as the **externals** one
- [js](#js-section)
- [assets](#assets-section)

## Js section
As we mentioned earlier in the **externals** section, the `js` section will be an array of js files paths.

Any path in the `vendor` will be relative to the vendor directory.
For example: if we want to include jquery file in the vendor and its path as follows:

`/ui/vendor/jquery/3.3.1/jquery.min.js`

In this case the path that will be written will be `jquery/3.3.1/jquery.min.js`.

Same thing applies on css and assets sections.

## Assets section
If there are other directories that are required for some css files like `font-awesome` fonts folder then we need to include it as follows:

> Assuming the font-awesome directory is: /ui/vendor/css/font-awesome

```json
{
    "assets": [
        "css/font-awesome/fonts"
    ]
}
```

> Please note that the **vendor** section info will be included in all applications.


# Framework
In this section, all required components for Visualizer need to function well should be set here and any other components that will be used in all applications should be set as well.

For complete reference of Visualizer components [click here](./framework-components.md)

# Apps
In this section, we will start adding our applications.

Each application can have the other three main sections **externals**, **vendor** and **framework** that will extend the global sections configurations.

There is one more property called `app` which will contain the application specifications as follows:

| Key        | Description                                                                                                                                                                                                                                                                       |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| favicon    | The application favicon that will be added. Please note that the path of the favicon will be relative to the **assets** directory in the app directory. For example, if favicon is set to `images/favicon.png` then its path should be `/ui/apps/MyApp/assets/images/favicon.png` |
| assets     | An array of assets directories that will be copied to be in the static app directory next to `css` and `js` directories. For example, if assets array contains `images` then the `images` directory will be copied to `/public/static/MyApp/images`                               |
| components | List of the application [components](./component.md) that will be used in the application which will be in the `/ui/apps/MyApp/components` directory.                                                                                                                             |

# Components Ordering
The framework is loaded based on your components/files ordering, so if we have `component A` that requires `component B` then you must set `component B` before `component A`.

# Minimum Loader Requirements
The following loader structure is the minimum requirements to make the framework functions as expected.

```json
{
    "externals": {
        "css": {
            "common": [],
            "ltr": [],
            "rtl": []
        }
    },
    "vendor": {
        "js": [
            "jquery/jquery/3.3.1/jquery.min.js"
        ],
        "css": {
            "common": [],
            "ltr": [],
            "rtl": []
        },
        "assets": []
    },
    "framework": [
        "support/javascript",
        "support/helpers",
        "support/is",
        "core/dynamic",
        "core/application",
        "core/component",
        "core/dynamicComponent",
        "core/current",
        "core/loader",
        "core/router",
        "core/events",
        "core/view",
        "core/layout"
    ],
    "apps": {
        "myAppName": {
            "externals": {
                "css": {
                    "common": [],
                    "rtl": [],
                    "ltr": []
                },
                "js": []
            },
            "vendor": {
                "css": {
                    "common": [],
                    "rtl": [],
                    "ltr": []
                },
                "assets": [],
                "js": []
            },
            "framework": [],
            "app": {
                "favicon": "",
                "assets": [],
                "components": [
                    "MyApp"
                ]
            }
        }
}
```

> Please note that all `core` components are required.
> Please note that jquery 3 or higher also required. 

# Next Step
[Component Structure](./component.md)