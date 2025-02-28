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
```javascript
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

***Flattening of an object***
Flattening a nested object means converting it into a single-level object where the keys represent the path to the original nested values. Here's a function to flatten a nested object in JavaScript:

Example Implementation
```javascript
function flattenObject(obj, parentKey = '', result = {}) {
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      const newKey = parentKey ? `${parentKey}.${key}` : key;
      if (typeof obj[key] === 'object' && obj[key] !== null && !Array.isArray(obj[key])) {
        flattenObject(obj[key], newKey, result);
      } else {
        result[newKey] = obj[key];
      }
    }
  }
  return result;
}

// Example usage
const nestedObject = {
  name: 'John',
  address: {
    city: 'New York',
    zip: {
      code: 10001,
      plus4: 1234
    }
  },
  contact: {
    phone: '123-456-7890',
    email: 'john@example.com'
  }
};

const flattenedObject = flattenObject(nestedObject);
console.log(flattenedObject);
/*
Output:
{
  'name': 'John',
  'address.city': 'New York',
  'address.zip.code': 10001,
  'address.zip.plus4': 1234,
  'contact.phone': '123-456-7890',
  'contact.email': 'john@example.com'
}
*/
```

Explanation
1. Function Definition:
   The flattenObject function takes three parameters:
   obj: The object to be flattened.
   parentKey: The key of the parent object, used to build the path for nested keys.
   result: The resulting flattened object.
2. Iterate Over Object Keys:
   The function iterates over the keys of the object using a for...in loop.
   It checks if the key is a direct property of the object using hasOwnProperty.
3. Build New Key:
   The new key is built by concatenating the parentKey and the current key with a dot (.) separator.
   Recursive Call for Nested Objects:
   If the value of the current key is an object (and not an array), the function calls itself recursively to flatten the nested object.
4. Assign Value to Result:
   If the value is not an object, it assigns the value to the result object using the new key.
5. Return Result:
   The function returns the flattened object.



# From a String word count the occurences of characters and return in an object

To count the occurrences of each character in a string and return the result as an object, you can create a function that iterates over the string and keeps track of the count of each character. Here's how you can do it:

Example Implementation
```javascript
function countCharacterOccurrences(str) {
  const result = {};

  for (let char of str) {
    if (result[char]) {
      result[char]++;
    } else {
      result[char] = 1;
    }
  }

   // Sort the result object by keys
  const sortedResult = {};
  Object.keys(result).sort().forEach(key => {
    sortedResult[key] = result[key];
  });

  return result;
}

// Example usage
const inputString = "hello world";
const characterCounts = countCharacterOccurrences(inputString);
console.log(characterCounts);
/*
Output:
{
  h: 1,
  e: 1,
  l: 3,
  o: 2,
  ' ': 1,
  w: 1,
  r: 1,
  d: 1
}
*/
```
Explanation
Function Definition:

The countCharacterOccurrences function takes a single parameter str, which is the input string.
Initialize Result Object:

An empty object result is initialized to store the character counts.
Iterate Over String:

The function uses a for...of loop to iterate over each character in the string.
Update Character Count:

For each character, the function checks if the character is already a key in the result object.
If the character is already a key, its value (count) is incremented by 1.
If the character is not a key, it is added to the result object with a value (count) of 1.
Return Result:

The function returns the result object containing the character counts.
Using BubbleSort: Sort the object 
```javascript
function countCharacterOccurrences(str) {
  const result = {};

  for (let char of str) {
    if (result[char]) {
      result[char]++;
    } else {
      result[char] = 1;
    }
  }

  // Get the keys of the result object
  const keys = Object.keys(result);

  // Bubble sort algorithm to sort the keys
  for (let i = 0; i < keys.length; i++) {
    for (let j = 0; j < keys.length - i - 1; j++) {
      if (keys[j] > keys[j + 1]) {
        // Swap keys[j] and keys[j + 1]
        const temp = keys[j];
        keys[j] = keys[j + 1];
        keys[j + 1] = temp;
      }
    }
  }

  // Create a new sorted result object
  const sortedResult = {};
  for (let key of keys) {
    sortedResult[key] = result[key];
  }

  return sortedResult;
}

