# Views

Visualizer JS is shipped with a powerful view and putting the ease of use into considerations as well.

Views are normal html files with `special` features that makes it easier to render dynamic data, but still its just **HTML** file!

# Package info

Package: `core/view`.

Parent Package: [core](./core.md).

Required: **Yes**.

Dependencies: [Application](./application.md).

Alias: `view`.

# Table of contents
- [Views](#views)
- [Package info](#package-info)
- [Table of contents](#table-of-contents)
- [View Path system](#view-path-system)
    - [View path syntax](#view-path-syntax)
- [Types of views](#types-of-views)
    - [App views](#app-views)
        - [Syntax](#syntax)
        - [Example](#example)
    - [Framework/Plugins](#frameworkplugins)
        - [Syntax](#syntax)
        - [Example](#example)
- [Passing data to view file](#passing-data-to-view-file)
- [Control structure](#control-structure)
    - [If and else if](#if-and-else-if)
- [For loops](#for-loops)
    - [Break/Continue](#breakcontinue)
- [Inline loops and conditions](#inline-loops-and-conditions)
- [Writing Javascript code inside the view file](#writing-javascript-code-inside-the-view-file)
    - [let and var](#let-and-var)
        - [Example](#example)
    - [Writing custom statement](#writing-custom-statement)
    - [Multiple javascript code lines](#multiple-javascript-code-lines)
        - [@echo](#echo)
- [Using custom scope](#using-custom-scope)
- [Elements events](#elements-events)
    - [Element target](#element-target)
- [Special attributes](#special-attributes)
        - [Boolean attributes](#boolean-attributes)
        - [Syntax](#syntax)
        - [Example](#example)
    - [Available boolean attributes](#available-boolean-attributes)
- [Special classes](#special-classes)
    - [Syntax](#syntax)
- [Styling](#styling)
    - [Syntax](#syntax)
        - [Example](#example)
    - [Available properties](#available-properties)
    - [Passing style object](#passing-style-object)
        - [Example](#example)
    - [Passing object of html attributes](#passing-object-of-html-attributes)
        - [Syntax](#syntax)
        - [Example](#example)
- [Nested views](#nested-views)
- [Restrictions](#restrictions)

 # View Path system
 Calling view is extremely simple as you can call any view from anywhere in the application, all you've to do is to call the proper function based on your [view type](#types-of-views).

 ## View path syntax

 For any package or even in the application, all views **MUST** be set in `html` folder with `.html` extension.


# Types of views

There are two main types of views:
- App views.
- Framework/Plugins views.

They both has same functionality but the only difference is how to call each type.

## App views

 So let's assume we've in our `app` directory a folder with `users` name and the folder contains a `list.html` view file in the `html` directory.

 To render any view file, use the `render` function from anywhere in the application

 ### Syntax
 `render(string viewPath, object data = {}, object scope = app)`

 Returns: `String`.

### Example

 In this case to call that view file which the full path of the file will be as follows:

 ```
/ui/apps/my-app/components/users/html/list.html
 ```

 **All of app views paths starts after the components directory**.

 So we will treat our view path only with the following part of the path

 ```
 users/html/list.html
 ```
Now we will ignore any `html` word in our directory, the `html` folder name and `.html` the file extension.

So when we wants to call that file the **final path** will be:

```
users/list
```

To call any view inside our app directory we will use the `render` function.

So the view html content will be called like this:

```
let usersView = render('users/list');
```



## Framework/Plugins
Actually we won't say much more than what has been said in the App views section but only couple notes.

- To get the view of any package inside the framework or plugins directory, we will use the `view` function instead of `render` function.
- The plugins views path **MUST** starts with `plugins` before the view path.

 To render any view file, use the `view` function from anywhere in the application

 ### Syntax
 `view(string viewPath, object data = {}, object scope = app)`

 Returns: `String`. 

### Example

Let's say we want to get the `alert` package view `prompt.html` which is in the framework packages.

The full path of the html file we wants is:

```
/ui/visualizer/alert/html/prompt.html
```
Our view path will start after the `visualizer` segment so our view path will look like:

```
alert/html/prompt.html
```

As we said earlier, we will truncate any `html` word in our path, the directory name and the file extension.

So our final path will be:

```
alert/prompt
```

To call it from anywhere inside our application we can do it as follows:

```
let alertPromptView = view('alert/prompt');
```

For plugins, it will be the same thing exactly but we will add `plugins/` at the beginning of the view path.

So if we've a plugin called `my-plugin` in the `plugins` directory and that plugin has a view file called: `data-print.html` So the full path of that view file will be:

```
/ui/plugins/my-plugin/html/data-print.html
```
To render that view it will be like this:

```
let printableDataView = view('plugins/my-plugin/data-print');
```

# Passing data to view file

Now Let's continue in our example of the users list page, let's assume we want to display all users.

To print any variable inside the html file, put in curly braces : `{{ statementOrVariableOrFunctionCall }}`

Our users list view path is: `users/list`

So in our app.js we will call it:

```
let usersHtml = render('users/list');
```

Let's pass some data to that view:


```
let name = 'hasan',
    email: 'hassanzohdy@gmail.com';

let usersHtml = render('users/list', {
    name: name,
    email: email,
});
```

Now we passed in the second argument the that we're going to use inside the view, as the key of the object will be the variable that will be used in the html file.

Now let's open our `list.html` file

```html
<h1>Hello {{ name }}</h1>
<h3>
    This is your email address 
    {{ email }}?
</h3>
```

The output of the file will be:
```html
<h1>Hello hasan</h1>
<h3>
    This is your email address 
    hassanzohdy@gmail.com?
</h3>
```


We can of course name it as we want but it has to be **valid variable name**.



```
let name = 'hasan',
    email: 'hassanzohdy@gmail.com';

let usersHtml = render('users/list', {
    myName: name,
    myEmailAddress: email,
});
```

```html
<h1>Hello {{ myName }}</h1>
<h3>
    This is your email address 
    {{ myEmailAddress }}?
</h3>
```



# Control structure

Sometimes we want to do some `logical` operations or even loops inside our html code to display certain data based on the given conditions.

Any of the following control structures must be in single line and the line **MUST NOT** contain any other code.

## If and else if

We can use the `if` control structure inside the view as follows:

```html
if (boolean-expression)
    do|write anything here
else if (another-boolean-expression)
    do|write another thing here
endif
```

So let's continue in our example:

`users/lists.html`

```html
if (myName == 'hasan')
    <h1>Welcome Back Boss!</h1>
else 
    <h1>Welcome {{ myName }}</h1>
endif
```

# For loops

As the application grows up, we need to iterate over some data to be displayed, like the list of users in our example.

So let's pass new array to our view to iterate over it.

`app.js`

```javascript

let name = 'hasan',
    email: 'hassanzohdy@gmail.com',
    usersData = [{
        id: 1,
        name: 'Hasan Z',
        age: 26,
    }, {
        id: 51,
        name: 'John doe',
        age: 18,
    }];

let usersHtml = render('users/list', {
    myName: name,
    myEmailAddress: email,
    users: usersData,
});

```

Now let's go to our view file

`list.html`


```html
if (myName == 'hasan')
    <h1>Welcome Back Boss!</h1>
else 
    <h1>Welcome {{ myName }}</h1>
endif

<table>
    <thead>
        <tr>
            <th>ID</th>
            <th>Name</th>
        </tr>
    </thead>
    <tbody>
        for (let user of users)
            <tr>
                <td>{{ user.id }}</td>
                <td>{{ user.name }}</td>
            </tr>
        endfor
    </tbody>
</table>

```

## Break/Continue

As we're using `for` loops,  sometimes you want to break or continue the loop based on certain conditions.

In the same example, let's say we will add the `edit ` and delete` buttons but the delete button will be displayed only if the current user name is `hasan`.



```html
if (myName == 'hasan')
    <h1>Welcome Back Boss!</h1>
else 
    <h1>Welcome {{ myName }}</h1>
endif

<table>
    <thead>
        <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Actions</th>
        </tr>
    </thead>
    <tbody>
        for (let user of users)
            <tr>
                <td>{{ user.id }}</td>
                <td>{{ user.name }}</td>
                <td>
                    <button>Edit</button>
                    if (myName != 'hasan')
                        continue
                    endif
                    <button>Delete</button>
                </td>
            </tr>
        endfor
    </tbody>
</table>

```

So in that example, we added new condition if the current user which will be the value of `myName` doesn't equal to `hasan` then we will continue to the next iteration without displaying the `delete` button.

> `continue ` | `break` **MUST** be written in the line without anything else beside it and it can't be in the same line of the `if` condition.


> **Tip**: You don't have to indent lines inside any control structure but it is just for styling.

# Inline loops and conditions

Inline loops and conditions work with simple data that will be displayed in one line.

For example if we've something like this:

```
 if (name == 'hasan')
    <h1>Welcome back hasan!</h1>
 endif
```

We can write it in one line:

```
<h1 *if="name == 'hasan'">Welcome back hasan!</h1>
```

This is a simple and easy way to print some data that doesn't require much code.

All we've to do is to add our condition inside the `*if` directive as if the condition is true, the whole `h1` tag will be printed, otherwise, it won't be added to the dom at all.

Formal syntax:
```
<tag *if="boolean-expression"></tag>
```

> Please note that this won't work with tha tag that is closed in the second line, the whole tag **MUST** be written in one line.

We can also do inline `for-loops` in the same way.

This form:

```
<li *for="let user of users">{{ user.name }}</li>
```

is equivalent to the following code

```
for (let user of users)
    <li>{{ user.name }}</li>
endfor
```

As mentioned earlier, these directives work only in one line so the following code **won't work** as expected:


```
<li *for="let user of users">
    {{ user.name }}
</li>
```
# Writing Javascript code inside the view file

One of the amazing features in this view engine that we can write javascript code inside it which is **not recommended** as you should do your logic code inside your `js` files.

But sometimes you want to use it for proper usage.

Here is the available options:

## let and var

You can declare variables inside the html code by writing the statement only in single line.

### Example
What if we've a `user` object that was passed to our view and we want to print all of its properties using a `for` loop

We can do it like this:

```
    for (let key in user)
        let value = user[key];

        <h1>{{ value }}</h1>
    endfor
```

This applies to the `var` statement and they both are `interchangeable`.

## Writing custom statement

What if there is a string that we need to add to it another string or even call method inside the view.

using the `@js` directive in a separate line.
For example if we've a `price` variable that we want to add 10% taxes for it.

```
@js(price += price * 0.1)
```

## Multiple javascript code lines

If you want to write more than one javascript line in your view use the following syntax:

```html
<h1>Hello, World!</h1>

startJs
    let myName = 'hasan';
    // do something else....
endJs

<h1>{{ myName }}</h1>
```

So all you've to do is to wrap your code between the `startJs` and `endJs` lines.

### @echo

To log any variable inside the view file, you can use the `@echo` directive to console log the value

```
@echo(users) 
```

# Using custom scope 

We can assign the html view to any `scope` we want so we can use the `this` keyword inside it.

To define the view `scope`, pass the object that will be used as third argument to the `render` or the `view` function.

Let's say this is our `Users.js` class

```javascript

class Users {
    /**
     * Constructor
     */
    constructor() {
        this.heading = 'Users List';
    } 

    /**
     * Display users list
     */ 
    list() {
        let data = {
            name: 'hasan',
        };

        let usersView = render('users/list', data, this);
    }
}
```

Now in our `users/list` view.

```html
<h1>{{ this.heading }}</h1>
<h2>Welcome {{ name }}</h2>
```

Output


```html
<h1>Users List</h1>
<h2>Welcome hasan</h2>
```


As you can see, we used the data that was sent in the `data` object, and also we used the `Users` object as a `scope` of the view .

> The default scope of any view file is the `App` object which is in the `app.js` file.

# Elements events

We can easily attach any event to any element in the dom using jQuery, but it won't work until the dom is rendered in the page.

To make our events work properly, which in this case when the view file is `rendered` in the dom , we can attach events to any element and use our `scope` to handle these events.


```html
<table>
    <tbody>
        for (let user of users)
            <tr>
                <td>{{ user.id }}</td>
                <td>{{ user.name }}</td>
                <td>
                    <button type="button" (click)="this.editUser(user)">Edit</button>
                    <button type="button" (click)="this.deleteUser(user)">Delete</button>
                </td>
            </tr>
        endfor
    </tbody>
</table>
```

So now we attached to event listeners, one for editing and the other for deleting user.

In our `Users.js` file

```javascript
class Users {
    editUser(user) {
        // edit user info.
    }

    deleteUser(user) {
        // Send a request to backend to delete user.
    }
}
```

We passed the `user` object to both of our methods inside our for loop.

> All types of dom events could be used like: click, change, mouseover, mouseleave...etc.

## Element target
If we want to get the `dom` object of the current element tag, pass to your method the special variable `$el` to work with it.


`list.html`

```html
<button id="my-button" (click)="this.handleButton($el)">My Button</button>
```

`Users.js`

```javascript
class Users {
    handleButton(button) {
        console.log(button.id); // my-button
    }
}
```


# Special attributes

We're not done yet!, There are some special attributes that will help you writing less code and a lot of stuff for you.

All special attributes are written between square brackets `[attribute]="value"`

### Boolean attributes
Boolean attributes are html attributes that either to be true or false, we're going to use the `disabled` attribute for our demonstration and it applies for all other boolean attributes.

Add the `disabled` attribute or not based on the given boolean value

### Syntax
`[booleanAttribute]="boolean-expression"
`
### Example
`list.html`
```html
let accountType = 'admin';
let hasFullAccess = false;

<button [disabled]="accountType != 'admin'">Control users</button>


<button [disabled]="hasFullAccess">I've full access!</button>

```

The output will be:

```html
<button>Control users</button>
<button disabled="disabled">I've full access</button>
```

Because `hasFullAccess` variable is a `boolean` value then we don't need to check for it 

## Available boolean attributes
- disabled
- readonly
- selected
- checked
- multiple

# Special classes

## Syntax

`[class]="{className: boolean-expression, anotherClassName: boolean-expression}"
`
So we may face situations that we want to add certain classes based on certain value.

For example, if we're building an ecommerce application, we want to check the status of the product whether if it `in-stock` or `out-of-stock` and based on its value we will add a `success` class for `greent` color or `danger` class for `red` color.

```html
let status = 'in-stock';

<span class="font-weight-bold" [class]="{success: status == 'in-stock', primary: status == 'out-of-stock'}">
    Product status: {{ status }}
</span>
```

Output
```html
<span class="font-weight-bold success">
    Product status: {{ status }}
</span>
```

# Styling

Inline styling is also available here in a simple form.

## Syntax
[styleProperty]="value"

### Example

```html
<h1 [color]="#F00">Red color</h1>
```

Output


```html
<h1 style="color:#F00;">Red color</h1>
```

## Available properties
- color
- border
- background
- width
- height

## Passing style object

In some cases, users have some preferences in their web page design as they may have the control of styling their elements.

Also in other situations, some styles are stored in database, for example to allow the administrator to control the background, color, border of the mega menu.

To pass an object of style to any element use the [style] directive to be parsed into the element inline style.

### Example

`Users.js`

```javascript
class Users {
    viewInfo() {
        let userNameStyling = {
            background: 'green',
            color: 'white',
            border: '1px solid #333',
        };

        let data = {
            name: 'hasan',
            userNameStyling: userNameStyling,
        };

        render('users/list', data);
    }
}
```

`list.html`

```html
<h1 [style]="userNameStyling">Hello {{ name }}</h1>
```

Output
```html
<h1 style="background: green; color: white;border: '1px solid #333';">Hello hasan</h1>
```

> **Note**: Only one styling directive is allowed per tag element.

## Passing object of html attributes
Same thing happens with HTML attributes, as you may need to pass a key/value pairs contained in object to an html tag and want it to be parsed as attributes.

### Syntax

`[attrs]="attributesObject"`

### Example

`Users.js`

```javascript
class Users {
    list() {
        let data = {
            myAttributes: {
                id: 'element-id',
                class: 'btn btn-success',
                'data-user-id': 421,
            }
        };

        render('users/list', data);
    }
}
```

`list.html`

```html
<h1 [attrs]="myAttributes">Hello, World</h1>
```

Output


```html
<h1 id="element-id" class="btn btn-success" data-user-id="421">Hello, World</h1>
```


# Nested views
One of the mostly useful advantages in our view engine is `nested views` which means you can `inject` or `call` view inside another view

Let's take our `list.html` for example

`list.html`

```html
if (myName == 'hasan')
    <h1>Welcome Back Boss!</h1>
else 
    <h1>Welcome {{ myName }}</h1>
endif

<table>
    <thead>
        <tr>
            <th>ID</th>
            <th>Name</th>
        </tr>
    </thead>
    <tbody>
        for (let user of users)
            <tr>
                <td>{{ user.id }}</td>
                <td>{{ user.name }}</td>
            </tr>
        endfor
    </tbody>
</table>
```

What if we want to separate the `record` in another view to make it easier to manipulate with?

So we can make our file looks like this

`list.html`

```html
if (myName == 'hasan')
    <h1>Welcome Back Boss!</h1>
else 
    <h1>Welcome {{ myName }}</h1>
endif

<table>
    <thead>
        <tr>
            <th>ID</th>
            <th>Name</th>
        </tr>
    </thead>
    <tbody>
        for (let user of users)
            {{ render('users/record', {user: user}) }}
        endfor
    </tbody>
</table>
```

`users/record.html`


```html
<tr>
    <td>{{ user.id }}</td>
    <td>{{ user.name }}</td>
</tr>

```

**Pretty neat, right?**

We could also do it like this


`list.html`

```html
if (myName == 'hasan')
    <h1>Welcome Back Boss!</h1>
else 
    <h1>Welcome {{ myName }}</h1>
endif

{{ render('users/table', {users}) }}
```

`users/table.html`

```html

<table>
    <thead>
        <tr>
            <th>ID</th>
            <th>Name</th>
        </tr>
    </thead>
    <tbody>
        for (let user of users)
            {{ render('users/record', {user: user}) }}
        endfor
    </tbody>
</table>
```

> Don't forget to pass the third argument for any `render` function if you want to define the `scope of the view`. 

# Restrictions

There are few restrictions or `invalid view syntax` that you should avoid while using your view

Which will be something like the tick ` as this is a reserved character for matching variables

So the following syntax will raise an error

`list.html
```html
<h1>Hello, World!</h1>

This is just a simple text with a `wrong` syntax
```
