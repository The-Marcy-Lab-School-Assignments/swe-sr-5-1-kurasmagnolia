<!-- @format -->

# Technical Writing Assignment

For guidance on setting up and submitting this assignment, refer to the Marcy lab School Docs How-To guide for [Working with Short Response and Coding Assignments](https://marcylabschool.gitbook.io/marcy-lab-school-docs/fullstack-curriculum/how-tos/working-with-assignments#how-to-work-on-assignments).

## Prompt 1

Imagine you are teaching a friend about OOP. They mainly want to understand what is Encapsulation. Write a brief lesson on Encapsulation that includes the following:

- What is encapsulation?
- What major goal does this help to achieve in software engineering?
- Give an example (in code) of encapsulation.
- An explanation of how the code example demonstrates encapsulation

### Response 1

## Prompt 2

The following `friendsManager` object is an example of an interface that is **NOT** consistent and predictable:

```js
const friendsManager = {
  friends: [],
  addFriend(newFriend) {
    if (typeof newFriend !== 'string') return;
    this.friends.push(newFriend);
  },
};

friendsManager.addFriend('daniel');
friendsManager.addFriend(true);
friendsManager.friends.push('emmaneul');
friendsManager.friends.push(42);
```

Explain how the code is not consistent or predictable, then provide an example in code that uses closure to make it more consistent and predictable.

### Response 2

The code shown above isn't consistent nor predictable because the methods within the function has drect access to the friends array. This allows the friends array to manipulated using the `.addFriend()` method **AND** directly by doing `friendsManager.friends.push()`, which leaves the data vunerable to entering false data and more.

```JavaScript
// Improved friendsManager using closure
const makeFriendsManager = () => {
  const friends = [];

  const friendMaker = {
    addFriend(newFriend) {
      if (typeof newFriend !== 'string') return;
      friends.push(newFriend);
    },
    printFriends() {
      console.log(friends);
    },
  };

  return friendMaker;
};

// Create a new instance of friendsManager
const friendsManager = makeFriendsManager();

// Test the functionality
friendsManager.addFriend('daniel');
friendsManager.addFriend('emmanuel');
friendsManager.addFriend('alice');
friendsManager.printFriends(); // output: ['daniel', 'emmanuel', 'alice']

friendsManager.addFriend(true); // attempting to add a boolean to the array
friendsManager.printFriends(); // output: ['daniel', 'emmanuel', 'alice']
friendsManager.friends = []; // this won't affect the internal friends array
friendsManager.printFriends(); // Output: ['daniel', 'emmanuel', 'alice']

```

The code above uses closure to ensure that the friends array cannot be accessed directly.

- `makeFriendsManager` is a function that encapsulates the friends array and its manipulation methods (addFriend and printFriends) within an inner function, the `friendMaker` object.

- Closure ensures that friends array is initialized in the outer funcction scope and only accessible through the methods provided (addFriend and printFriends), as references, preventing direct manipulation or access from outside the object.

## Prompt 3

With OOP in JavaScript, it's possible to use factory functions to achieve encapsulation and re-use them to make objects that look alike. However, factory functions have drawbacks and we often use classes instead.

How would you explain to a budding developer what the drawbacks of using factory functions are and why it is better to use classes instead?

### Response 3

## Prompt 4

Do some research on the history of when / how classes were introduced into JavaScript and share your findings. Your response should include:

- What version of JavaScript were classes introduced in and when did it come out?
- Why were classes introduced into JavaScript?

### Response 4

`Classes` were introduced into JavaScript in June of 2015, when the 6th edition of ECMAScript 6 (ES6) was released. ECMAScript is the standardized specification that defines the JavaScript programming language.

`Classes` were introduced in ECMAScript 6 (ES6) to make JavaScript more structured and intuitive, particularly for developers coming from languages like Java and C++. Before ES6, JavaScript relied on prototypal inheritance, which, while powerful, could be complex and unintuitive.

By introducing a familiar class-based syntax, ES6 made it easier for developers to write, organize, and manage object-oriented code while still leveraging JavaScript’s prototype-based nature under the hood.

## Prompt 5

OOP can still be achieved in JavaScript without using the `class` keyword and instead using the "Constructor Functions" and the "Prototype Chain" (look them up!)

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.greet = function () {
  return `Hi, I'm ${this.name}, and I'm ${this.age} years old.`;
};

const alice = new Person('Alice', 30);
console.log(alice.greet());
```

Provide one point that advocates for the use of this syntax and then provide a counter-argument for the use of classes instead.

### Response 5
