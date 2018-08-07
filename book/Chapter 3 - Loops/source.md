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

    while (something is true)
        do something
Let's see an example in C++, just to get a hang of the syntax:

    bool am_hungry = true;
    while (am_hungry) {
        cout << "Let's eat some more!" << endl;
        am_hungry = false;
    }
This code will print `Let's eat some more!` once. That's because `am_hungry` is initially `true`,
but we set it equal to `false` after only one pass in the `while` loop.
