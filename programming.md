# Programming Paradigm

## Full-Stack Javascript

## Javascript is a Prototype-based language

## Functional programming

## Self-explanatory code

## No code replication

## Modular structure (node.js)
  Modules are reusable
  Modules are stand-alone units
  Modules define their requirements (require) and output (module.exports)

## Embrace community modules

## Modules we embrace
Please take a moment to review package.json to get an idea of all modules we use.

### Helpful libraries
underscorejs (underscorejs.org) - we should embrace underscore, as it's well-writen and very popular functional programming library.
moment.js - This is best we could find so far for date-time manipulation in JavaScript.
when.js - This is one of, but our library of choice for dealing with Promises.
check-types - This is one of type validation libraries that we choose to embrace in our code.

### Structure of the app
broadway - A great and simple way to divide application in modules (see server codee)
eventemitter2 - Node's standard event bus.
nconf - From creators of broadway, configuration reader.

### Infrastructure modules
express - Best and most widely used HTTP server for node.js.
mongodb - Our current Database of choice, we are using mongo-native-driver for node.
redis - Database that can be utilized for certain tasks (session storage, cache, etc)
socket.io - WebSockets library.

### Unit testing modules
mocha - test framework
http://visionmedia.github.io/mocha/

chai - BDD Assertion library
http://chaijs.com/api/bdd/
     http://chaijs.com/plugins/chai-things
     http://chaijs.com/plugins/chai-as-promised
     
superagent - Reverse of express, by visionmedia.


## Asynchronous programming

### Node is non-blocking

### Promises
Embrace promises over call-backs whenever possible

## Error handling
Must read: https://www.joyent.com/developers/node/design/errors


## Must-read documentation 
Keep it close for reference.

http://docs.mongodb.org/manual/
http://underscorejs.org/
http://momentjs.com/docs/
https://github.com/cujojs/when/blob/master/docs/api.md
https://github.com/philbooth/check-types.js
http://visionmedia.github.io/mocha/
http://nodejs.org/api/
http://docs.ractivejs.org/latest/get-started
http://blog.nodejitsu.com/introducing-flatiron/

## Useful Sites
http://nodeschool.io/

## Blogs to follow
http://bahmutov.calepin.co/