// Example usage
const inputString = "hello world";
const characterCounts = countCharacterOccurrences(inputString);
console.log(characterCounts);
/*
Output:
{
  ' ': 1,
  d: 1,
  e: 1,
  h: 1,
  l: 3,
  o: 2,
  r: 1,
  w: 1
}
*/
```
Using REDUCE METHOD:

```javascript
function countCharacterOccurrences(str) {
  const result = {};

  for (let char of str) {
    if (result[char]) {
      result[char]++;
    } else {
        result[char] = 1;
    }
  }

  // Convert the object to an array of key-value pairs
  const entries = Object.entries(result);

  // Sort the array by keys
  const sortedEntries = entries.sort((a, b) => a[0].localeCompare(b[0]));

  // Use reduce to reconstruct the sorted object
  const sortedResult = sortedEntries.reduce((acc, [key, value]) => {
    acc[key] = value;
    return acc;
  }, {});

  return sortedResult;
}

// Example usage
const inputString = "hello world";
const characterCounts = countCharacterOccurrences(inputString);
console.log(characterCounts);
/*
Output:
{
  ' ': 1,
  d: 1,
  e: 1,
  h: 1,
  l: 3,
  o: 2,
  r: 1,
  w: 1
}
*/
```

# SORTING 
```javascript
***SORT AN ARRAY***
function bubbleSort(arr) {
  let n = arr.length;
  let swapped;

  do {
    swapped = false;
    for (let i = 0; i < n - 1; i++) {
      if (arr[i] > arr[i + 1]) {
        // Swap arr[i] and arr[i + 1]
        let temp = arr[i];
        arr[i] = arr[i + 1];
        arr[i + 1] = temp;
        swapped = true;
      }
    }
    n--; // Reduce the range of comparison
  } while (swapped);

  return arr;
}

// Example usage
const numbers = [5, 3, 8, 1, 2];
const sortedNumbers = bubbleSort(numbers);

console.log(sortedNumbers); // Output: [1, 2, 3, 5, 8]

***SORT AN OBJECT***

```javascript
 // Get the keys of the result object
  const keys = Object.keys(result);

  // Bubble sort algorithm to sort the keys
  for (let i = 0; i < keys.length; i++) {
    for (let j = 0; j < keys.length - i - 1; j++) {
      if (keys[j] > keys[j + 1]) {
        // Swap keys[j] and keys[j + 1]
        const temp = keys[j];
        keys[j] = keys[j + 1];
        keys[j + 1] = temp;
      }
    }
  }

  // Create a new sorted result object
  const sortedResult = {};
  for (let key of keys) {
    sortedResult[key] = result[key];
  }

  return sortedResult;
```
# BubbleSort the array of string
```javascript
function bubbleSortStrings(arr) {
  let n = arr.length;
  let swapped;

  do {
    swapped = false;
    for (let i = 0; i < n - 1; i++) {
      if (arr[i].localeCompare(arr[i + 1]) > 0) {
        // Swap arr[i] and arr[i + 1]
        let temp = arr[i];
        arr[i] = arr[i + 1];
        arr[i + 1] = temp;
        swapped = true;
      }
    }
    n--; // Reduce the range of comparison
  } while (swapped);

  return arr;
}

// Example usage
const fruits = ['banana', 'apple', 'cherry', 'date'];
const sortedFruits = bubbleSortStrings(fruits);

console.log(sortedFruits); // Output: ['apple', 'banana', 'cherry', 'date'];
```

#SELECTION SORT
1. Selection Sort
Selection sort is an in-place comparison sorting algorithm. It divides the input list into two parts: the sublist of items already sorted, which is built up from left to right at the front (left) of the list, and the sublist of items remaining to be sorted that occupy the rest of the list. Initially, the sorted sublist is empty, and the unsorted sublist is the entire input list. The algorithm proceeds by finding the smallest (or largest, depending on the sorting order) element in the unsorted sublist, swapping it with the leftmost unsorted element (putting it in sorted order), and moving the sublist boundaries one element to the right.

