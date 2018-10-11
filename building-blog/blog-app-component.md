# BlogApp Component

Now we will start the real work. We will create the `BlogApp` component.

# Table of contents
- [BlogApp Component](#blogapp-component)
- [Table of contents](#table-of-contents)
- [Naming the js file](#naming-the-js-file)
- [Extending application component](#extending-application-component)
- [Defining our blog pages](#defining-our-blog-pages)
- [Creating layout component](#creating-layout-component)
- [Next Step](#next-step)

# Naming the js file
Its always preferable to name our js files with its class name, so in our case we will create `BlogApp.js` file as our class name will be `BlogApp`.

So now so far we've the following structure:

```
my-blog
└─── ui
|   └─── apps
|        └─── myBlog
|             └─── assets
|             └─── components
|                  └─── blogApp
|                       └─── js
|                            └─── BlogApp.js 
|             └─── scss
|                  └─── app.scss
|   └─── visualizer
|   └─── vendor 
|   └─── loader.json
```

# Extending application component
Now we've created our `BlogApp.js` file so lets head to create our class.

```javascript
class BlogApp extends Application {

}
```

As our application is entirely built on [Application component](./../components/application.md) so our main application class `BlogApp` **MUST** extend it.

> Please note that the application component is registered on itself so you can use it as `this.app.doSomething()`   

Next we need to implement `init()` method in our class to define our configurations and components.

```javascript
class BlogApp extends Application {
    /**
     * Initialize application 
     *
     * @returns this
     */
    init() {
        return this;
    }
}
```

Now we need to register some components to our application.

> Please note that the `core` components are registered by default so you don't need to re-register it again.
> 
```javascript
class BlogApp extends Application {
    /**
     * Initialize application 
     *
     * @returns this
     */
    init() {
        this.registerMainComponents();
        this.registerAppComponents();
        return this;
    }

    /**
     * Register main components that we need to use from framework components
     * Please note that we won't register our components in this method but we will do it in `registerAppComponents` method
     * 
     * @returns void
     */
    registerMainComponents() {

    } 

    /**
     * Register  app components
     * 
     * @returns void
     */
    registerAppComponents() {

    } 
}
```

in the `registerMainComponents()` method, we will register our app components that we will define it on the [loader.json](./../loader.md) file in `apps.myBlog.app.components` path.

# Defining our blog pages

Before we start registering what components we need, first let's see what pages we will have in our website.

- Home page
- Sign up page
- Login page
- Logout page
- Category page
- Post page
- Contact us page

This list will be our pages for the website and we can extend it later.

So lets create new folder and name it `pages` we will put it next to our `blogApp` folder.

Now we will create folder for each page in our `pages` folder.

```
myBlog
└─── components
|    └─── blogApp
|    └─── pages
|         └─── category
|         └─── contact-us
|         └─── home
|         └─── login
|         └─── logout
|         └─── post
|         └─── sign-up
```

But as we can see that the **Sign up page** and **Login page** are relative to the user so we can create `user` folder to hold any page that related to the user. 

```
myBlog
└─── components
|    └─── blogApp
|    └─── pages
|         └─── category
|         └─── contact-us
|         └─── home
|         └─── post
|         └─── user
|              └─── login
|              └─── logout
|              └─── sign-up
```

Now we will add `pages` component before `blogApp` in the `loader.json` file, so the file will be:

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
        "core/view"
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
                    "pages",
                    "blogApp"
                ]
            }
        }
}
```

> Please remember that the `blogApp` **MUST BE** at the very last bottom of the components list so any components should be defined before it.

# Creating layout component
As we are building an SPA application, so the entire website will have a **layout** that will contain the content of each page plus the common partials like header, menu, breadcrumb and footer.

Now we created the `layout` folder in our components directory, we will create more two folders, `layout` and `common`.

The `layout` folder will contain the main layout of all pages structure.

The `common` folder will contain 4 folders: `breadcrumb`, 
`footer`, `header` and `menu`.

Now we will add the `layout` component to our app components list so it will be:

```json
"components": [
    "layout",
    "pages",
    "blogApp",
]
```

And our `myBlog` directory will be:

```
myBlog
└─── components
|    └─── layout
|         └─── common
|              └─── breadcrumb
|              └─── footer
|              └─── header
|              └─── menu
|         └─── layout
|    └─── blogApp
|    └─── pages
|         └─── category
|         └─── contact-us
|         └─── home
|         └─── post
|         └─── user
|              └─── login
|              └─── logout
|              └─── sign-up
```

> Please note that we can access the application object from anywhere using `$.app` object. For example: $.app.http.get('https://sitename.com'); 

# Next Step
[Registering layout and pages components](./layout.md)
