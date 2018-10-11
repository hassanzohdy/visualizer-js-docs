# Creating layout views
At this point, we've just created our logic classes of the layout, partials and the home page.

Now we'll start creating the view for each component and see how to inject it in the main layout.

# Table of contents
- (Layout view)[#layout-view]
- (Header view)[#header-view]
- (Menu view)[#menu-view]
- (Breadcrumb view)[#breadcrumb-view]
- (Footer view)[#footer-view]
- (Home page view)[#home-page-view]

# Layout view
As we're extending the [Layout component](./../components/layout.md), you can find tha layout view basic structure in [Layout view](./../components/layout.md#layout-view-structrue). 

However, if you want to customize your own order of the layout, you can change it using the [Config](./../components/config.md) component Through `Config.layout.baseHtml`

#### For example in `config/js/Config.js`:

```javascript
Config.extend('layout', {
    baseHtml: render('my-own-layout-structure'),
}); 
```

> Please note that all layout tags names CAN NOT be changed.

# Header view 
Now let's head to our header class and adjust our view

####**** header.html `layout/common/header/html/header.html`

```html
<header>
    <h1>Hello, Blog!</h1>
    <!-- Write your other code here -->
</header>
```
****
as our header won't need to wait for some info from the endpoint, so we will render it instantly.

```javascript
class Header extends Layout.Partial {
    /** 
    * Define the header configurations
    * 
    * @returns void
    */
    bootstrap() {
        this.name = 'header'; 
        this.viewPath = 'layout/common/header/header';
    }    
}
```