Example: Selection Sort Algorithm for Strings
```javascript
function selectionSortStrings(arr) {
  let n = arr.length;

  for (let i = 0; i < n - 1; i++) {
    let minIndex = i;
    for (let j = i + 1; j < n; j++) {
      if (arr[j].localeCompare(arr[minIndex]) < 0) {
        minIndex = j;
      }
    }
    if (minIndex !== i) {
      let temp = arr[i];
      arr[i] = arr[minIndex];
      arr[minIndex] = temp;
    }
  }

  return arr;
}

// Example usage
const fruits = ['banana', 'apple', 'cherry', 'date'];
const sortedFruits = selectionSortStrings(fruits);

console.log(sortedFruits); // Output: ['apple', 'banana', 'cherry', 'date']
```
2. Insertion Sort
Insertion sort is a simple sorting algorithm that builds the final sorted array one item at a time. It is much less efficient on large lists than more advanced algorithms such as quicksort, heapsort, or merge sort. However, insertion sort provides several advantages:

Simple implementation
Efficient for (quite) small data sets
More efficient in practice than most other simple quadratic (i.e., O(n^2)) algorithms such as selection sort or bubble sort
Adaptive: efficient for data sets that are already substantially sorted
Example: Insertion Sort Algorithm for Strings
```javascript
function insertionSortStrings(arr) {
  let n = arr.length;

  for (let i = 1; i < n; i++) {
    let key = arr[i];
    let j = i - 1;

    while (j >= 0 && arr[j].localeCompare(key) > 0) {
      arr[j + 1] = arr[j];
      j = j - 1;
    }
    arr[j + 1] = key;
  }

  return arr;
}

// Example usage
const fruits = ['banana', 'apple', 'cherry', 'date'];
const sortedFruits = insertionSortStrings(fruits);

console.log(sortedFruits); // Output: ['apple', 'banana', 'cherry', 'date']
```
3. Merge Sort
Merge sort is an efficient, stable, comparison-based, divide and conquer sorting algorithm. Most implementations produce a stable sort, meaning that the order of equal elements is the same in the input and output. Merge sort is a divide and conquer algorithm that was invented by John von Neumann in 1945.

Example: Merge Sort Algorithm for Strings
```javascript
function mergeSortStrings(arr) {
  if (arr.length <= 1) {
    return arr;
  }

  const mid = Math.floor(arr.length / 2);
  const left = arr.slice(0, mid);
  const right = arr.slice(mid);

  return merge(mergeSortStrings(left), mergeSortStrings(right));
}

function merge(left, right) {
  let result = [];
  let leftIndex = 0;
  let rightIndex = 0;

  while (leftIndex < left.length && rightIndex < right.length) {
    if (left[leftIndex].localeCompare(right[rightIndex]) < 0) {
      result.push(left[leftIndex]);
      leftIndex++;
    } else {
      result.push(right[rightIndex]);
      rightIndex++;
    }
  }

  return result.concat(left.slice(leftIndex)).concat(right.slice(rightIndex));
}

// Example usage
const fruits = ['banana', 'apple', 'cherry', 'date'];
const sortedFruits = mergeSortStrings(fruits);

console.log(sortedFruits); // Output: ['apple', 'banana', 'cherry', 'date']
```
4. Quick Sort
Quicksort is an efficient, in-place, comparison-based, divide and conquer sorting algorithm. Developed by Tony Hoare in 1959, it is still a commonly used algorithm for sorting. Quicksort is faster in practice than other O(n log n) algorithms such as merge sort and heapsort.

