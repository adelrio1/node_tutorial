## Node Notes
**Resources include:**
  * [Node.js](https://nodejs.org/en/)
  * [Node Guide](http://nodeguide.com/)
  * [Tutorials Teacher](http://www.tutorialsteacher.com/nodejs/what-is-nodejs)
  * [The Node Beginner Book](http://www.nodebeginner.org/)
  * [Code Mentor](https://www.codementor.io/olatundegaruba/nodejs-restful-apis-in-10-minutes-q0sgsfhbd)

### Background
  Node.js is simultaneously a runtime environment and a library. Rather than relying on the browser, Node.js allows for a JavaScript backend to be run server-side. This means even-driven asynchronous calls, agnostic of the environment.

### Basics
  * Buffer - an additional data type mainly used to store binary data while receiving packets over the network.
  * Process Object - object which retains all the information  about the current process
  * Global Scope - Node.js defaults to local.
    * must use import/export to add something to the global scope
  * Stack
    * HTTP server
    * Router
    * Request data handlers
    * View logic
    * Upload handling


### Node REPL
  Read - Eval - Print - Loop

  | REPL Command     | Description                              |
  |------------------|------------------------------------------|
  | .help            | Display help commands                    |
  | tab keys         | Display list of comands                  |
  | up/down          | See previous commands                    |
  | .save <filename> | Save current Node REPL session to a file |
  | .load <filename> | Load specified file                      |
  | ctrl + c         | Terminate current command                |
  | ctrl + c (twice) | Exit REPL                                |
  | ctrl + d         | Exit REPL                                |
  | .break           | Exit multiline expression                |
  | .clear           | Exit multiline expression                |


### Modules
1. Core Modules - modules inherent to Node.js
    * To load a module: ` let module = require('module');`
    * These are compiled and loaded when the Node.js process starts

    | Core Module | Description                                   |
    |-------------|-----------------------------------------------|
    | http        | classes, methods, and events to create server |
    | url         | methods for URL parsing                       |
    | querystring | deals with query                              |
    | path        | deals with file path                          |
    | fs          | classes, methods, and events for file I/O     |
    | util        | useful functions                              |


2. Local Modules - provide different functionalities. distributed by the community.

    * Writing a module

      log.js
      ```
      var log = {
            info: function (info) {
                console.log('Info: ' + info);
            },
            warning:function (warning) {
                console.log('Warning: ' + warning);
            },
            error:function (error) {
                console.log('Error: ' + error);
            }
          };

      module.exports = log
      ```

    * Loading a module

      app.js
      ```
      var myLogModule = require('./Log.js');

      myLogModule.info('Node.js started');
      ```

3. module.exports
  * literals

    message.js
    ```
    module.exports = 'Hello world';

    //or

    exports = 'Hello world';
    ```

    app.js
    ```
    var msg = require('./Messages.js');

    console.log(msg);
    ```

  * exports - an object which can have methods attached.

    message.js
    ```
    exports.SimpleMessage = 'Hello world';

    //or

    module.exports.SimpleMessage = 'Hello world';
    ```

    app.js
    ```
    var msg = require('./Messages.js');

    console.log(msg.SimpleMessage);
    ```


### Node Package Manager: npm
  Online repository for open-source packages which provide useful modules for Node.js
  [Official Site](https://www.npmjs.com)
  [Docs](https://docs.npmjs.com/)

  * `npm install`
  * `npm install <package name>`
  * `npm install <package name> --save` - adds dependency to package.json
  * `npm install -g <package name>` - installs package globally
  * `npm update <package name>` - updates package
  * `npm uninstall <package name>` - uninstalls package

  package.json
  ```
  {
    "name": "NodejsConsoleApp",
    "version": "0.0.0",
    "description": "NodejsConsoleApp",
    "main": "app.js",
    "author": {
      "name": "Dev",
      "email": ""
    },
    "dependencies": {
      "express": "^4.13.3"
    }
  }
  ```


### Building a server
  The Node.js is a single process server, which runs the code in a single thread. This means less resources than a multi-threaded/multi process server. An event loop runs asynchronously, executing the response when the job completes.

  ```
  let http = require("http");

  let onRequest = (request, response) => {
    response.writeHead(200, {"Content-Type": "text/plain"});
    response.write("Hello World");
    response.end();
  };

  http.createServer(onRequest).listen(8888);
  ```

  1. Import the core http module from Node.js
  2. Handle incoming requests
  3. Create Server (passed callback for when there is a request)
    * request: gets information about current HTTP request
    * response: used to send a response for HTTP request
  4. Listen for incoming requests
