# JS engines vs Node vs npm vs nvm: Different tools in JavaScript

There are many different tools for compiling and running JavaScript codes on local computers and web browsers. Let's take a look at some differences:

- **V8** is a JavaScript engine developed by Google for Chromium-based browsers. Similarly, **SpiderMonkey** is Mozilla's JavaScript engine, for the Firefox browser. In C++ terms, V8 and SpiderMonkey would be similar to the C++ compilers, such as GCC or Clang. HOWEVER, V8 and SpiderMonkey are JIT (Just-In-Time) compilation, meaning the code is compiled and executed at the same time.

- **Node (NodeJS)**: A runtime environment that allows you to run JS on the server side. Built on top of the V8 JS engine. There is no exact Python equivalent for Node; the closest equivalence would be the Python runtime environment. Node essentially contains V8 and built-in libraries.

- **npm (Node Package Manager)** is a package manager for Node. The Python equivalent would be pip. npm uses `package.json`, which is similar to `requirements.txt`.

- **nvm (Node Version Manager)** is a version manager for NodeJS, where the user can install multiple versions of npm on their computer. My computer runs npm through nvm.