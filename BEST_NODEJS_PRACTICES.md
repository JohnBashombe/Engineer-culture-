# NodeJs Best Practices and Conventions

This is not about JS style, as style guide we use Prettier and lint with Eslint.

## Overview

### Modules

    no side effects
        exceptions: singleton-like modules, memoizing / cache
    Prefer one class / function per module
    path in 'require' includes extension
    if you need to expose async data, export function that accepts callback as a parameter (or use promises)
    Naming:
        lower snake case (some filesystems are non case sensitive!)
        same name as class / function inside (but snake case)

### Async

    prefer plain old callbacks in function / method parameters
    always call with (err, data) parameters
    callback is called exactly once
    if you need to report more than once, convert your function/class to EventEmitter or Stream
    EventEmitter: expect more then (and less then) one listener.
    All handlers are called synchronously one after another.
    Promises / Thunks are OK but if you can express your flow with promises 
    but cannot with callbacks you might want to refactor architecture

### Packages 

    use standard top level structure: lib/, bin/, test/, test/integration/, examples/, src/, index.js, 
    package.json, README.md, LICENSE, Changelog.md
    use expressive non-creative name when possible
    use proper non-creative keywords in package.json (always)
    package.json scripts:
        npm start
        npm run debug
        npm npm run integration
        etc.
    Changelog: answers different question than git log. Git: "why do we have this change?". 
    Changelog: "Why should I upgrade this package?"

### Performance 

    lazy everything
    zero penalty if not used
    never optimise first, but always know algorithmic complexity
    if in doubt, request for later upgrade in the Changelog file
    make sure you code work as expected if callback function throws an exception.

## Error Handling

Errors can be divided into two main parts: operational errors and programmer errors.

### Operational errors

    Operational errors can happen in well-written applications as well, because they are not bugs, 
    but problems with the system / a remote service, like:

        request timeout
        system is out of memory
        failed to connect to a remote service

    Handling operational errors

    Depending on the type of the operational error, you can do the followings:

        Try to solve the error - if a file is missing, you may need to create one first
        Retry the operation, when dealing with network communication
        Tell the client, that something is not ok - can be used, when handling user inputs
        Crash the process, when the error condition is unlikely to change on its own, 
        like the application cannot read its configuration file

    Also, it is true for all the above: log everything.

#### Programmer errors

    Programmer errors are bugs. This is the thing you can avoid, like:

        called an async function without a callback
        cannot read property of undefined

    Handling programmer errors

    Crash immediately - as these errors are bugs, you won't know in which state your application is.
    A process control system should restart the application when it happens, like: supervisord or monit.

## Do not reinvent / unless if requested or needed.

    Always look for existing solutions first. NPM has a crazy amount of packages, 
    there is a pretty good chance you will find the functionality that you are looking for.

## Dive Into Implementation

### Callback Convention

Modules should expose an error-first callback interface.

It should be like this:

```
const sample =  (user, callback) => {
  let creation = createUser(user);
  return callback(null, creation);

```

Always check for errors in callbacks and report them trough helpers

### Async

Use try-catch in sync code only and where else you judge an excption can be thrown 

```
    try {

    } catch(exception) {
        callback(exception);
    }

```

Try to avoid this and new
Use good async patterns

```
 use async / await

 ```

### Consistent Style, lint and Config

#### Style and Lint

We enforce style rules and hints using Prettier and EsLint, this enable pre-commit, pre-push on the developer's computer 
```
  "husky": {
    "hooks": {
        "pre-commit": "lint-staged && npm run lint",
        "pre-push": "git diff HEAD --quiet && npm test"
    }
  },
```

#### Config 

##### NodeJs over JSON for configuration

package.json remain the only config file for batch and rules over the project and others spec config file
for different integration like .rc, yml, etc.
but we mainly use the config.js or config folder/* for the project management development as it gives more flexibility 

Sample 

```
config.server = {
    host: '0.0.0.0',
    port: process.env.PORT || 3000
};

config.db = {
    use_env_variable: 'DATABASE_URL_DEV',
    username: process.env.DB_USER_DEV,
    password: process.env.DB_PASSWORD_DEV,
    database: process.env.DB_NAME_DEV,
    host: process.env.DB_HOST_DEV,
    dialect: '...',
    seederStorage: '...',
}
```

##### Path 

We use NODE_PATH 

Somthing like following is not supported ( realtive path) :

```
import myModule from '../../../../myModule';
```

Here how we set up node_path in package.json file 

```
 "scripts": {
    "start": "NODE_PATH=src node app.js"
  },
```

Now the right implementation become an Abosulte path  

```
import myModule from 'src/model/myModule';
```