Example: Quick Sort Algorithm for Strings
```javascript
function quickSortStrings(arr) {
  if (arr.length <= 1) {
    return arr;
  }

  const pivot = arr[arr.length - 1];
  const left = [];
  const right = [];

  for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i].localeCompare(pivot) < 0) {
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }

  return [...quickSortStrings(left), pivot, ...quickSortStrings(right)];
}

// Example usage
const fruits = ['banana', 'apple', 'cherry', 'date'];
const sortedFruits = quickSortStrings(fruits);

console.log(sortedFruits); // Output: ['apple', 'banana', 'cherry', 'date']
```
Summary
These examples cover various sorting algorithms that can be used to sort an array of strings without using the built-in sort method. Each algorithm has its own advantages and use cases:
Selection Sort: Simple and easy to understand, but not efficient for large arrays.
Insertion Sort: Efficient for small or nearly sorted arrays.
Merge Sort: Efficient and stable, with a time complexity of O(n log n).
Quick Sort: Efficient and widely used, with an average time complexity of O(n log n).
Understanding these sorting algorithms and their implementations can help you choose the right one for your specific use case and improve your problem-solving skills in JavaScript.

# Deep copy and Shallow copy:
In JavaScript, copying objects can be done in two ways: shallow copy and deep copy. Understanding the difference between these two types of copies is crucial for managing object references and avoiding unintended side effects.

Shallow Copy
A shallow copy of an object is a copy where only the top-level properties are copied. If the object contains nested objects, the nested objects are not copied; instead, references to the nested objects are copied. This means that changes to the nested objects in the copied object will affect the original object and vice versa.

Example of Shallow Copy
Using Object.assign():
```javascript
const original = {
  name: 'John',
  address: {
    city: 'New York',
    zip: 10001
  }
};

const shallowCopy = Object.assign({}, original);

console.log(shallowCopy); // Output: { name: 'John', address: { city: 'New York', zip: 10001 } }

// Modifying the nested object in the shallow copy
shallowCopy.address.city = 'San Francisco';

console.log(original.address.city); // Output: 'San Francisco' (original object is affected)
```
Using the Spread Operator:
```javascript
const original = {
  name: 'John',
  address: {
    city: 'New York',
    zip: 10001
  }
};

const shallowCopy = { ...original };

console.log(shallowCopy); // Output: { name: 'John', address: { city: 'New York', zip: 10001 } }

// Modifying the nested object in the shallow copy
shallowCopy.address.city = 'San Francisco';

console.log(original.address.city); // Output: 'San Francisco' (original object is affected)
```
Deep Copy
A deep copy of an object is a copy where all levels of the object are copied, including nested objects. This means that changes to the nested objects in the copied object will not affect the original object and vice versa.

Example of Deep Copy
Using JSON Methods:
```javascript
const original = {
  name: 'John',
  address: {
    city: 'New York',
    zip: 10001
  }
};

const deepCopy = JSON.parse(JSON.stringify(original));

console.log(deepCopy); // Output: { name: 'John', address: { city: 'New York', zip: 10001 } }

// Modifying the nested object in the deep copy
deepCopy.address.city = 'San Francisco';

console.log(original.address.city); // Output: 'New York' (original object is not affected)
```
Using a Recursive Function:
```javascript
function deepCopy(obj) {
  if (obj === null || typeof obj !== 'object') {
    return obj;
  }

  if (Array.isArray(obj)) {
    const arrCopy = [];
    for (let i = 0; i < obj.length; i++) {
      arrCopy[i] = deepCopy(obj[i]);
    }
    return arrCopy;
  }

  const objCopy = {};
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      objCopy[key] = deepCopy(obj[key]);
    }
  }
  return objCopy;
}

const original = {
  name: 'John',
  address: {
    city: 'New York',
    zip: 10001
  }
};

const deepCopyObj = deepCopy(original);

console.log(deepCopyObj); // Output: { name: 'John', address: { city: 'New York', zip: 10001 } }

// Modifying the nested object in the deep copy
deepCopyObj.address.city = 'San Francisco';

console.log(original.address.city); // Output: 'New York' (original object is not affected)
```

Summary
Shallow Copy:

Copies only the top-level properties.
Nested objects are not copied; references to the nested objects are copied.
Changes to nested objects in the copied object affect the original object.
Methods: Object.assign(), spread operator (...).
Deep Copy:

Copies all levels of the object, including nested objects.
Changes to nested objects in the copied object do not affect the original object.
Methods: JSON methods (JSON.parse(JSON.stringify(obj))), recursive function.
