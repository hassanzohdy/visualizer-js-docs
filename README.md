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

First of, build your app, which is `blog` as it is integrated with the framework with your first installation.

`php visualize build blog`

Once it's done, go to your browse then go to `http://localhost/visualizer-js`.

You will see `Visualizer JS` in the middle of the page.

# Packages
The entire framework is a set of packages **components** that makes you create your frontend application easily

For more details about how to create a package and what is package consists of click [here to understand how packages work](./package.md).

# Available packages
For full list of the available packages in the framework [click here](./packages-list.md).

# Production
To make the production version for any application we will need to have node installed on your machine or in your server only to make the production.

After installing nodejs run the following command in root directory **Do it only once**
`npm install`

Now to generate the production files run the following command
`php visualize produce app-name`

For example
`php visualize produce blog`

Then change the environment in config.json file to `production`