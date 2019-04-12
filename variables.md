## **VARIABLES**

JavaScript variables are containers for storing data values. 

### **Variable declaration**

Creating a variable in JavaScript is called “declaring” a variable. 
The keywords `var`, `let`, or `const` can be used to declare a variable.

```javascript
var car;
let shoppingList;
const person;
```  
At this point the variable is declared. However, since it has not yet been assigned a value, its value is undefined.

You can give your variables any name you fancy but it should be unique, start with a letter, and use camelCase. CamelCase is a coding convention for writing identifier names, such as variables and functions. Instead of separating words with a space or hyphen, camelCase capitalises the first letter of each word, except for the first one.

```javascript
First name > const firstName
List booked venues > let listOfBookedVenues
```

Please note that JS identifier names are case-sensitive.  
“listOfBookedVenues” and “listOfBookedvenues” are different variable names.

### **Assigning value to a variable**

The basic assignment operator is the equal sign (=).  
JS evaluates what is on the right side of the equal sign, and assigns the value to the variable on the left side.

```javascript
car = “Mercedes”;
person = “adult”;
```  
No need for var/let/const keywords here, as we have previously declared these variables.
```javascript
let finalResult = totalScore / 12;
```  
Here it is assumed that totalScore as been previously declared and assigned a value. Say totalScore was assigned a value of 36: the right-hand side of the equal sign will evaluate as 36 / 12, hence 3. The value of 3 is then assigned to the variable on the left-hand side of the equal sign. 

### **JavaScript value types**

#### Primitive values
-	undefined
-	null
-	Boolean: true or false
-	Number
-	String: a series of characters (letters, symbols and/or numbers) surrounded by double (“ “) or single (‘ ‘) quotes. 
```javascript 
“You win the game”, ‘hamburger’
```  
Backticks can also be used, especially with string interpolation: 
```javascript 
    `Hello ${userName}` 
``` 

#### Objects
-	Array: collection of values surrounded by square braces [ ] and separated by commas.  
```javascript
[‘Julie’, 27, false, “The Hitchhiker’s guide to the Galaxy”]  
```
-	Function: more on this later
-	Object: collection of key:value pairs surrounded by curly braces and separated by commas.  
```javascript
{  
  name: ‘Julie’,  
  age: 27,  
  married: false,  
  favouriteBook: “The Hitchhiker’s guide to the Galaxy”
}
```

The most important difference is that 
Primitive values are manipulated by value and 
Objects, by reference. 
What this really means is that primitive values will not be shared between multiple variables – even after setting variables equal to each other. Every variable representing a primitive value is guaranteed to represent a unique memory location and no two variables will ever point to the same memory location. The other key point is that the value itself is stored in the physical memory location.

```javascript
const a = 12;
const b = 12;
a === b; // false. Both variables hold equal values but there’re not equal because they are different pieces of memory. 
```  

Object variables are different since multiple variables may point to a shared location in memory instead of representing multiple copies of the same data. Unlike primitive values, objects are not immutable, so you have to be careful when changing referenced data since the change will be seen by all references.
 
