## **REST and SPREAD OPERATORS**
---
`...` is a new functionality provided by Javascript's ECMA6. It can be used as  rest parameters or a spread operator.

### **Rest parameters**

Collects all the remaining arguments into an array. It allows us to represent an indefinite number of arguments as an array.

Without rest parameters:
```javascript
const myFunc = (a, b) => console.log(a, b);
myFunc(1, 2, 3, 4, 5) // will console.log 1, 2. Even though the function call accepts any number of arguments, the function declaration only accounts for two, so the function is run with the first two arguments only. 
```
With rest parameters:
```javascript
const myFunc = (…args) => console.log(args);
myFunc(1, 2, 3, 4, 5) // will console.log [1, 2, 3, 4, 5]. All the arguments passed to myFunc are gathered into an array. Since the rest parameters gives us an array, we can then use any array method on it. 
```
We can also define some arguments in the function declaration; the remaining arguments in the function call will be gathered in an array.

```javascript
const myFunc2 = (arg1, arg2, …array) => {
console.log(array)
return arg1 + arg2;
}
myFunc2(2, 4, 5, 6, 7) // console.log 5, 6 ,7 and returns 6
```
In the function declaration, the rest parameters has to be the last argument. Since it gathers all remaining arguments, adding another one after it will throw an error.

```javascript
const myFunc2 = (arg1, …array, arg2) => {
consol	e.log(array)
return arg1 + arg2;
}
myFunc2(2, 4, 5, 6, 7) // ERROR arg1 gets the value of the first argument and array gets all remaining ones, so there is no value left for arg2.
```  

### **Spread operator**

Unpacks elements of an array/properties of an object into separate arguments. Say we have a function that takes a list of integers (such as `Math.max()`), and an array of integers that we want to use as arguments. 
```javascript
const integersArray = [2, 56, 678, 224, 3]
Math.max(…integersArray) // the spread operator ‘unpacks’ the array, allowing each element of the array to be passed as a separate argument. 
```
The spread operator can be very useful in different scenarios:

- We want to add an element to an array:
```javascript
const arrayOfColours = [‘red’, ‘green’, ‘yellow’]
const newArrayOfColours  = [‘blue’, …arrayOfColours, ‘purple’]
newArrayOfColours  === [‘blue’, ‘red’, ‘green’, ‘yellow’, ‘purple’]
```
- We want to copy an object:
```javascript
const obj1 = { name: ‘Julie’, age: 27, height: 167}
const obj2 = {…obj1} // now obj2 === { name: ‘Julie’, age: 27, height: 167}
```
- We want to split a string into separate characters:
```javascript
const str = “hello”;
const spreadStr = …str; // spreadStr  === [‘h’, ‘e’, ‘l’, ‘l’, ‘o’]
```
- We want to add a property to an object:
```javascript
const obj1 = {
	name: ‘julie’,
	age: 27,
	height: 167
}
const updatedObj1 = {
	… obj1,
	allergies: ‘none’
} // updatedObj1 has all the properties of obj1, plus the allergies property. 
```
