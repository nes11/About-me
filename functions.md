## **FUNCTIONS**
---
In JavaScript, functions are objects.

### **Function expression vs function declaration**

In JavaScript, a function is a block of code designed to perform a specific task. 
A function needs to be defined/declared before it is called/invoked.

There are two ways to define a function with the function keyword:

Function declaration:  
```javascript
	function myFuncName(arguments optional) { 
  	statement/what you want your function to do;
	}
```

Function expression:
```javascript  
function myFuncName * (arguments optional) { 
  statement:what you want your function to do 
} // * name optional
// if you omit myFuncName, the function is deemed 'anonymous'
```

As you can see, both syntaxes are pretty similar. Now, there are important differences between these two ways of defining functions, which I don’t quite understand yet. One thing I know is that function declarations are hoisted, which means they can appear in your code after they’ve been invoked. This is more forgiving than function expressions, but it can lead to sloppiness. Function expressions demand that your code be neatly structured, with functions written in the specific order in which they’ll be called/invoked. 

ES6 introduced a new, shorter (and more elegant imo) way of defining function expressions: the arrow function. I usually store my functions in a variable so that they can be used easily later on.

```javascript  
	const myFunc = (arguments optional) => {  
	statement/what you want your function to do 
}
```	

### **Invoking a function**

We’ve talked about defining a function, but unless we invoke it, or call it, this function is just sitting there. 
To invoke a function, and execute the code inside it, we use the name of the function (or the identifier of the variable in which we stored it) followed by parenthesis.

```javascript
	myFuncName();
	myFunc();
```
	
Let’s say we define a function and store it in the variable ‘print’.  
```javascript
	const print = () => { 
	console.log(‘Life is good’);
	} 
	// function is defined here, but nothing is happening yet.
```
We can then invoke it like such:  
```javascript
	print(); 
	// this will print ‘Life is good’ to the console. 
	// print > the function itself
	// print() > the result of invoking the function
```  

### **Parameters vs arguments**

In the example above, we state what we want to be printed inside the body of the function (between the `{ }`). That means our function is only able to print ‘Life is good’. If we wanted to print something else, we’d have to define another function. However, we want to keep our code DRY ( = Don’t Repeat Yourself), so we’re going to define parameters when we define our function. These parameters are placeholders for the values that we will pass the function when we invoke it. 

```javascript
	const print = (text) => { 
		console.log(text);
	} // the parameter ‘text’ is passed in (between the parenthesis), then used in the body of the function. This means that the function will print whatever you pass it when you invoke it. 
```

We can then invoke it like such:
```javascript
	print(‘Life is good’); 
```

We can use the same function with different arguments to produce different results:
```javascript
	print(‘12’); // this will print 12 to the console. 
	print(‘Blah blah blah!’); // this will print ‘Blah blah blah!’ to the console.
```	

Where we defined the `print` function, `(text)` is a parameter. When we invoked the function, we passed in arguments (`‘Life is good’, 12, ‘Blah blah blah!’`), which are the values that will go into the function in lieu of the parameter. We can pass in up to 255 parameters to a function, and they are separated by commas. 
So the parameter is the placeholder in the function definition, whereas the argument is the actual value you pass in the function when you invoke it. 

### **Function return**

Every function in JavaScript returns `undefined` unless specified otherwise. Our print function above prints anything you pass it to the console, but returns `undefined` nonetheless. 
Now usually, we’ll want our function to return something, so that we can load that something into a variable for later use. 
Let’s declare a function with the return keyword:

```javascript
	const multiply = (number) => {
		return number * 2;
	} // this function has a number parameter, which will be multiplied by two. The result will then be returned from the function.
```

When we invoke the function, we can load the return value into a variable, for later use:
```javascript
	const result = multiply(12); // 12 is the argument which will be passed in to our multiply function in lieu of number ( = the parameter). 
```

Without the return keyword, our result variable would be assigned the value `undefined`. 
With the return keyword, something actually comes out of the function, to be loaded into our result variable. Now if we console log result, we will get 24, which is the return value of our function when we invoke it with 12 as an argument. 

Another important thing about the return keyword: it stops execution of the function. Anything that comes after it inside the function body will be ignored. Let’s use our multiply function again to illustrate this:

```javascript
const multiply = (number) => {
	return number * 2;
	console.log(‘Fail!’);
} // the console.log comes after the return statement, so nothing will be printed to the console. 
``` 

### **Self-invoking functions**

We can surround a function expression with parenthesis, followed by () to make it ‘self-invoking’. 

```javascript
	const myfunc = (() => console.log('boo'))();
```

This function is defined and invoked in one fell swoop. 

Other things:  
Arguments are Passed by Value
The parameters, in a function call, are the function's arguments.
JavaScript arguments are passed by value: The function only gets to know the values, not the argument's locations.
If a function changes an argument's value, it does not change the parameter's original value.
Changes to arguments are not visible (reflected) outside the function.
 
Objects are Passed by Reference
In JavaScript, object references are values.
Because of this, objects will behave like they are passed by reference:
If a function changes an object property, it changes the original value.
Changes to object properties are visible (reflected) outside the function.

1) Don't alter a variable or object - create new variables and objects and return them if need be from a function.
2) Declare function arguments - any computation inside a function depends only on the arguments, and not on any global object or variable.

 
