+++
author = "Frank Adrian"
comments = true
cover = ""
date = "2019-02-26T23:00:00+00:00"
tags = ["angular", "web-development", "webpack", "typescript"]
title = "Lazy Load 3rd party scripts in lazy loaded Angular module with webpack"

+++
# How to lazy load 3rd party scripts globally in Angular using Typescript and webkit

  
We are busy migrating our web app from AngularJS 1.6 all the way up to Angular 7.   
For this we needed to migrate our ImageEditor module which allows users to customise images in the web app. For this module we relied on the [TUI image editor](https://github.com/nhnent/tui.image-editor) plugin. 

Since this module is not needed on bootstrap we decided to lazy load it and wanted to have the vendors lazy load as well to optimise our apps startup time.

It turned out to be rather easy to do this with `script-loader` npm package:

1) Install it by running `npm install script-loader --save-dev` 

2) Remove loaded scripts from `angular.json` scripts array

3) import the script(s) at the top of the file or module you need it: 

    import 'script-loader!../../../scripts/libs/fabric.js';

    import 'script-loader!../../../../node_modules/tui-code-snippet/dist/tui-code-snippet.js';

    import 'script-loader!../../../scripts/libs/tui-image-editor.js';

(We had some scripts saved locally and some in node_modules. This approach works for both use cases).

This loads the specified script into the global window namespace and hence is also available to other vendors that require the global namespace (in this case `tui`) to be present.

The advantage of this approach is that we still benefit from tree shaking when we build the project using the angular cli.