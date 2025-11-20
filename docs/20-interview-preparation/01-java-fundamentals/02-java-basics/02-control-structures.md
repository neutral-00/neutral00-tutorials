# Control Structures in Java

Control structures in Java determine the flow of execution of a program. They allow you to make decisions, repeat actions, and control the program's behavior based on conditions.

---

## 1. Types of Control Structures
Java provides three main types of control structures:
1. **Decision-Making Statements**
2. **Looping Statements**
3. **Branching Statements**

| Control Structure       | Purpose                                      | Examples                                   |
|--------------------------|----------------------------------------------|-------------------------------------------|
| Decision-Making          | Executes code based on conditions.          | `if`, `if-else`, `switch`                 |
| Looping                  | Repeats code until a condition is met.       | `for`, `while`, `do-while`, enhanced `for`|
| Branching                | Alters the normal flow of execution.         | `break`, `continue`, `return`             |

---

## 2. Decision-Making Statements
Decision-making statements allow the program to execute certain parts of the code based on conditions.

### Types:
- **`if` Statement**
- **`if-else` Statement**
- **`if-else-if` Ladder**
- **`switch` Statement**

### Example:
```java
public class DecisionMakingExample {
    public static void main(String[] args) {
        int number = 10;

        // if-else statement
        if (number > 0) {
            System.out.println("The number is positive.");
        } else {
            System.out.println("The number is negative.");
        }

        // switch statement
        switch (number) {
            case 10:
                System.out.println("The number is 10.");
                break;
            default:
                System.out.println("The number is not 10.");
        }
    }
}
```

---

## 3. Looping Statements
Looping statements allow the program to execute a block of code multiple times.

### Types:
- **`for` Loop**
- **`while` Loop**
- **`do-while` Loop**

### Example:
```java
public class LoopingExample {
    public static void main(String[] args) {
        // for loop
        for (int i = 0; i < 5; i++) {
            System.out.println("Iteration: " + i);
        }

        // while loop
        int count = 0;
        while (count < 3) {
            System.out.println("Count: " + count);
            count++;
        }

        // do-while loop
        int num = 0;
        do {
            System.out.println("Number: " + num);
            num++;
        } while (num < 2);
    }
}
```

---

## 4. Branching Statements
Branching statements allow the program to alter the flow of execution by breaking out of loops or skipping iterations.

### Types:
- **`break` Statement**
- **`continue` Statement**

### Example:
```java
public class BranchingExample {
    public static void main(String[] args) {
        // break statement
        for (int i = 0; i < 5; i++) {
            if (i == 3) {
                break; // Exit the loop when i is 3
            }
            System.out.println("i: " + i);
        }

        // continue statement
        for (int i = 0; i < 5; i++) {
            if (i == 2) {
                continue; // Skip the iteration when i is 2
            }
            System.out.println("i: " + i);
        }
    }
}
```

## 5. Summary

| Control Structure       | Purpose                                      | Examples                                   |
|--------------------------|----------------------------------------------|-------------------------------------------|
| Decision-Making          | Executes code based on conditions.          | `if`, `if-else`, `switch`                 |
| Looping                  | Repeats code until a condition is met.       | `for`, `while`, `do-while`, enhanced `for`|
| Branching                | Alters the normal flow of execution.         | `break`, `continue`, `return`             |