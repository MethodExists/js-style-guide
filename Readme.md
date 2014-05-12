# Javascript Style Guide

This is a guide for writing consistent and aesthetically pleasing node.js code.
It is inspired by what is popular within the community, and flavored with some
personal opinions.

This guide was created by [Felix Geisendörfer](http://felixge.de/) and is
licensed under the [CC BY-SA 3.0](http://creativecommons.org/licenses/by-sa/3.0/)
license. You are encouraged to fork this repository and make adjustments
according to your preferences.

This version is updated by Mark Sergienko for use within MethodExists Inc.

![Creative Commons License](http://i.creativecommons.org/l/by-sa/3.0/88x31.png)

## 2 Spaces for indention

Use 2 spaces for indenting your code and swear an oath to never mix tabs and
spaces - a special kind of hell is awaiting you otherwise.
No Exceptions.

## Newlines

Use UNIX-style newlines (`\n`), and a newline character as the last character
of a file. Windows-style newlines (`\r\n`) are forbidden inside any repository.

## No trailing whitespace

Just like you brush your teeth after every meal, you clean up any trailing
whitespace in your JS files before committing. Otherwise the rotten smell of
careless neglect will eventually drive away contributors and/or co-workers.

## Use Semicolons

According to [scientific research][hnsemicolons], the usage of semicolons is
a core value of our community. Consider the points of [the opposition][], but
be a traditionalist when it comes to abusing error correction mechanisms for
cheap syntactic pleasures.

[the opposition]: http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding
[hnsemicolons]: http://news.ycombinator.com/item?id=1547647

## 80 characters per line

Limit your lines to 80 characters. Yes, screens have gotten much bigger over the
last few years, but your brain has not. Use the additional room for split screen,
your editor supports that, right?

## Use double quotes

Use single quotes, unless you are writing JSON.

*Right:*

```js
var foo = "bar";
```

## Opening braces go on the same line

Your opening braces go on the same line as the statement.

*Right:*

```js
if (true) {
  console.log('winning');
}
```

*Wrong:*

```js
if (true)
{
  console.log('losing');
}
```

Also, notice the use of whitespace before and after the condition statement:

*Wrong:*

```js
}catch(err){

try{

return function(params, session){

if(!_.isFalsey(profile)){

}else{
```

*Right:*
```js
} catch(err) {

try {

return function(params, session) {

if( !_.isFalsey(profile) ) { 

} else {

```


## Variable definition blocks

You can make var statement with multiple var once per closure or module, on top of it.
Here are some examples:

*Right:*

```js

var lib = require("./lib"),
    _ = require("platform2/shared/functional”);
```

Do NOT line up = signs 

Do NOT add extra spaces after var

*Wrong:*

```js
var   _               = require("platform2/shared/functional”),
      saveProfile     = require("./saveProfile");

```

## Use lowerCamelCase for variables, properties and function names

Variables, properties and function names should use `lowerCamelCase`.  They
should also be descriptive. Single character variables and uncommon
abbreviations should generally be avoided.

*Right:*

```js
var adminUser = db.query('SELECT * FROM users ...');
```

*Wrong:*

```js
var admin_user = db.query('SELECT * FROM users ...');
```

## Use UpperCamelCase for class names

Class names should be capitalized using `UpperCamelCase`.

*Right:*

```js
function BankAccount() {
}
```

*Wrong:*

```js
function bank_Account() {
}
```

## Use UPPERCASE for Constants

Constants should be declared as regular variables or static class properties,
using all uppercase letters.

Node.js / V8 actually supports mozilla's [const][const] extension, but
unfortunately that cannot be applied to class members, nor is it part of any
ECMA standard.

*Right:*

```js
var SECOND = 1 * 1000;

function File() {
}
File.FULL_PERMISSIONS = 0777;
```

*Wrong:*

```js
const SECOND = 1 * 1000;

function File() {
}
File.fullPermissions = 0777;
```

[const]: https://developer.mozilla.org/en/JavaScript/Reference/Statements/const

## Object / Array creation

Use trailing commas and put *short* declarations on a single line. Only quote
keys when your interpreter complains:

*Right:*

```js
var a = ['hello', 'world'];
var b = {
  good: 'code',
  'is generally': 'pretty',
};
```

*Wrong:*

```js
var a = [
  'hello', 'world'
];
var b = {"good": 'code'
        , is generally: 'pretty'
        };
```

*Avoid excessive spacing:*

```
return _.keys.all({

  categories: categories

});
```

## Proper use of ternary operator

The ternary operator can be used on a single line if very simple. 
Otherwise, split it up into multiple lines instead.

*Right:*

```js
var foo = (a === b) ? 
  long_expression : 
  another_long_expression;
// or:
var foo = (a === b) ? 1 : 2;
```

## Do not extend built-in prototypes

Do not extend the prototype of native JavaScript objects. Your future self will
be forever grateful.

*Right:*

```js
var a = [];
if (!a.length) {
  console.log('winning');
}
```

*Wrong:*

```js
Array.prototype.empty = function() {
  return !this.length;
}

var a = [];
if (a.empty()) {
  console.log('losing');
}
```

## Use descriptive conditions

Any non-trivial conditions should be assigned to a descriptively named variable or function:

*Right:*

```js
var isValidPassword = password.length >= 4 && /^(?=.*\d).{4,}$/.test(password);

if (isValidPassword) {
  console.log('winning');
}
```

*Wrong:*

```js
if (password.length >= 4 && /^(?=.*\d).{4,}$/.test(password)) {
  console.log('losing');
}
```

## Write small functions

Keep your functions short. A good function fits on a slide that the people in
the last row of a big room can comfortably read. So don't count on them having
perfect vision and limit yourself to ~15 lines of code per function.

## Return early from functions

To avoid deep nesting of if-statements, always return a function's value as early
as possible.

*Right:*

```js
function isPercentage(val) {
  if (val < 0) {
    return false;
  }

  if (val > 100) {
    return false;
  }

  return true;
}
```

*Wrong:*

```js
function isPercentage(val) {
  if (val >= 0) {
    if (val < 100) {
      return true;
    } else {
      return false;
    }
  } else {
    return false;
  }
}
```

Or for this particular example it may also be fine to shorten things even
further:

```js
function isPercentage(val) {
  var isInRange = (val >= 0 && val <= 100);
  return isInRange;
}
```

## Name your closures

Feel free to give your closures a name. It shows that you care about them, and
will produce better stack traces, heap and cpu profiles.

*Right:*

```js
req.on('end', function onEnd() {
  console.log('winning');
});
```

*Wrong:*

```js
req.on('end', function() {
  console.log('losing');
});
```

## No nested closures

Use closures, but don't nest them. Otherwise your code will become a mess.

*Right:*

```js
setTimeout(function() {
  client.connect(afterConnect);
}, 1000);

function afterConnect() {
  console.log('winning');
}
```

*Wrong:*

```js
setTimeout(function() {
  client.connect(function() {
    console.log('losing');
  });
}, 1000);
```

## Commenting


## Chaining
Put dots in the ends of the lines, not at the beginning! 

*Wrong:*

```js
return app.repo
    .select("fc_document")
    .filter({
      review_date: { ne: "" },
      owner: session.profile._id
    })
    .run();
```

*Right:*

```js
return app.repo.
    select("fc_document").
    filter({
      review_date: { ne: "" },
      owner: session.profile._id
    }).
    run();
```

### Splitting long chained lines
Splitting is allowed. Try to balance the lines, so that the beginning makes sense 

*Wrong:*
```js
// app is left meaningless:

directories: app.
      apiServer.callDataView("filingCabinetDirectoryDataView", params, session), 
```

*Right:*
```js
directories: app.apiServer.
      callDataView("filingCabinetDirectoryDataView", params, session),
```

After the first next line and tab all the consequent chaining must be done on new line:

*Wrong:*
```js
app.repo.
    select("fc_document”).filter({ }).
    run();
``` 

*Right:*
```js
app.repo.
    select("fc_document").
    filter({ }).
    run();
```
