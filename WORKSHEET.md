# JavaScript Hoisting Worksheet

## Instructions
1. Review each code snippet below.
2. Fill in what will be output to the console.
3. Run the code to see if you were correct.
4. Describe why the code behaved as it did.
5. Re-write the code snippet to maintain the same output, but to avoid hoisting.

```js
var myvar = 'my value'; 
  
(function() { 
	console.log(myvar);
	var myvar = 'local value'; 
})();
```

> output:
>-undefined
>-
>-
> why?
>-because 'local value' would not get set until after the console log
>-moves the declaration but not the definition
>-
>-
>-
>-
> rewrite without hoisting
>-var myvar = 'my value'
>-(function() { 
	var myvar;
	console.log(myvar);
	myvar = 'local value'; 
})();
>-
>-
>-
>-
>-
>-
>-
>-
>-
>-

```js
var flag = true; 
  
function test() {

	if(flag) {
		var flag = false;
		console.log('Switch flag from true to false');
	}
	else {
		flag = true;
		console.log('Switch flag from false to true');
	}
}
test();
```

> output:
>-console.log('Switch flag from false to true')
>-
>-
> why?
>-the flag variable was not locally defined before the if statement was run.
>-
>-
>-
>-
>-
> rewrite without hoisting
>-
>-
var flag = true; 
  
function test() {
	var flag;
	if(flag) {
		flag = false;
		console.log('Switch flag from true to false');
	}
	else {
		flag = true;
		console.log('Switch flag from false to true');
	}
}
test();
>-
>-
>-
>-
>-
>-
>-
>-
>-
>-


```js
var message = 'Hello world'; 
  
function saySomething() {
	console.log(message);
	var message = 'Foo bar';
}
saySomething();
```

> output:
>-
>-undefined
>-
> why?
>-
>-the var message was declared but not defined when console got logged
>-
>-
>-
>-
> rewrite without hoisting
>-
>-
var message = 'Hello world'; 
	var message;
function saySomething() {
	console.log(message);
	message = 'Foo bar';
}
saySomething();
>-
>-
>-
>-
>-
>-
>-
>-
>-
>-

```js
var message = 'Hello world'; 
  
function saySomething() {
	console.log(message);
	message = 'Foo bar';
}
saySomething();
```

> output:
>-'hello world'
>-
>-
> why?
>-
>-no new variables were declared in the function
>-
>-
>-
>-


```js
function test() {
	console.log(a);
	console.log(foo());

	var a = 1;
	function foo() {
		return 2;
	}
}
 
test();
```

> output:
>-undefined, 2
>-
>-
> why?
>-
>-the whole function is available, but only the declaration of var a is available for the console logs
>-
>-
>-
>-
> rewrite without hoisting
>-
>-
function test() {
	function foo() {
		return 2;
	}
	var a;
	console.log(a);
	console.log(foo());

	a = 1;
	
}
 
test();
>-
>-
>-
>-
>-
>-
>-
>-
>-
>-

```js
(function() {
	console.log(bar);
	foo();

	function foo() {
		console.log('aloha');
	}

	var bar = 1;
	baz = 2;
})();
```

> output:
>-undefined, 'aloha'
>-
>-
> why?
>-
>-bar is declared but undefined by the time it gets console logged
>-the function is available at the beginning
>-
>-
>-
> rewrite without hoisting
>-
>-
(function() {
	function foo() {
		console.log('aloha');
	}
	var bar;
	console.log(bar);
	foo();

	bar = 1;
	baz = 2;
})();
>-
>-
>-
>-
>-
>-
>-
>-
>-
>-

```js
var run = false;

function fancy(arg1, arg2) {
	if(run) {
		console.log('I can run');
	}
	else {
		console.log('I can\'t run');
	}

	function run() {
		console.log('Will I run?');
	}
}
fancy();
```

> output:
>-'i can run'
>-
>-
> why?
>-
>-the function run hoisted to top, the if statement knew run was truthy valaue
>-
>-
>-
>-
> rewrite without hoisting
>-
>-
var run = false;

function fancy(arg1, arg2) {
	function run() {
		console.log('Will I run?');
	}
	if(run) {
		console.log('I can run');
	}
	else {
		console.log('I can\'t run');
	}

	
}
fancy();
>-
>-
>-
>-
>-
>-
>-
>-
>-
>-

```js
var run = false;

function fancy(arg1, arg2) {
	if(run) {
		console.log('I can run');
	}
	else {
		console.log('I can\'t run');
	}

	var run = function() {
		console.log('Will I run?');
	}
}
fancy();
```

> output:
>-'i cant run'
>-
>-
> why?
>-the variable run was hoisted but not defined yet. So the fancy function saw it a undefined
>-
>-
>-
>-
>-
> rewrite without hoisting
>-
>-
var run = false;

function fancy(arg1, arg2) {
	var run;
	if(run) {
		console.log('I can run');
	}
	else {
		console.log('I can\'t run');
	}

	run = function() {
		console.log('Will I run?');
	}
}
fancy();
>-
>-
>-
>-
>-
>-
>-
>-
>-
>-