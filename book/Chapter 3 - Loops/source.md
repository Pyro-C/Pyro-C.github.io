# Chapter 3: Loops
### 3.1 - Intuition
Many times in programming, we want to be able to do something repeatedly. One way to do this is to,
quite literally, copy-paste a piece of code multiple times. Obviously, this is not ideal. In some
cases, we may want to repeat something indefinitely, in which case it's impossible to use the naive
copy-paste method.

In this chapter, we'll explore a concept called "loops". Loops allow us to express repeated
computation in a compact way.
### 3.2 - The `while` Loop
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
### 3.3 - The `for` Loop
