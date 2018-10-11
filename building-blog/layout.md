# Layout and pages
Now we will start our journey with the layout component.

# Table of contents
- [Creating layout class](#creating-layout-class).
- [Creating Partials](#creating-partials).
- [Registering Partials](#registering-partials).
- [Creating home page](#creating-home-page).

# Creating layout class 
First we need to create the `AppLayout.js` in `layout/layout/js` directory.

### Now lets head to The layout class
`layout/layout/js/AppLayout.js`

```javascript
class AppLayout extends Layout {}
```

Here we extended the core  [layout class](./../components/layout.md) but we will leave it empty for now as all what we need from it will be in the `layout core component`.

Now lets head back to our `BlogApp` class to register our layout component

> Please note that this layout component will be registered as a `mainComponent` because the layout component could be used directly without extending it.

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
        this.newComponent(new AppLayout);
    } 

    /**
     * Register app components
     * 
     * @returns void
     */
    registerAppComponents() {

    } 
}
```

So, when we need here to do is to register our `AppLayout` class as new component in our application using [newComponent() method](./../application.md#new-component).

From this point after we registered our layout component we can easily get the layout object from anywhere in the application by the key `layout`. For example: `this.app.layout.header.doSomething()`.

# Creating Partials
Now lets create our four partials components and register it to our layout.

### Breadcrumb partial `layout/common/breadcrumb/js/Breadcrumb.js` 

```javascript
class Breadcrumb extends Layout.Partial {
    /** 
    * Define the breadcrumb configurations
    * 
    * @returns void
    */
    bootstrap() {
        this.name = 'breadcrumb'; // the name of the partial that will be accessible through the layout object
    }    
}
```

Here we created the `Breadcrumb` class that extends [Layout.Partial](./../components/layout.md#partial-component) class.

The `bootstrap()` method is where we set our configurations for the class.
The only required property here is `name` property as this one defines the partial name that will be used to access the object from anywhere through the layout component

After we set our configurations in `bootstrap()` method, now we will create `init()` that will be called only once the layout is ready to be published

```javascript
class Breadcrumb extends Layout.Partial {
    /** 
    * Define the breadcrumb configurations
    * 
    * @returns void
    */
    bootstrap() {
        this.name = 'breadcrumb'; // the name of the partial that will be accessible through the layout object
    }   

    /** 
    * Initialize the object
    * 
    * @returns void
    */
    init() {
        // do whatever you want here like sending request to some api or whatever you want 
    }    
}
```

### Footer partial `layout/common/footer/js/Footer.js` 

```javascript
class Footer extends Layout.Partial {
    /** 
    * Define the footer configurations
    * 
    * @returns void
    */
    bootstrap() {
        this.name = 'footer'; 
    }    
}
```

### Header partial `layout/common/header/js/Header.js` 

```javascript
class Header extends Layout.Partial {
    /** 
    * Define the header configurations
    * 
    * @returns void
    */
    bootstrap() {
        this.name = 'header'; 
    }    

    /** 
    * Initialize the object
    * 
    * @returns void
    */
    init() {
        // do whatever you want here like sending request to some api or whatever you want 
    }    
}
```

### Menu partial `layout/common/menu/js/Menu.js` 

```javascript
class Menu extends Layout.Partial {
    /** 
    * Define the Menu configurations
    * 
    * @returns void
    */
    bootstrap() {
        this.name = 'menu'; 
    }    

    /** 
    * Initialize the object
    * 
    * @returns void
    */
    init() {
        // For example, get from the backend the menu of all categories 
    }    
}
```

# Registering Partials
After we created our partials, now we will register it on our layout component.

Lets for instance create `registerLayoutComponents()` and we will call it on `registerAppComponents()` method.

### `BlogApp` class

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
        this.newComponent(new AppLayout);
    } 

    /**
     * Register app components
     * 
     * @returns void
     */
    registerAppComponents() {
        this.registerLayoutComponents();
    } 

    /**
     * Register layout pages and partials
     * 
     * @returns void
     */
    registerLayoutComponents() {
        // register partials
        this.layout.newPartial(new Header);
        this.layout.newPartial(new Menu);
        this.layout.newPartial(new Breadcrumb);
        this.layout.newPartial(new Footer);
    } 
}
```

Here we registered all of our partials using [newPartial() method](./../components/layout.md#new-partial).

From now on, we can access any partial like this: `this.layout.header.name` or whatever we need to do with the class.

> Please note that the order of  registering partials will differ only on the order of executing `init()` method but won't affect the order of rendering as we will custom the way of rendering each partial differently.

> Please note that the allowed partials are: `header`, `breadcrumb`, `footer`, `menu` and `sidebar` and every component MUST have its name to function properly.

# Creating home page
We will create now our first page which will be the home page.
the location of the component will be `myBlog/components/pages/home`.

the `HomePage` class will be created in the `js` folder so the file path will be `myBlog/components/pages/home/js/HomePage.js`

### `HomePage` class

```javascript
class HomePage extends Layout.Page {

}
```

Any page should extend the [Layout.Page class](./../components/layout.page.md).

Next, we will define everything we need about the home page on the `bootstrap()` method like we did in our partials.

```javascript
class HomePage extends Layout.Page {
    /** 
    * Set page configurations
    * 
    * @returns void
    */
    bootstrap() {
        this.name = 'home'; 
        this.route  = '/';
        this.baseView = 'pages/home';
        this.endpointOptions = {
            method: 'GET',
            route: '/',
        };
    }    
}
```

So now what we did is we defined some properties that we need for page to render it.

For full details about available properties for the page component, go to [Layout.Page properties](./../components/layout.page.md#properties).

The `name` of the page usage will be as the partials name usage but the extra thing here is the body of the page id will be changed to `home-page` so we can easily set our styling for the home page only without doing any conflict with other pages.

And the `route` property will be the route of the page that the user will open from the navigation bar to access the page which here by default will be the app location on our domain like `localhost/my-blog`.

The `this.baseView` will be the path of our views directory so we can use [this.view(viewName)](./../components/layout.page.md#view-method) method to render any view easily.

For more details [Layout.Page properties](./../components/layout.page.md#properties).

If we set the property `endpointOptions` then we will send a request via the [Endpoint Component](./../components/endpoint.md).

For full list of `endpointOptions`, please visit the [Endpoint.send(options) method options](./../components/endpoint.md#send).

As we've set our `endpointOptions`, now we can use [render(response)](./../components/layout.page.md#render) method for success response and [error(response, statusCode)](./../components/layout.page.md#error) method to handle the response error.

```javascript
class HomePage extends Layout.Page {
    /** 
    * Set page configurations
    * 
    * @returns void
    */
    bootstrap() {
        this.name = 'home'; 
        this.route  = '/';
        this.baseView = 'pages/home';
        this.endpointOptions = {
            method: 'GET',
            route: '/',
        };
    }
    
    /**
     * Render success response
     * 
     * @param object response
     * @returns string
     */
    render(response) {
        this.response = response;

        return this.view('page');
    }
    
    /**
     * Render error response
     * 
     * @param object response
     * @param int statusCode
     * @returns string
     */
    error(response, statusCode) {
        // manage your error here
    }
}
```

### Registering home page to layout
After we created our home page, we need to register it to our layout in the application class using the [Layout.newPage method](./../components/layout.md#new-page).

### BlogApp class

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
        this.newComponent(new AppLayout);
    } 

    /**
     * Register app components
     * 
     * @returns void
     */
    registerAppComponents() {
        this.registerLayoutComponents();
    } 

    /**
     * Register layout pages and partials
     * 
     * @returns void
     */
    registerLayoutComponents() {
        // register partials
        this.layout.newPartial(new Header);
        this.layout.newPartial(new Menu);
        this.layout.newPartial(new Breadcrumb);
        this.layout.newPartial(new Footer);

        // register pages
        this.layout.newPage(new HomePage);
    } 
}
```

Now the `HomePage` class can be accessed through layout object like `this.layout.home`.


# Next Step
[Creating layout, partials and home page views](./creating-layout-views.md).