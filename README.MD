# Object Manipulation
1. Creating Objects
Example:
```javascript
// Using object literal syntax
const person = {
  name: 'John',
  age: 30,
  city: 'New York'
};
```
Explanation:
Object Literal Syntax: The most common way to create objects using curly braces {}.
Object Constructor: Another way to create objects using the new Object() syntax.

2. Accessing and Updating Properties
Example:
```javascript
const person = {
  name: 'John',
  age: 30,
  city: 'New York'
};

// Accessing properties
console.log(person.name); // Output: John
console.log(person['age']); // Output: 30

// Updating properties
person.age = 31;
person['city'] = 'San Francisco';

console.log(person); // Output: { name: 'John', age: 31, city: 'San Francisco' }
```
Explanation:

Dot Notation: Access and update properties using the dot notation (object.property).
Bracket Notation: Access and update properties using the bracket notation (object['property']).

3. Adding and Deleting Properties
Example:
```javascript
const person = {
  name: 'John',
  age: 30
};

// Adding properties
person.city = 'New York';
person['country'] = 'USA';

console.log(person); // Output: { name: 'John', age: 30, city: 'New York', country: 'USA' }

// Deleting properties
delete person.age;

console.log(person); // Output: { name: 'John', city: 'New York', country: 'USA' }
```
Explanation:

Adding Properties: Simply assign a value to a new property.
Deleting Properties: Use the delete operator to remove a property from an object.

4. Iterating Over Properties

Example:
```java
const person = {
  name: 'John',
  age: 30,
  city: 'New York'
};

// Using for...in loop
for (let key in person) {
  if (person.hasOwnProperty(key)) {
    console.log(`${key}: ${person[key]}`);
  }
}

// Using Object.keys() and forEach()
Object.keys(person).forEach(key => {
  console.log(`${key}: ${person[key]}`);
});

// Using Object.entries() and for...of loop
for (let [key, value] of Object.entries(person)) {
  console.log(`${key}: ${value}`);
}
```
Explanation:

for...in Loop: Iterates over all enumerable properties of an object.
Object.keys(): Returns an array of the object's own property names.
Object.entries(): Returns an array of the object's own enumerable property [key, value] pairs.

5. Merging Objects
Example:
```javascript
const person = {
  name: 'John',
  age: 30
};

const address = {
  city: 'New York',
  country: 'USA'
};

// Using Object.assign()
const merged1 = Object.assign({}, person, address);

// Using spread operator
const merged2 = { ...person, ...address };

console.log(merged1); // Output: { name: 'John', age: 30, city: 'New York', country: 'USA' }
console.log(merged2); // Output: { name: 'John', age: 30, city: 'New York', country: 'USA' }
```
Explanation:

Object.assign(): Copies all enumerable own properties from one or more source objects to a target object.
Spread Operator: A more concise way to merge objects using the spread operator (...).

6. Cloning Objects
Example:
```javascript
const person = {
  name: 'John',
  age: 30,
  address: {
    city: 'New York',
    country: 'USA'
  }
};

// Shallow clone using Object.assign()
const clone1 = Object.assign({}, person);

// Shallow clone using spread operator
const clone2 = { ...person };

// Deep clone using JSON methods
const clone3 = JSON.parse(JSON.stringify(person));

console.log(clone1); // Output: { name: 'John', age: 30, address: { city: 'New York', country: 'USA' } }
console.log(clone2); // Output: { name: 'John', age: 30, address: { city: 'New York', country: 'USA' } }
console.log(clone3); // Output: { name: 'John', age: 30, address: { city: 'New York', country: 'USA' } }
```
Explanation:

Shallow Clone: Copies the object's properties, but nested objects are shared between the original and the clone.
Object.assign(): Creates a shallow clone.
Spread Operator: Creates a shallow clone.
Deep Clone: Creates a complete copy of the object, including nested objects.
JSON Methods: Convert the object to a JSON string and then parse it back to an object.
