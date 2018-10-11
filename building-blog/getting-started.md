# Getting started with our first application.
Let's stop talking and let's build our first application which will be a blog.

# Table of contents
- [Getting started with our first application.](#getting-started-with-our-first-application)
- [Table of contents](#table-of-contents)
- [Blog configurations](#blog-configurations)
- [Preparing folders structure](#preparing-folders-structure)
- [Preparing loader file](#preparing-loader-file)
- [Next Step](#next-step)

# Blog configurations
First off, let's edit `config.json` file.

```json
{
    "baseUrl": "localhost/my-blog", 
    "apps": [ 
        {
            "route": "/", 
            "env": "development", 
            "locale": "en", 
            "appName": "myBlog", 
            "version": 1.0 
        }
    ]
}
```
So far nothing is new, we set our base url to our blog path in the localhost.

# Preparing folders structure
Now lets head to the `/ui` directory.
We've there three directories: `apps`, `visualizer` and `vendor` and our `loader.json` file.

What we need here is to modify `loader.json` and `apps` directory.

First, lets create the necessary folders in the `apps` directory.

AS we named our application with `myBlog` so we will create new folder `myBlog` in the `apps` directory.

In `apps/myBlog` directory, we'll create three folders: `assets`, `components` and `scss`.

Just for now, We will leave the `assets ` directory and head to `scss` directory to create `app.scss` for styling purposes.

> For full details about styling, please head to [Styling section](./../styling.md).

Now we will go to `apps/myBlog/components` directory and create `blogApp` folder.

> Its preferable to naming components folders like my-component style.

The final structure should looks like: 

```
my-blog
└─── ui
|   └─── apps
|        └─── myBlog
|             └─── assets
|             └─── components
|                  └─── blogApp
|             └─── scss
|                  └─── app.scss
|   └─── visualizer
|   └─── vendor 
|   └─── loader.json
```

# Preparing loader file
So far so good, now lets open `loader.json` file which looks like:

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
Now we will replace `myAppName` with `myBlog` and `MyApp` with `BlogApp`.

So the final structure for the `loader.json` will be 

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
        "myBlog": {
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
                    "blogApp"
                ]
            }
        }
}
```

# Next Step
[Creating BlogApp component](./blog-app-component.md)   