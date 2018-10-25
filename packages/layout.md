# Layout
The layout package is the responsible package for handling any page or partial in your application.

In other words, It manages the application views.

# Package info

Package: `core/layout`.

Parent Package: [core](./core.md).

Required: **Yes**.

Components: [Layout](#layout-package), [Layout Page](#layout-page), [Layout Smart Page](#layout-smart-page), [Layout Partial](#layout-partial)

# Table of contents
- [Layout](#layout)
- [Package info](#package-info)
- [Table of contents](#table-of-contents)
- [Layout package](#layout-package)
    - [The base layout](#the-base-layout)
        - [Configurations](#configurations)
    - [Accessing pages and partials](#accessing-pages-and-partials)
- [Layout Page](#layout-page)


# Layout package

Package: `core/layout/layout`.

Parent Package: [core/layout](#layout).

Required: **Yes**.

Dependencies: [Events](./events.md), [Views](./views.md) [Dom](./dom.md), [Jquery](./jquery.md) [Dom](./dom.md), [Config](./config.md).

Alias: `layout`

The layout is the middleware between the [Router](./router.md) class which checks that is the proper page to be loaded based on the current route and the page that should be loaded.

It's also responsible for setting the content of any [Partial](#layout-partial-package) in the dom.

## The base layout
As the framework generates the full page layout, you've the ability to define what to be set in the `body` tag for your application.

You can set any partials you want besides the `main` tag as this is the only required tag to be set in your layout structure file.

### Configurations
In the [app configurations](./config.md) you can set your `basePath` under the `layout` key.

`config.js`
```javascript

Config.extend({
    layout: {
        basePath: 'layout/layout/layout-structure',
    }
});
```

The `basePath` is the path of the layout in your application directory.

You may use more than one layout based on certain criteria.

For example, you may want to use a layout for a **non logged-in** user and another layout structure for **logged-in** user.

Let's assume the following scenario:

We're developing an admin panel and the user is not logged in, so we will display only the login page.

Once the user is logged in, we need to change the layout structure to display a **header**, **footer**, **sidebar**, **breadcrumbs** and **the page content**.

`app.js`
```javascript
/**
  * {@inheritDoc}
  */
 init() {
     let layout = DI.resolve('layout),
    user = DI.resolve('user');

    user.onLogin(() => {
        layout.rebuild('layout/layout/logged-in-layout');
    }).onLogout(() => {
        layout.rebuild('layout/layout/non-logged-in-layout');
    });
 } 
```

We may also based set the current layout based on the user login status from the beginning by passing a `callback` function to `basePath` key instead of layout path.


`config.js`
```javascript

Config.extend({
    layout: {
        basePath: () => {
            let user = DI.resolve('user');
            return user.isLoggedIn() ? 'layout/layout/logged-in-layout' :
                                       'layout/layout/non-logged-in-layout ;
        },
    }
});
```

As mentioned earlier, the base path will be determined based on the current user status.

So we may refine our user events on login or logout as follows:

`app.js`
```javascript
/**
  * {@inheritDoc}
  */
 init() {
     let layout = DI.resolve('layout),
    user = DI.resolve('user');

    user.onLogin(() => {
        layout.rebuild();
    }).onLogout(() => {
        layout.rebuild();
    });
 } 
```
By not passing any arguments to `rebuild` method, it will go and get the default value which is in the `layout.basePath` and the callback will be triggered again and check the current status of the user then it will take the proper base path accordingly.

## Accessing pages and partials
Once the application is ready, from now on you can access your pages/partials through the layout object.

The accessing key from the layout is based on the [Page name](#page-name).

i.e

```javascript
let layout = DI.resolve('layout'),
    homePage = layout.home;
```


# Layout Page

Package: `core/layout/page`.

Parent Package: [core/layout](#layout).

Required: **Yes**.

Dependencies: [Events](./events.md), [Views](./views.md) [Dom](./dom.md), [Router](./router.md)  [Layout](#layout-package).

Alias: `N/a`

The `Layout.Page` is considered as an `abstract class` as it's meant to be used fro inheritance only.

Any page should extend the layout page as it sets most of the page configurations automatically.

`HomePage.js`

```javascript
class HomePage extends Layout.Page {
    /**
     * Set the main configurations of the page
     *
     * This method is triggered only once during the request life cycle
     */
    bootstrap() {
        this.name = 'home';

        this.viewName = 'page';

        this.title = 'Home Page';
    }

    /**
     * This method is triggered once the visitors hits the home page route
     */
    init() {
        
    }

    /**
     * This method is triggered after the page content is rendered
     */
    ready() {
    }
}
```

As sometimes the view we don't want to display it until we get some data from the backend, in that case we will not set the `viewName` property in the `bootstrap` method, but instead, we'll send a request first to the backend then on the success response we'll render the page.


`HomePage.js`

```javascript
class HomePage extends Layout.Page {
    /**
     * Set the main configurations of the page
     *
     * This method is triggered only once during the request life cycle
     */
    bootstrap(endpoint) {
        this.name = 'home';

        this.title = 'Home Page';

        this.endpoint = endpoint;
    }

    /**
     * This method is triggered once the visitors hits the home page route
     */
    init() {
        this.endpoint.get('/home-data').then(response => {
            this.response = response;

            // now let's get the output of the html file.
            let myPageView = this.view('page');

            // set the output in the <main> tag to be rendered in the page. 
            this.render(myPageView);
        });
    }
}
```