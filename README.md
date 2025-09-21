# Unit 4: Loops

## Introduction
Loops are what we use to execute a block of code repeatedly while a given condition evaluates to true. Loops are helpful because they save time, reduce errors, and make programs more readable.

The types of loops we'll cover now are **for loops** and **while loops**. Although they look different, both of them repeat a block of code based on a condition. \
Like conditionals, loops are also block statements.

An **iteration** is the term for a single execution of the code block, or **body**, of the loop. 

### Table of Contents
- [Introduction](#introduction)
    - [Table of Contents](#table-of-contents)
- [More Math](#more-math)
    - [Precision](#precision)
    - [Mixing `int` and `double`](#mixing-int-and-double)
        - [Integer Division](#integer-division)
    - [The `Math` Class](#the-math-class)
    - [Modulus Operator](#modulus-operator)
    - [>Exercise: Quadratic Formula](#exercise-quadratic-formula)
- [While Loops](#while-loops)
    - [>Exercise: Birthday Party](#exercise-birthday-party)
- [For Loops](#for-loops)
    - [>Exercise: Sums With Loops](#exercise-sums-with-loops)
- [Break and Continue Statements](#break-and-continue-statements)
    - [Break Statements](#break-statements)
    - [Continue Statements](#continue-statements)
    - [>Exercise: Solving Equations](#exercise-solving-equations)
- [Nested Loops](#nested-loops)
    - [>Exercise: Times Tables](#exercise-times-tables)
- [Recap](#recap)
- [>>Project: Guessing Game](#project-guessing-game)

[Feedback](#feedback) \
[License](#license)

## More Math
<sub>(Long detour)</sub>

In Unit 2, you learned about the basic arithmetic operators, `+` `-` `*` `/` and numeric types `double` and `int`. \
Now we'll go a little deeper into these and also introduce more math operations.

### Precision
The two numeric types you learned are `int` and `double`. \
**Precision** refers to, conceptually, how large is the set of numbers that the type can hold. `double` can hold decimal numbers while `int` can only hold integers. So `double` is more precise than `int`.

Also, computers don't have infinite memory, so these types are limited in range and accuracy. \
For example, the maximum possible value for an `int` is $2,147,483,647 = 2^{31} - 1$. \
And `double`s cannot represent infinite digits, values are approximate, rounded. So, `0.1 + 0.2` is actually calculated to be `0.30000000000000004` because of limitations of **binary**, the number system that computers use (like how 1/3 has infinite digits and needs to be rounded eventually). `double`s can hold about 16 digits of precision, and the max value is $1.7976931348623157 * 10^{308}$.

When writing a `double` value, it needs to have a decimal part (with `.`) so that it can be distinguished from an `int`. The value `3` is an `int` while `3.0` is a `double`.

Note that the other types such as `long` and `float` are similar to `int` and `double`, but have different size and precision.

### Mixing `int` and `double`
An `int` value can be used anywhere where a `double` may be used because `int` is less precise than `double`.
```java
double x = 3;
System.out.println(x); // Output: 3.0
```
(For clarity, you still should add the `.0` when assigning whole number `double` values.)

When using an `int` in place of a `double`, the `int` is implicitly converted into a `double`. \
Java does this automatically because `int` to `double` is lossless and equivalent, as `double` is more precise.

Note that this does not happen for `double` to `int` because of the **loss of precision**. It is possible forcefully convert a `double` to an `int` with explicit **casting**, but that won't be taught in this unit.

The conversion from `int` to `double` also happens when doing math operations with both `int`s and `double`s. \
If at least one of the operands is a `double`, the result is also a `double`, regardless of the values of the operands. \
So only when both are `int` is the result also an `int`. \
`5 * 2` gives `10` (`int`), while `5 * 2.0` gives `10.0` (double).

#### Integer Division
For division between two `int`s, <u>the decimal part is removed from the integer result</u>: integer division **truncates** the result. \
So `3 / 2` gives `1`, and `3.0 / 2` gives `1.5`.

Be careful with this behavior, as it can lead to unexpected results:
```java
double portion = 5 / 3;
System.out.println(portion);
```
Output:
```
1.0
```

### The `Math` Class
`Math` is a utility 'container' with various constants and mathematical functions in it. \
To access something, use `Math.<name>` where `<name>` is the name of the thing.

Here are some of the common functions (`int` may used in place of `double` for inputs):
| Function | Description | Input | Output |
| - | - | - | - |
| `Math.abs()` | Absolute value | `double` or `int` | Same as input |
| `Math.sqrt()` | Square root | `double` | `double` |
| `Math.pow()` | Exponentiation (power) | `double` base, `double` exponent | `double` |
| `Math.random()` | Random value, 0.0 <= x < 1.0 | No input | `double` | `Math.max()` | Greater of two values | Two `double`s or `int`s | Same as input |
| `Math.min()` | Lesser of two values | Two `double`s or `int`s | Same as input |

Other things include constants `E` and `PI`, and functions for rounding, flooring, trigonometry, Pythagorean theorem, and angle conversion.

Example `Math` usage:
```java
int x = Math.abs(-3); // 3
double y = Math.sqrt(16); // 4.0
double z = Math.max(Math.E, Math.PI); // 3.141592653589793
```

### Modulus Operator
The modulus operator, `%`, is another arithmetic operator that is less common in mathematics but useful in programming. \
It calculates the remainder of a division operation.

Example:
```java
int x = 10 % 3;
System.out.println(x); // 1
```
10 divided by 3 is equal to 3, remainder 1. \
Another way to think about it is a circle, numbered `0` to `n - 1`. If you go around `x` times, you loop around and land on one of the numbers, equal to `n % x`.

It can be used on both `double`s and `int`s, though it is more common to use it on `int`s. \
One use is to determine divisibility, whether one number is a factor of another. For example, to see if a number is even (divisible by 2), check `n % 2 == 0`.

It has the same operator precedence as multiplication and division.

### >Exercise: Quadratic Formula
You've gotten tired of manually calculating with the quadratic formula. So now, you decide to write a program to do the calculations for you.

When $a \ne 0$, the solutions to the equation $ax^2 + bx + c = 0$ are given by the quadratic formula:
```math
x = {-b \pm \sqrt{b^2-4ac} \over 2a}
```

[`QuadraticFormula.java`](QuadraticFormula.java)
1. Prompt the user to enter the `double` coefficients `a`, `b`, `c`.
2. Use the quadratic formula. (Assume that the coefficient `a` is not zero.)
3. With the formula, there are either 2, 1, or 0 real solutions, depending on the number inside the square root (called the discriminant) in the formula.
    - If the discriminant is positive, there are two real solutions because of the ±. Print both.
    - If the discriminant is equal to 0.0, there is only one real solution. Print it.
    - If the discriminant is negative, there are no real solutions. Print `No solution`.
4. Test your program! Try these examples:
    - `a = 1`, `b = -5`, and `c = 6` should print `2` and `3`
    - `a = 1`, `b = -4`, and `c = 4` should print `2`
    - `a = 1`, `b = 1`, and `c = 1` should print `No solution`

<details><summary>Solution code</summary>

```java
import java.util.Scanner;

public class QuadraticFormula {
    public static void main(String[] args) throws Exception {
        Scanner input = new Scanner(System.in);

        System.out.println("Please enter a: ");
        double a = input.nextDouble();
        System.out.println("Please enter b: ");
        double b = input.nextDouble();
        System.out.println("Please enter c: ");
        double c = input.nextDouble();

        double discriminant = Math.sqrt((b * b) - (4 * a * c));
        if (discriminant > 0.0) {
            double solutionOne = (-b + discriminant) / (2 * a);
            double solutionTwo = (-b - discriminant) / (2 * a);
            System.out.println("Solution 1: " + solutionOne);
            System.out.println("Solution 2: " + solutionTwo);
        } else if (discriminant == 0.0) {
            double solution = -b / (2 * a);
            System.out.println("Solution: " + solution);
        } else {
            System.out.println("No solution");
        }
    }
}
```
Output:
```
Please enter a:
1
Please enter b:
-5
Please enter c:
6
Solution 1: 3.0
Solution 2: 2.0
```
```
Please enter a:
1
Please enter b:
-4
Please enter c:
4
Solution: 2.0
```
```
Please enter a:
1
Please enter b:
1
Please enter c:
1
No solution
```
</details>

## While Loops
A **while loop** loops through a block of code as long as a specific condition is true.

While loops look like this:
```java
while (condition) {
    // code to run repeatedly
}
```
The code inside the while loop will execute repeatedly until `condition` evaluates to `false`.

Example:
```java
int i = 0;
while (i < 10) {
    System.out.println(i);
    i++;
}
// Outputs: 0 1 2 3 4 5 6 7 8 9
```
It's akin to an if statement that repeatedly runs until its condition is `false`.

### >Exercise: Birthday Party
You work at an arcade and have to prepare a 4-year-old's birthday party. They've demanded as many balloons as possible, but not over 6 or they *will* throw a tantrum. And because you're also very lazy, you'd rather have a while loop count the balloons for you.

[`BirthdayParty.java`](BirthdayParty.java)
1. Create a while loop to count balloons.
2. Each iteration, print `MORE BALLOONS!!` and then the current balloon count on the next line.
3. After the 6th balloon, print `STOP!! ENOUGH BALLOONS!!`

<details><summary>Solution code</summary>

```java
public class BirthdayParty {
    public static void main(String[] args) {
        int balloons = 0;
        while (balloons < 6) {
            System.out.println("MORE BALLOONS!!");
            balloons++;
            System.out.println(balloons);
        }
        System.out.println("STOP!! ENOUGH BALLOONS!!");
    }
}
```
Output:
```
MORE BALLOONS!!
1
MORE BALLOONS!!
2
MORE BALLOONS!!
3
MORE BALLOONS!!
4
MORE BALLOONS!!
5
MORE BALLOONS!!
6
STOP!! ENOUGH BALLOONS!!
```
</details>

## For Loops
Counting a known number of iterations is a common use case. A **for loop** is used when we know exactly how many times we want to repeat a given block of code.

For loops look like this:
```java
for (initialization; condition; update) {
    // code to run repeatedly
}
```
- **initialization** is where we initialize the variable, a counter, used in the condition.
- **condition** is the condition checked to determine if the code in the loop should be run (if it's true, the loop runs the code again; if it's false, the loop is exited - it is done running).
- **update** is where we update the variable at the end of the current iteration.

Example:
```java
for (int i = 0; i < 11; i++) {
    System.out.println(i);
}
// Outputs (on separate lines): 0 1 2 3 4 5 6 7 8 9 10
```
Let's take a closer look:
- `int i = 0` is our *initialization*. We are declaring the variable `i` so we can use it in our *condition*.
- `i < 11` is our *condition*. This says that, if i is still less than 5, run the loop again. If i is *not* less than 11, exit the loop.
- `i++` is the **update** we apply to 	`i` before the next iteration of the loop.
- The loop runs 11 times, through `0` to `10`.

Note that the statements in the parentheses don't run *in order*: `i` is not initialized at the start of every iteration, only the beginning of the loop. The condition `i < 11` is run *before* the code block (to check if it should be run at all), but the update `i++` is only applied *after* the code block `System.out.println(i)` is run.

For loops are like specialized while loops. Here's how the same behavior above can be achieved with a while loop:
```java
int i = 0; // initialization
while (i < 11) { // condition
    System.out.println(i);
    i++; // update
}
// Outputs (on separate lines): 0 1 2 3 4 5 6 7 8 9 10
```
Note that you can still update the loop variable inside the body of a for loop, in addition to the update expression.

### >Exercise: Sums with Loops
You want to calculate the sum of every integer from 0 to 10 using a loop.

[`Sums.java`](Sums.java)
1. Declare a variable called `sum` to store the final sum. Set it to 0 to start.
2. Create a for loop that evaluates the value of a variable `i`, starting when `i` is 0 and looping as long as i is less than or equal to 10. `i` should be incremented by 1 after every iteration of the loop.
3. In the body of the loop, set `sum` to its previous value plus `i`.
4. After `sum` is updated, add a print statement inside the loop to print the value of `sum`.
5. After the loop, add another print statement to print `Final sum: ` and the final value of `sum`.

<details><summary>Solution code</summary>

```java
public class Sums {
    public static void main(String[] args) {
        int sum = 0;
        for (int i = 0; i <= 10; i++) {
            sum += i;
            System.out.println("Current sum: " + sum);
        }
        System.out.println("Final sum: " + sum);
    }
}
```
Output
```
Current sum: 0
Current sum: 1
Current sum: 3
Current sum: 6
Current sum: 10
Current sum: 15
Current sum: 21
Current sum: 28
Current sum: 36
Current sum: 45
Current sum: 55
Final sum: 55
```
</details>

## Break and Continue Statements

### Break Statements
**Break** statements are used to exit a loop. We've also seen them used in switch statements, where they terminate the statement once a case has been run.

Break statements look like this:
```java
for (int i = 0; i < 10; i++) {
    if (i == 4) {
        break;
    }
    System.out.println(i);
}
// Output: 0 1 2 3
```
Here, once the loop runs an iteration where `i` is 4, the if statement evaluates to true and runs the `break` statement, which exits the loop entirely.

(Note: if there are multiple, nested loops, `break` only exits the first containing loop.)

### Continue Statements
**Continue** statements are used to jump out of *one* iteration of the loop and continue to the next iteration.

Continue statements look like this:
```java
for (int i = 0; i < 10; i++) {
    if (i > 3 && i < 6) {
        continue;
    }
    System.out.println(i);
}
// Output: 1 2 3 6 7 8 9
```
Here, once the loop runs an iteration where if `i` between 3 and 6, exclusive, the if statement evaluates to true and runs the `continue` statement, which cancels the current iteration and moves on to the next one. This results in `4` and `5` never being printed because that iteration was exited before the print statement.

### >Exercise: Solving Equations

[`Equations.java`](Equations.java)
The function `y = (x - 3) * (x - 8) / (x - 6.0)` is equal to `2` for exactly 2 *positive integer* x values. \
Write a program that prints both solutions, using a while loop. \
Make sure to use `continue` to avoid zero division! \
Stop once you have found the second solution.

<details><summary>Solution Code</summary>

```java
public class Equations {
    public static void main(String[] args) {
        int solutions = 0;
        int x = 0;

        while (solutions < 2) {
            if (x == 6) {
                x++;
                continue;
            }
            double y = (x - 3) * (x - 8) / (x - 6.0);
            if (y == 2) {
                solutions++;
                System.out.println(x);
            }
            x++;
        }
    }
}
```
Output:
```
4
9
```
</details>

## Nested Loops
Just like with conditional statements, loops can be **nested**!

Here's an example with for loops:
```java
// outer loop
for (outer_initialization; outer_condition; outer_update) {
    // inner loop
    for (inner_initialization; inner_condition; inner_update) {
        // code to be run repeatedly
    }
}
```
Here, the entirety of the inner loop will run in *every iteration* of the outer loop.

These are often used for 2 dimensional or grid data. \
Typically, one iteration of the outer loop represents one *row*, and one iteration of the inner loop represents one value (or column) of the current row.

Example:
```java
// outer loop
for (int i = 0; i < 4; i++) {
    // inner loop
    for (int j = 0; j < 4; j++) {
        // Executed on every iteration of the inner loop, which is in
        turn repeated on every iteration of the outer loop
        System.out.print("(" + i + ", " + j + ") ");
    }
    // Executed only on each iteration of the outer loop
    System.out.println();
}
```
Output:
```
(0, 0) (0, 1) (0, 2) (0, 3) 
(1, 0) (1, 1) (1, 2) (1, 3) 
(2, 0) (2, 1) (2, 2) (2, 3) 
(3, 0) (3, 1) (3, 2) (3, 3) 
```
In this example, we are using the statement `System.out.print(msg);`! This does the same thing as `System.out.println()` (prints the message passed into the parentheses), but it doesn't create a new line for the message. This is why the coordinates printed in the same iteration of the outer loop are on the same line. \
After the inner loop finishes, there is a `System.out.println()` with no string given, which starts a new line for the next iteration of the outer loop.

### >Exercise: Times Tables
You want to write a program that will print out the times tables for numbers 1-9.

[`TimesTables.java`](TimesTables.java)
Write two loops to go through the 9 rows and 9 columns. \
In the body of the inner loop, print out the product of the current row and column, followed by a single space. \
Each row of 9 products should appear on its own line.

Expected output:
```
1 2 3 4 5 6 7 8 9 
2 4 6 8 10 12 14 16 18 
3 6 9 12 15 18 21 24 27 
4 8 12 16 20 24 28 32 36 
5 10 15 20 25 30 35 40 45 
6 12 18 24 30 36 42 48 54 
7 14 21 28 35 42 49 56 63 
8 16 24 32 40 48 56 64 72 
9 18 27 36 45 54 63 72 81 
```
Bonus challenge: \
Make the table columns properly aligned.
```
1  2  3  4  5  6  7  8  9  
2  4  6  8  10 12 14 16 18 
3  6  9  12 15 18 21 24 27 
4  8  12 16 20 24 28 32 36 
5  10 15 20 25 30 35 40 45 
6  12 18 24 30 36 42 48 54 
7  14 21 28 35 42 49 56 63 
8  16 24 32 40 48 56 64 72 
9  18 27 36 45 54 63 72 81 
```

<details><summary>Solution Code</summary>

No bonus challenge:
```java
public class TimesTables {
    public static void main(String[] args) {
        for (int i = 1; i <= 9; i++) {
            for (int j = 1; j <= 9; j++) {
                System.out.print(i * j + " ");
            }
            System.out.println();
        }
    }
}
```
</details>

## Recap
- `double` has more precision than `int`, and data has limited precision
- `int` can be used anywhere where a `double` can, and math operations involving both will produce `double`
- Dividing two `int`s gives the truncated `int` result (without the decimal part)
- The `Math` class has functions such as `abs()`, `sqrt()`, `pow()`, `random()`, `max()`
- The modulus operator `%` calculates the remainder of division, and can be used to test divisibility
- `while` loops repeat a block until a boolean condition is `false`
– `for` loops count a number of iterations, and the statement includes *initialization*, *condition*, and *update* expressions.
- The `break` statement stops and exits the containing loop immediately
- The `continue` statement skips the rest of the current iteration, and jumps to the start of the next one
- Loops can be nested, which can represent a grid (typically with outer loop as the rows, inner loop as the values/columns)

<!--
### Keyboard Shortcuts
-->

## >>Project: Guessing Game
Create a program for a repeatable game where the user guesses a random number. \
[`Guess.java`](Guess.java)

The user has 10 guesses to find a random number from `1` to `1000` inclusive. \
Before each guess, the number of guesses left is printed (starting at 10).
After each guess, the program tells the user if the guess is too low, too high, or correct. \
The game ends when the player gets the number, or when the player uses all ten guesses. \
A win message is printed for a win, and for a loss, a lose message including the random number is printed.

After the game ends, the user may input `y` or `Y` to play again; all other inputs exit the game.

The random number generator for an `int` from `1` to `1000` inclusive is provided for you. \
Use the expression `randomNumber()` to get one:
```java
int number = randomNumber();
```
<details><summary>Example input/output</summary>

```
10 guesses left
Guess a number between 1 and 1000:
600
Too low!
9 guesses left
Guess a number between 1 and 1000:
800
Too low!
8 guesses left
Guess a number between 1 and 1000:
900
Too high!
7 guesses left
Guess a number between 1 and 1000:
850
Too low!
6 guesses left
Guess a number between 1 and 1000:
875
Too high!
5 guesses left
Guess a number between 1 and 1000:
860
Too low!
4 guesses left
Guess a number between 1 and 1000:
870
Too high!
3 guesses left
Guess a number between 1 and 1000:
865
Correct! You win!
Play again? (y/n)
y
10 guesses left
Guess a number between 1 and 1000:
200
Too high!
9 guesses left
Guess a number between 1 and 1000:
100
Too low!
8 guesses left
Guess a number between 1 and 1000:
50
Too low!
7 guesses left
Guess a number between 1 and 1000:
120
Too low!
6 guesses left
Guess a number between 1 and 1000:
140
Too low!
5 guesses left
Guess a number between 1 and 1000:
160
Too low!
4 guesses left
Guess a number between 1 and 1000:
180
Too low!
3 guesses left
Guess a number between 1 and 1000:
185
Too low!
2 guesses left
Guess a number between 1 and 1000:
190
Too low!
1 guesses left
Guess a number between 1 and 1000:
195
Too low!
You lost. The number was 199
Play again? (y/n)
n
Exiting.
```
</details>

## Feedback
Please provide feedback if you have any. \
Also, please give an estimate of how much time you spent on this unit.

<details><summary>Possible feedback points</summary>

- Confusing explanations
- Knowledge, skills, or procedures that were required but weren't taught
- Too fast or too slow explanations; pacing
- Too hard or too easy exercises
- Step-by-step instructions that are not comprehensive/thorough enough, or didn't work
- Seemingly unnecessary or ineffective information or exercises
- Any improvements (e.g. wording) or more effective ways/formats to teach
</details>

___



## License
© 2025 @aatle, @spacepotatoes3, @gjgarson, @KaitoTLex

This work is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).
