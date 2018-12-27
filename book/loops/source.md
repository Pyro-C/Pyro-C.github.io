# Chapter 3: Loops
## 3.1 - Intuition
Many times in programming, we want to be able to do something repeatedly. One way to do this is to,
quite literally, copy-paste a piece of code multiple times. Obviously, this is not ideal. In some
cases, we may want to repeat something indefinitely, in which case it's impossible to use the naive
copy-paste method.

In this chapter, we'll explore a concept called "loops". Loops allow us to express repeated
computation in a compact way.
## 3.2 - The `while` Loop
`while` loops in English:

    while (expression is true)
        do something
Let's see an example in C++, just to get a hang of the syntax:

    #include <iostream>

    using namespace std;

    int main() {
        bool am_hungry = true;
        while (am_hungry) {
            cout << "Let's eat some more!" << endl;
            am_hungry = false;
        }
    }
This code will print `Let's eat some more!` once. That's because `am_hungry` is initially `true`,
but we set it equal to `false` after only one pass in the `while` loop.
***
NOTE: For brevity's sake, we won't be typing this boilerplate code in future examples:

    #include<iostream>
    using namespace std;
    int main() {
        // A bunch of code.
        return 0;
    }
Assume that all code is written in `main` unless stated otherwise.
***
What if we never set `am_hungry` to `false`? What do you think will happen?

    bool am_hungry = true;
    // Equivalent to `while (true)`
    while (am_hungry) {
        cout << "Let's eat some more!" << endl;
    }
This code will print out `Let's eat some more!` forever! `am_hungry` is always `true`, and `true`
is, well, `true`.

Let's see an example with a more detailed expression inside.

    bool x = true;
    int y = 10;
    while ((!x) && (y == 10)) {
        cout << "Hello World!" << endl;
    }
How many times do you think this code will print out `Hello World!`?

If you answered none, you're correct! Let's take a closer look at the `while` statement to see why:

    (!x) && (y == 10)
`y` does indeed equal `10`; however, `x` is set to `true`, and `!x` makes it `false`! Since we know
that `&&` (*the logical AND* operator) requires *both sides of the expression* to be `true`, the
code cannot execute.

Let's try that again, but this time with a different logical operator:

    (!x) || (y == 10)
Remember that `||` is the *logical OR* operator. Only one side of the expression has to be `true`,
so if this expression is inside of the `while` loop, the code will print `Hello World!` infinitely.

Note that in these examples, we encased the boolean expressions `!x` and `y == 10` inside of
parentheses when comparing them using a logical operator. This is important because it cleanly
separates each expression in a readable way.

In this simple example, it would still be pretty readable without parentheses, but if things get
more complicated, parentheses can become very important. Let's build off of our previous example:

    bool x = true;
    int y = 10;
    int z = 10;
    while ((!x) && (y == 10) || (z == 10)) {
        cout << "Hello World!" << endl;
    }
Let's take a look at the expression in the `while` loop:

    (!x) && (y == 10) || (z == 10)
This is very confusing by itself, because it's not entirely clear how the logical operators are
handling this expression. There are a few possibilities:

Case 1:

    // The leftmost expression is being compared to the lone `z == 10`.
    ((!x) && (y == 10)) || (z == 10)
Case 2:

    // The lone `(!x)` is being compared to the rightmost expression.
    (!x) && ((y == 10) || (z == 10))
As it happens, C++ follows the first case and proceeds to print `Hello World!` infinitely, but it'd
be nice if we made things a bit clearer using extra parentheses, as in explicitly following the
first case:

    ((!x) && (y == 10)) || (z == 10)
With the extra parentheses enclosing the first expression completely, it's much more clear that
this expression is being evaluated *before* comparing it to the rightmost expression.
## 3.3 - The `do while` Loop
The `do while` loop is almost identical to the `while` loop.

The only difference is the *order* in which the the code operates.

For a `while` loop, the condition is checked; if it's true, the code in the block executes. For a
`do while` loop, the code in the block executes, and *then* the condition is checked.

Let's see an example to solidify this:

    int n = 0;
    // Check the condition. If the expression is `false`, then don't execute the code.
    while (n != 0) {
        // Now execute the code.
        n++;
    }
    cout << n << endl;
This prints out `0` as expected. Now with `do while`:

    int n = 0;
    // Execute the code right away. We're not checking the condition just yet.
    do {
        n++;
        // Now we check the condition. If it's `false`, then stop the loop.
    } while (n != 0);  // Don't forget this semicolon!
    cout << n << endl;
This prints out `1`, unlike the plain `while` loop. You can see that the differing order of
operations caused the code to behave differently, even though we started with the same variable `n`
and the same expression `n != 0`.
## 3.4 - The `for` Loop
In English, the `for` loop could be written as follows:

    for some N amount of times
        do this
