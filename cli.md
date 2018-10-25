# CLI

The framework has a simple, elegant and powerful cli took to handle your applications.

# Table of contents
- [CLI](#cli)
- [Table of contents](#table-of-contents)
- [How to run any command in the framework](#how-to-run-any-command-in-the-framework)
- [Commands list](#commands-list)
- [Install](#install)
- [Global](#global)
    - [Available options](#available-options)
- [Serve](#serve)
- [Build](#build)
- [New page](#new-page)
- [New smart page](#new-smart-page)
- [Build smart views](#build-smart-views)
- [New application](#new-application)
    - [Options description](#options-description)
- [Produce](#produce)

# How to run any command in the framework
Any command must start with `php visualize` then your command name and command options after that.

`php visualize command-name command-options...`.

# Commands list
- [Install](#install)
- [Global](#glboal)
- [Serve](#serve)
- [Build](#build)
- [New page](#new-page)


# Install
This command should be used only once, after downloading the framework as it will start installing the necessary packages and preparing the framework to make it ready for development.

`php visualize install`


# Global
Set the global configurations for the cli options

`php visualize global <options list>`

i.e

`php visualize global --colored --silent=false --baseApp=myAppName`

## Available options

| command     | Default   | Description                                                                                                                                                  |
| ----------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `--colored` | **true**  | Display the message colored. In git bash, it might display `ANSI` code instead of the actual color, so you can disable/enable as you want. `--colored=false` | `--colored=true`. |
| `--silent`  | **false** | A `peep` sound will be triggered each time a command is finished.                                                                                            |
| `--baseApp` | **blog**  | Set the default application name. `--baseApp=myAppName`                                                                                                      |

# Serve
This command is used to lunch the application in the browser, observe any file updates and recompile the [Smart Views](./smart-views.md) on any update.

`php visualize serve`.

It's **recommended** to use this command while you're developing your application(s).

# Build
This command is used to rebuild the application files that will be displayed in the html page.

Use this command when you create new `js` file or when you update any `package.json`

> The [serve command](#serve) does that for you automatically.

`php visualize build {appName}`.

i.e

`php visualize build blog`.

Or you can use it without the application name as the cli tool will use the default application name

i.e

`php visualize build`

# New page
To create new page you could use it like this:

`php visualize new:page posts`

This will create new folder in the `pages` directory in your application with all necessary files.

```

src/apps/appName/components/pages/posts
└─── html
     └─── page.html
└─── js
     └─── Posts.js
└─── scss 
│    └─── common
│         └─── desktop.scss
│         └─── mobile.scss
│    └─── ltr
│         └─── desktop.scss
│         └─── mobile.scss
│    └─── rtl
│         └─── desktop.scss
│         └─── mobile.scss
│    └─── rtl // create only sass files 
```

Also a new route will be added automatically in the `routing.js` file

In our example the following code will be added after `// add your routes here`:

```javascript
router.add('/posts', PostsPage, {
    baseView: 'posts'
});
```

> Please note if the `// add your routes here` line is not in your `routing.js` file , the cli tool won't be able to add the route for you, you'll have to add it by yourself in that case.

You can set the route if it is not the same as the page name.

**For example:**

`php visualize new:page posts/new-post --route=/posts/new`

This will create a new folder `posts` if not exists in the `pages` directory then `new-post` folder.

> For git bash users in windows, you've to escape the trailing slash as git bash will set the full path for it. i.e `php visualize new:page posts//new-post --route=//posts//new`.


# New smart page
This will create the same exact page structure as in the [new page command](#new-page) but instead of the `html` directory it will be `smart-views`.

See more details about [Smart Views](./packages/smart-views.md).  

Also the javascript class will extend `Smart.page` instead of `Layout.page`.

`php visualize new:smart-page posts`

# Build smart views
Smart views won't be rebuilt unless you're running the `serve` command.

But you may recompile all of the smart views using the following command:

`php visualize build:smartViews`

# New application

If You're going to develop new application in the same framework directory, you can use the following command line to create the new application files and settings automatically.

`php visualize new:app {appName}`

i.e

`php visualize new:app admin`

You can set the following options as well

`php visualize new:app admin --path=/admin --locale=en --locales=en,ar --title=en:Admin,ar:AdminInArabic`

Once the cli finishes the application build, go to `config.json` and adjust your settings if you want.

## Options description
- `--path` the application base root.
- `--locale` the default locale code
- `--locales` list of the available locales in the application separated by comma.
- `--title` the default application title in each locale. the title syntax is: `--title=localeCode:title,anotherLocaleCode:anotherTitle`.


# Produce
Once you've finished your development, you're ready now to generate the production files for your application

`php visualize produce {appName}`

i.e

`php visualize produce blog`.