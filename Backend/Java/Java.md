## Index
[[#Resources]]
[[#Commands]]
[[#Basics]]
[[#Booleans]]
[[#String class]]
[[#If-Else Statements]]
[[#Arrays]]
[[#For-Each]]
[[#For Loops]]
[[#Nullability]]
[[#Ternary operators]]
[[#Class]]
[[#Lists]]
[[#Generics]]

---
---
---
### Resources
[Learn Java - Official Oracle's Tutorial](https://dev.java/learn)
[Build a Java app with VS Code](https://dev.java/learn/vscode-java)

---
### Commands
```powershell
# Execute a file
java className.java

# Compile
javac className.java # Converts to .class file
# Execute the .class file
java className
```

---
### Basics
```java
int count = 1; // Assign initial value
count = 2; // Update to new value
```
All functions need to be defined in a class:
```java
class Calculator {
	// Create a method to be called by other classes.
	// Define the kind of data to be returned at the beginning.
	public int add(int x, int y) {
		return x + y;
	}
}
```
To call a method:
```java
int sum = new Calculator().add(1, 2);
```

`//` -> Single comments
`/* */` -> Multiline comments

---
---
### Booleans
```java
boolean isTrue = true;
boolean isFalse = false;
```
- `!` (NOT): negates the boolean.
- `&&` (AND): takes two booleans and results in true if they're both true.
- `||` (OR): results in true if any of the two booleans is true.

---
---
### String class
```java
String fruit = "Apple";
```
[String class methods](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#method.summary)

---
---

### If-Else Statements
```java
// if-then statement
class Car {
	void drive() {
		if (fuel > 0) {
			fuel--;
		}
	}
}

// if-then-else statement
class Car {
	void drive() {
		if (fuel > 0) {
			fuel--;
		} else {
			stop();
		}
	}
}

// else if clause
class Car {
	void drive() {
		if (fuel > 5) {
			fuel--;
		} else if (fuel > 0) {
			turnOnFuelLight();
		} else {
			strop();
		}
	}
}
```

---
### Arrays
```java
// Standard syntax
type[] variableName = new type[size];
// Declare array with explicit size
int[] twoInts = new int[2];

// Two ways to declare and initialize and array
int[] threeIntsV1 = new int[] {4, 9, 7};
int[] threeIntsV2 = {4, 9, 7};

// Assign second element by index
twoInts[1] = 8;

// Retrieve the second element by index and assign it
int secondElement = twoInts[1];

// Example of accessing an array with for-each
char[] vowels = {"a", "e", "i", "o", "u"};
// Access to all the values
for (char vowel: vowels) {
	System.out.print(vowel);
}

// Control over which values to iterate over
for (int i = 0; i < 3; i++) {
	System.out.print(vowels[i]);
}
```

[Array's class functions](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html)

---
### For-Each
```java
for (declaration: collection) {
	body;
}

// Example of accessing an array with for-each
char[] vowels = {"a", "e", "i", "o", "u"};
// Access to all the values
for (char vowel: vowels) {
	System.out.print(vowel);
}
```

---
### For Loops

```java
for (initialization; test; update) {
	body;
}

// Example
for (int i = 1; i <= 4; i++) {
	System.out.println("square of " + i + " is " + i * i);
}
```

---
### Nullability
- Primitive data types all have a default zero value and therefore can never be `null`.
- Reference types contain the memory address of an object and can have a value of `null`

```java
String str = null;
```
---
### Ternary operators
Simple `if/else` usually used in `return` statements. Just one single line to make the decision, returning the left value if the expression is `true` and the right value if `false`:

```java
// model
condition ? valueIfTrue : valueIfFalse

// example
boolean expr = 0 != 200; // expr is true

// "If expr is true, assign 22 to value, otherwise assign 33"
int value = expr ? 22 : 33;
```

---
### Class
- `public`: the member can be accessed by any code (no restrictions).
- `private`: the member can only be accessed by code in the same class.

```java
class Car {
	// Accessible by anyone and initialized
	public int weight = 2500;
	// Only accessible by code in this class and default value
	private String color;
	
	// Private field updated by calling a method.
	private int carsImported;
	
	public void importCars(int numberOfCars) {
		// Update private field from public method
		carsImported = carsImported + numberOfCars;
	}
}

// Create an instance of the class
Car newCar = new Car();
// Access a public field
newCar.weight; // 2500
```

---
### Lists

Lists may be empty or hold any number of items (including duplicates). Lists are a generic interface typed to indicate which type of objects they can contain.
```java
List<String> emptyListOfStrings = List.of();
List<Integer> singleInteger = List.of(1);
List<Boolean> threeBooleans = List.of(true, false, true);
List<Object> listWithMultipleTypes = List.of("hello", 1, true);

// Methods to add, remove, get and check for an element
List<Character> vowels = new ArrayList<>(List.of('a', 'e', 'i', 'o', 'i', 'e', 'a'));

int startingSize = vowels.size(); // 7

vowels.add("u") // "u" appended

char a = vowels.get(0); // a

boolean hadI = vowels.remove("i"); // true and deletes the first "i"

boolean hasI = vowels.remove("i"); // true (one more left)
```

---
### Generics
They're like labeled boxes in programming.
When you create a list or collection to hold things, you can tell Java **what type of thing** goes inside.
```java
// A box specifically for text (Strings)
List<String> names = new ArrayList<String>();
names.add("Alice");   // ✓ Works!
names.add("Bob");     // ✓ Works!
names.add(42);        // ✗ ERROR! Java says "Hey, this box is for text only!"

// When you take something out, Java knows it's text
String name = names.get(0);  // No need to tell Java, it already knows!

// Common examples
List<String> groceryList;        // List of text items
List<Integer> ages;              // List of numbers
Map<String, Integer> scores;     // Pairs of names and scores

// Or whatever you decide
class Container<E> {
	private E object;
	public void set(E object) {
		this.object = object;
	}
	public E get() {
		return object;
	}
}
// Declare the type it holds
// empty <> can infer from context
Container<String> stringContainer = new Container<>();
// compiler knows this is a String, so it is allowed
stringContainer.set("Some string");
// no cast needed, compiler knows it is a String
String result = stringContainer.get();
// this causes a compiler error:
stringContainer.set(42);
```

---

### Date-Time
`java.time` has different classes to work with dates and time.
- [LocalDate docs](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html)
- [LocalDateTime docs](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDateTime.html)
- [DateTimeFormatter docs](https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html)