In C++, we express this as follows:

    for (int i = 0; i < 10; i++) {
        cout << "Hello World!" << endl;
    }
This code will print `Hello World!` 10 times.

`for` loops in C++ work by keeping track of an integer, in this case `i`, in order to repeat
computation for a set amount of times. Let's see how this works by breaking apart the previous
example:

    int i = 0; i < 10; i++
The first part of the expression declares the integer that will be used to keep track of the
repeated computation. We set it equal to `0`.

The next part declares a condition; so long as that condition is `true`, the code inside of the
`for` loop will execute. Once it's no longer `true`, the `for` loop stops.

The last part controls how the integer changes after each execution of the inside of the `for`
loop. The `++` indicates that we increment it by `1`.

Let's see this in action once more with a different example:

    for (int a = 0; a < 2; a++) {
        cout << a << endl;
    }
What do you think this code will do?

This code prints out the controlling integer `a` out until the loop terminates.

At the first iteration, `a` is simply `0` as it was initialized. So `0` is printed to the screen.
Now C++ increments `a` by `1`.

Now that the first iteration is over, C++ checks to ensure that `a` is still less than `2`. It is,
so the second iteration begins. `a` was incremented after the last iteration, so now it's `1`. So
`1` is printed to the screen. Now C++ increments `a` once more.

Now `a` is `2`. Will C++ run through the loop again? No, since it fails the condition.

In summary, the code will print the following to the screen:

    0
    1
Let's play around a little with the `for` loop. Instead of counting up, let's try counting down!

    for (int i = 5; i > 0; i--) {
        cout << i << endl;
    }
What do you think this code will print out? Note that `--` is the opposite of `++`; instead of
incrementing by one, it *decrements* by one.

This code prints out the following to the screen:

    5
    4
    3
    2
    1
You can tinker around with `for` loops even further; we could count up by 2s!

    // Note that `i += 2` is equivalent to `i = i + 2`. We're incrementing `i` by `2`.
    for (int i = 2; i < 10; i += 2) {
        cout << i << endl;
    }
    cout << "Who do we appreciate?" << endl;
This code will print out:

    2
    4
    6
    8
    Who do we appreciate?
## 3.5 - The `break` Statement
So far, we've shown how to facilitate repeated computation using loops. There's also a tool to stop
that repeated computation before the loop is programmed to terminate; that's the `break` statement:

    while (true) {
        cout << "Howdy, partner!" << endl;
        break;
    }
Here, the loop would normally print `Howdy, partner!` infinitely. However, we added a `break`
statement, which essentially tells C++ to immediately stop the loop and exit out of it. Therefore,
this code will only print `Howdy, partner!` once.

Let's see an example with a `for` loop:

    cout << "It's the final countdown" << endl;
    for (int i = 10; i > 0; i--) {
        cout << i << endl;
        break;
    }
    cout << "It's the final countdown, yeah" << endl;
Does the final countdown complete?

If you answered "no", you're correct! The `break` statement works exactly the same as with the
`while` loop. Once C++ sees `break`, the loop is immediately terminated, and the computer moves on
to the next line of code. This code will print:

    It's the final countdown
    10
    It's the final countdown, yeah
## 3.Q - Questions
Here, you can test your knowledge of what you've learned up to this point!
***
QUESTION 1: What will the following block of code do?

    cout << "Enter an integer: ";
    int num;
    cin >> num;
    for (int i = 0; i <= num; i++) {
        if (i % 2) {
            cout << i << " is odd!\n"; 
        }
        else {
            cout << i << " is even!\n";
        }
    }
ANSWER: Prints out the even and odd numbers starting from 0 to the number entered by the user.
***
QUESTION 2: How should this code be changed to run 10 times?

    for (int i = 0; i < 5; i++) {
        cout << "Hello World!" << endl;
    }
ANSWER: Change the `i < 5` to be `i < 10`.

    for (int i = 0; i < 10; i++) {
        cout << "Hello World!" << endl;
    }
***
QUESTION 3: This `for` loop is bugged. What's wrong with it?

    for (int i = 0, i < 10, i++) {
        cout << i + 1 << endl;
    }
ANSWER: Commas cannot be used to separate the syntactic elements of the `for` loop. You must use
semicolons.
***
QUESTION 4: Change this code so that it counts down from 42 all the way to, *and including*, 13.

    for (int i = 100; i < 56; i--) {
        cout << i << endl;
    }
ANSWER: Change the first and second syntactic elements of the `for` loop accordingly.

    for (int i = 42; i >= 13; i--) {
        cout << i << endl;
    }
***
