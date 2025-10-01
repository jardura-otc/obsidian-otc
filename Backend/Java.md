## Index

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
