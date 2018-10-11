# Framework Structure
```
Project Structure
└─── App
└─── public
│   └─── static 
└─── routes
└─── storage
└─── ui
|   └─── apps
|   └─── visualizer
|   └─── vendor
|   |── loader.json
└─── vendor
│─── .htaccess
│─── composer.json
|─── config.json
│─── index.php
|─── visualize 
```

Here is a quick description for the entire tree

## The framework compiler

Visualizer JS is built with a php framework for compiling
Which contains everything than the following directories/files:

- The `public` directory is where to place all assets and it contains:
    - `static` directory: which will be used for putting the application assets automatically
    - Any other common assets that could be used in more than one application can be placed in the `public` directory
- The `ui` directory >> the directory of our framework which will contain everything we need which contains:
    - **apps directory**: all applications should be placed in this directory
    - **visualizer directory**: Visualizer Js components
    - **vendor directory**: any 3d party plugins we need to use will be placed in this directory
    - [loader.json](./loader.md) file: the framework loader which where we will start next 
- The **config.json file** >> [The Pre Compiled Configurations File](./pre-compiled-configurations.md).
- The **visualize file** >> for compiling our application for production. 
    > Please check the [production documentation](./production.md) for further information.


   ## Next Step
   [Framework Loader: loader.json](./loader.md)