# JavaScript / Node.js Style Guide

This is a guide for writing consistent and aesthetically pleasing node.js code.
It is inspired by what is popular within the community, and flavored with some
personal opinions.

There is a .jshintrc which enforces these rules as closely as possible. You can
either use that and adjust it, or use
[this script](https://gist.github.com/kentcdodds/11293570) to make your own.

This guide was originally created by [Felix Geisendörfer](http://felixge.de/) and is
licensed under the [CC BY-SA 3.0](http://creativecommons.org/licenses/by-sa/3.0/)
license.

This version is updated by Bobby Rockers for use within Automation Integrated, LLC.

![Creative Commons License](http://i.creativecommons.org/l/by-sa/3.0/88x31.png)

## Table of contents

* [Tabs leading Spaces otherwise](#tabs-leading-spaces-otherwise)
* [Newlines](#newlines)
* [No trailing whitespace](#no-trailing-whitespace)
* [Use Semicolons](#use-semicolons)
* [80 characters per line](#80-characters-per-line)
* [Use single quotes](#use-single-quotes)
* [Opening braces go on the same line](#opening-braces-go-on-the-same-line)
* [Method chaining](#method-chaining)
* [Declare one variable per var statement](#declare-one-variable-per-var-statement)
* [Use lowerCamelCase for variables, properties and function names](#use-lowercamelcase-for-variables-properties-and-function-names)
* [Use lowerCamelCase for class names](#use-lowercamelcase-for-class-names)
* [Name files alllowercase. Use of dashes and dots](#name-files-alllowercase-use-of-dashes-and-dots)
* [Use UPPERCASE for Constants](#use-uppercase-for-constants)
* [Object / Array creation](#object--array-creation)
* [Use the === operator](#use-the--operator)
* [Use multi-line ternary operator](#use-multi-line-ternary-operator)
* [Use slashes for comments](#use-slashes-for-comments)
* [Object.freeze, Object.preventExtensions, Object.seal, with, eval](#objectfreeze-objectpreventextensions-objectseal-with-eval)
* [Getters and setters](#getters-and-setters)

## Tabs leading spaces otherwise

Only sociopaths with an intrinsic need to control other peoples text layout
require leading spaces.  All __leading__ spaces should be tabs.  I don't care
about your tabstop length because tabs are only allowed at the beginnings of 
lines, you know, kinda like __what the Tab key was invented for!!__ 

__All__ other space formatting should be done with... spaces!! Finally, swear an oath 
to never mix tabs and spaces - a special kind of hell is awaiting you otherwise.

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

## Use single quotes

Use single quotes is preferred for variable declaration.  Do not use single quotes 
when you are writing JSON.

For sentences or messages use double quotes as well.

*Right:*

```js
var foo = 'bar';
console.log("Something is happening here");
```

*Wrong:*

```js
var foo = "bar";
```

## Opening braces go on the same line

Your opening braces go on the same line as the statement. Because K&R!

*Right:*

```js
if (true){
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

Also, notice the lack of whitespace after the condition statement.

## Method chaining

One method per line should be used if you chain more than 2 methods.

You should also indent these methods so it's easier to tell they are part of the same chain.

*Right:*

```js
User
	.findOne({ name: 'foo' })
	.populate('bar')
	.exec(function(err, user) {
		return true;
	});
```

*Wrong:*

```js
User
.findOne({ name: 'foo' })
.populate('bar')
.exec(function(err, user) {
	return true;
});

User.findOne({ name: 'foo' })
	.populate('bar')
	.exec(function(err, user) {
		return true;
	});

User.findOne({ name: 'foo' }).populate('bar')
.exec(function(err, user) {
	return true;
});

User.findOne({ name: 'foo' }).populate('bar')
	.exec(function(err, user) {
		return true;
	});
```

## Declare one variable per var statement

Declare one variable per var statement, it makes it easier to re-order the
lines. However, ignore [Crockford][crockfordconvention] when it comes to
declaring variables deeper inside a function, just put the declarations wherever
they make sense.

Do *not* add extra spaces after var or try to line up the = signs.

*Right:*

```js
var keys   = ['foo', 'bar'];
var values = [23, 42];

var object = {};
while (keys.length) {
	var key = keys.pop();
	object[key] = values.pop();
}
```

*Wrong:*

```js
var keys = ['foo', 'bar'],
		values = [23, 42],
		object = {},
		key;

var test         = 'this';
var lotsOfThings = 'here';

while (keys.length) {
	key = keys.pop();
	object[key] = values.pop();
}
```

[crockfordconvention]: http://javascript.crockford.com/code.html

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

## Use lowerCamelCase for class names

Class names should be capitalized using `lowerCamelCase`.

*Right:*

```js
function bankAccount() {
}
```

*Wrong:*

```js
function bank_Account() {
}

function BankAccount() {
}
```
## Name files alllowercase. Use of dashes and dots

File names should be all lowercase using dashes to separate words and dots to separate
logical parts.

*Right:*

```js
my-new-module-1.0.js
```

*Wrong:*

```js
myNewModule-1.0.js
my_new_module.1-0.js
my new module.10.js
My-new-module.1.0.js
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

## Use the === operator

Programming is not about remembering [stupid rules][comparisonoperators]. Use
the triple equality operator as it will work just as expected.

*Right:*

```js
var a = 0;
if (a !== '') {
	console.log('winning');
}

```

*Wrong:*

```js
var a = 0;
if (a == '') {
	console.log('losing');
}
```

[comparisonoperators]: https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators

## Use multi-line ternary operator

The ternary operator can be used on a single line if very simple. Otherwise, split it 
up into multiple lines instead.

*Right:*

```js
var foo = (a === b) ? 1 : 2;
```

*Wrong:*

```js
var foo = (a === b)
	? 1
	: 2;
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

## Use slashes for comments

Use slashes for both single line and multi line comments. Try to write
comments that explain higher level mechanisms or clarify difficult
segments of your code. Don't use comments to restate trivial things.

*Right:*

```js
// 'ID_SOMETHING=VALUE' -> ['ID_SOMETHING=VALUE', 'SOMETHING', 'VALUE']
var matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// This function has a nasty side effect where a failure to increment a
// redis counter used for statistics will cause an exception. This needs
// to be fixed in a later iteration.
function loadUser(id, cb) {
	// ...
}

var isSessionValid = (session.expires < Date.now());
if (isSessionValid) {
	// ...
}
```

*Wrong:*

```js
// Execute a regex
var matches = item.match(/ID_([^\n]+)=([^\n]+)/);

// Usage: loadUser(5, function() { ... })
function loadUser(id, cb) {
	// ...
}

// Check if the session is valid
var isSessionValid = (session.expires < Date.now());
// If the session is valid
if (isSessionValid) {
	// ...
}
```

## Object.freeze, Object.preventExtensions, Object.seal, with, eval

Crazy shit that you will probably never need. Stay away from it.

## Getters and setters

Do not use setters, they cause more problems for people who try to use your
software than they can solve.

Feel free to use getters that are free from [side effects][sideeffect], like
providing a length property for a collection class.

[sideeffect]: http://en.wikipedia.org/wiki/Side_effect_(computer_science)
