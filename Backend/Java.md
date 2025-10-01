## Index
[[#Resources]]
[[#Commands]]
[[#Basics]]
[[#Booleans]]

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
java file.java
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

