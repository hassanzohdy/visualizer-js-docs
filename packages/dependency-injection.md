# Dependency Injection

One of the most powerful designs that is used in `Visualizer JS` is the **dependency injection** or `DI` for shorthand.

# Package Info

Package: `core/dependency-injection`.

Parent Package: [Core](./core.md).

Required: **Yes**.

Dependencies: [Support](./support.md).


# How dose it work
Once you've created your class or package, you can `register` it in the  `DI` container to be used later.

# Example

```javascript
class SmoothAlert {
    constructor() {
        // do something
    }
}

// now let's register it in our DI

DI.register({
    class: SmoothAlert,
    alias: 'smoothy',
});
```

Now we created a new class which is `SmoothAlert` that is supposed to display some popups of alerts for the user.

> Note, the `DI` class is just an alias to `DependencyInjection`, so you can use any of them as they are interchangeable.

After we're done with our class, we need to register it to our `DI` using the `register` method.

# DI.register

This method accepts one argument, an object.

The object contains the following

| Key | Required | Description |
|---|---|---|
| **class** | Yes | Set the **class name** that will be registered in the **DI container**.
| **alias** | no | Set class **alias** to be used instead of using the original class name.

# Resolving class

To `resolve` our **smoothy** class, we can do it as follows:

```javascript
let smoothyObject = DI.resolve('SmoothAlert');

// or even better, why not use our alias?
let smoothyObjectUsingAlias = DI.resolve('smoothy');
```

# Auto injection
The main key of the DI concept is to pass our `dependencies` to the class `constructor` or to any certain `method` and the `DI` will handle these dependencies automatically.

Let's say the `SmoothyAlert` class requires the [View](./views.md) object to handle create some views.



```javascript
class SmoothAlert {
    constructor(views) {
        // do something
        this.views = views;
    }
}

// now let's register it in our DI

DI.register({
    class: SmoothAlert,
    alias: 'smoothy',
});
```

As we can see now, we add only the `class alias` of the **Views** object to the constructor, our DI will automatically inject the Views object for us.

# Resolving methods

The **DI** doesn't work only with constructors, but with any method inside the class as well.

For example, in Any [Layout Page](./layout-page.md), we've the `bootstrap` method, which is resolved using the `DI` container.

For Example:


```javascript
class HomePage extends Layout.page {
    bootstrap() {
        this.name = 'home';
        this.title = 'Home Page';
    }
}
```

This is a simple structure of any page that could be in the application, now let's assume we want to use our `smoothy` class in our **Home Page**.


```javascript
class HomePage extends Layout.page {
    bootstrap(smoothy) {
        this.name = 'home';
        this.title = 'Home Page';
        this.smoothy = smoothy;
    }
}
```
That's it!, so all you've to do to use any package class is only to know the class name or even better, the class alias which is `smoothy` in that case.

You can also resolve some methods using the `DI.resolve` method like this.



```javascript
class SmoothAlert {
    constructor(views) {
        // do something
        this.views = views;
    }

    getSmoothyView() {
        return this.views.render('plugins/smoothy/box');
    }
}

// now let's register it in our DI

DI.register({
    class: SmoothAlert,
    alias: 'smoothy',
});

// now let's call the `getSmoothyView` method directly

let smoothyAlertView = DI.resolve('smoothy', 'getSmoothyView');
```
By default, the second argument of the `DI.resolve` is the `constructor` method, however, if you want to resolve another method, you can easily pass the name of the method as second argument to the method.

# Registry design pattern

The DI container works with RDP **Registry Design Pattern** which means no matter how many times you `resolve` any class, it won't create more than one object of that class.

**But**, if you want to create new `instance` of any particular class, which is not **RECOMMENDED**, you can use the `instance` method.

```javascript
// the resolve method will create only one object 
let smoothyObject = DI.resolve('smoothy');
let sameSmoothyObject = DI.resolve('smoothy');
let sameSmoothyObject2 = DI.resolve('smoothy');
let sameSmoothyObject3 = DI.resolve('smoothy');

// create new object each time we use the instance method
let smoothyObject1 = DI.instance('smoothy'); // new object is created
let smoothyObject2 = DI.instance('smoothy'); // new object is created
let smoothyObject3 = DI.instance('smoothy'); // new object is created
```