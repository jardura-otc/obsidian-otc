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