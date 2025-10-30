Variables
```javascript
let isCool = false;

let name = "Alice";

let age = 42;

let weight = 150.5;

let brainSize = undefined;

const mySkillIssues = 42;
```

>[!warning] Be careful with `let` and `var`
>`let` is block-scoped. Whereas `var` is function-scoped.

Null vs. Undefined
- [`undefined`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined): It doesn't exist _at all_. In grug-speak `undefined` is "very nothing"
- [`null`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/null): It (kind of) exists, but it's _empty_. In grug-speak `null` is "kinda nothing"

Conditionals:
```js
if (height > 6) {
  console.log("You are super tall!");
} else if (height > 4) {
  console.log("You are tall enough!");
} else {
  console.log("You are not tall enough!");
}
```

Here are some common comparison operators:
- `===` equal to
- `!==` not equal to
- `<` less than
- `>` greater than
- `<=` less than or equal to
- `>=` greater than or equal to

>[!info]
>The "strict equals" (`===`) and "strict not equals" (`!==`) compare both the value _and_ the type. The "loose equals" (`==`) and "loose not equals" (`!=`) attempt to convert and compare values of different types. With the loose versions, the string `'5'` and the number `5` are considered "equal", which, in _good_ code, is usually _not_ what you want.

Logical operators
```js
true && true; // true
true && false; // false
true || false; // true
false || false; // false
!false; // true
!true; // false
```

Switch statements
```js
const os = "mac";
let creator;
switch (os) {
  case "linux":
    creator = "Linus Torvalds";
    break;
  case "windows":
    creator = "Bill Gates";
    break;
  case "mac":
    creator = "Steve";
    break;
  default:
    creator = "Unknown";
    break;
}

console.log(creator);
// Steve
```

Ternary operator
```js
const price = isMember ? "$2.00" : "$10.00";
```

Functions
```js
// function declaration
function getSum(a, b) {
  return a + b;
}

// function call
const result = getSum(60, 9);

console.log(result);
// 69
```

Example of named function vs. anonymous function
```js
// We have this function
function conversions(converter, x, y, z) {
  const convertedX = converter(x);
  const convertedY = converter(y);
  const convertedZ = converter(z);
  console.log(convertedX, convertedY, convertedZ);
}

// using a named function
function double(a) {
  return a + a;
}
conversions(double, 1, 2, 3);
// 2 4 6

// using an anonymous function
conversions(
  function (a) {
    return a + a;
  },
  1,
  2,
  3,
);
// 2 4 6
```

Objects
```js
const apple = {
  name: "Apple",
  radius: 2,
  color: "red",
};

// Access properties
console.log(apple.name); // prints "Apple"
console.log(apple.radius); // prints "2"
console.log(apple.color); // prints "red"
```

You can omit the colon and the value
```js
const radius = 2;
const color = "red";
const apple = {
  radius, // same as radius: radius
  color: color, // set explicitly for demonstration
};
```

Objects can contain other objects:
```js
const tournament = {
  referee: {
    name: "Sally",
    age: 25,
  },
  prize: {
    units: "dollars",
    value: 100,
  },
};

// Access them
console.log(tournament.referee.name); // Sally
console.log(tournament.prize.value); // 100
```

Object methods:
```js
const person = {
  firstName: "Lane",
  lastName: "Wagner",
  getFullName() {
    return this.firstName + " " + this.lastName;
  },
};

console.log(person.getFullName());
// Lane Wagner
```

Spread Syntax, shallow-copies of the objects' properties:
```js
const engineering_dept = {
  lane: "software engineer",
  hunter: "software engineer",
};

const video_dept = {
  lane: "cringe youtuber",
  alex: "video producer",
};

const all_employees = { ...engineering_dept, ...video_dept };
/*
{
  lane: 'cringe youtuber',
  hunter: 'software engineer',
  alex: 'video producer'
}
*/
```

Unpack function return values:
```js
function getApple() {
  const apple = {
    radius: 2,
    color: "red",
  };
  return apple;
}

const { radius, color } = getApple();
console.log(radius); // 2
console.log(color); // red
```

Classes
```js
class User {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

const user = new User("Lane", 100);
```

Private properties `#`:
```js
class Movie {
  #title;
  constructor(title, rating) {
    this.#title = title;
    this.rating = rating;
  }

  getTitleAllCaps() {
    const allCaps = this.#title.toUpperCase();
    return allCaps;
  }
}

const matrixMovie = new Movie("The Matrix", 9.5);
console.log(matrixMovie.getTitleAllCaps());
// THE MATRIX
```

Inheritance
```js
class Titan {
  constructor(name) {
    this.name = name;
  }

  speak(msg) {
    // this gets overridden in the BeastTitan class
    console.log("*titan noises*");
  }
}

class BeastTitan extends Titan {
  speak(msg) {
    console.log(`${this.name} says, "I'm the Beast Titan"`);
  }
}

const pureTitan = new Titan("Eren's mom");
pureTitan.speak();
// *titan noises*

const beast = new BeastTitan("Zeke");
beast.speak();
// Zeke says, "I'm the Beast Titan"
```

Super: to call methods on an object's parent
```js
class Titan {
  constructor(name) {
    this.name = name;
  }

  toString() {
    return `Titan - Name: ${this.name}`;
  }
}

class BeastTitan extends Titan {
  constructor(name, power) {
    // call the parent's constructor
    super(name);
    this.power = power;
  }

  toString() {
    // call the parent's `toString` method
    return `${super.toString()}, Power: ${this.power}`;
  }
}

const beast = new BeastTitan("Zeke", 9000);
console.log(beast.toString());
// Titan - Name: Zeke, Power: 9000
```

