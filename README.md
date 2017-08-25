# ️Custom Elements Everywhere 🍻

## What is this?

Karma tests for each of the major frameworks to see how they handle working
with Custom Elements.

## Installation

To install all dependencies and build the site:

```bash
npm run install-all

# You'll see errors during this next step because some of the framework tests
# fail. That's by design, so don't worry! At the end it should print the
# message "Site built successfully!". If you don't see that then something
# actually did break :P

npm run build

npm start
```

## How do I add a library/framework to the project?

Tests for each library/framework live in the `libraries/` directory. The easiest
way to start is by copying the test directory from a project that is similar to
your own. For example, if the library you use is similar to React/Preact, you
might start by copying and renaming the `libraries/preact` directory.

Your library structure should look like this:

```
├── karma.conf.js
├── meta
│   ├── issues.json
│   └── summary.md
├── package-lock.json
├── package.json
├── src
│   ├── component-tests.js
│   └── components.js
└── tests.webpack.js
```

### karma.conf.js

Your [Karma](https://karma-runner.github.io/1.0/index.html) configuration.
Ideally you shouldn't need to change much in here. The config file uses
[karma-webpack](https://github.com/webpack-contrib/karma-webpack), so there is
a `webpack` property where you can essentially write your `webpack.config.js`.
You'll need to change this property to tell it how to bundle your library.

### meta/

This directory contains `issues.json` where you list any open GitHub issues
related to custom element support in your library. There is also a `summary.md`
where you write a short description of how the library interacts with custom
elements and any known quirks or gotchas.

### src/

This directory contains `components.js` where you create library/framework
components which try to communicate with custom elements. You then test these
components in `component-tests.js`. You'll want to use all of the assertions
in `component-tests.js` but update the actual test implementations to use your
library's testing tools and components.

Note that all frameworks use the custom elements in the
`/libraries/__shared__/webcomponents/` directory for tests.

### tests.webpack.js

This file is consumed by the test runner and tells it to import any files ending
in `-test`. You probably won't need to change this file.

## What kind of behavior do the tests assume?

- The library/framework should be able to display elements that use shadow DOM,
  insert children in them, and handle hiding and showing them.
- The library/framework should be able to pass **primitive** data (strings,
  numbers, booleans) to a custom element as either attributes or properties.
- The library/framework should be able to pass **rich** data (objects, arrays)
  to a custom element using properties.
- The library/framework should be able to listen to DOM events from a custom
  element. These DOM events could use any casing style.

## License

Copyright 2017 Google, Inc.

Licensed under the [Apache License, Version 2.0](LICENSE) (the "License");
you may not use this file except in compliance with the License. You may
obtain a copy of the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
