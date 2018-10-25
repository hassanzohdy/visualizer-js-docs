# Visualizer JS (Version 1.0)
> [Visualizer JS](https://github.com/hassanzohdy/visualizer-js) is a javascript framework for frontend development

# Table Of Contents
- [Visualizer JS (Version 1.0)](#visualizer-js-version-10)
- [Table Of Contents](#table-of-contents)
- [Requirements](#requirements)
- [Installation](#installation)
- [Getting started](#getting-started)
- [Packages](#packages)
- [Available packages](#available-packages)
- [Production](#production)

# Requirements
- PHP >= 7
- Composer
- Node Js 

# Installation
- Download
- Run `php visualize install`

# Getting started
After a successful installation of the framework, let's try to use it.

Edit the `config.json` file and update the `baseUrl.development` to match the current directory name.

i.e `http://localhost/visualizer-js`

Where `visualizer-js` is your root directory.

Now let's start run our application.

Run the following command to start the application automatically.

`php visualize serve`

Or 

`php visualize serve appName` which would be `blog` by default.

Once the application is ready to be lunched, the application will be opened in the browser.

You will see `Visualizer JS` in the middle of the page.

# Packages
The entire framework is a set of packages **components** that makes you create your frontend application easily

For more details about how to create a package and what is package consists of click [here to understand how packages work](./package.md).

# Available packages
For full list of the available packages in the framework [click here](./packages-list.md).

# Production
Now to generate the production files run the following command
`php visualize produce app-name`

For example
`php visualize produce blog`

Then change the environment in config.json file to `production`.

And now you're ready!
