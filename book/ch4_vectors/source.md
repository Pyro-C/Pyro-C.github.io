# Chapter 4: Vectors
## 4.1 - Basic Vector Operations
The *vector* is one of the simplest data structures in C++, but its usefulness knows no bounds. You
can think about vectors as a list of elements of some datatype. Let's dive right in with an
example!

    #include <iostream>
    // We have to include `vector` from the STL to use it.
    #include <vector>

    using namespace std;

    int main() {
        // Let's declare a vector of integers.
        // First, we type `vector`.
        // Then, in between angled brackets, we declare the datatype this vector will hold.
        // Then add a space, and type the name of the vector.
        // Don't forget the semicolon!
        vector<int> my_vector;
        return 0;
    }
The program above declares a vector, then exits out of the program, doing nothing else.
***
NOTE: For brevity's sake, we won't be typing this boilerplate code in future examples:

    #include<iostream>
    #include<vector>
    using namespace std;
    int main() {
        // A bunch of code.
        return 0;
    }
Assume that all code is written in `main` unless stated otherwise.
***
Now, let's get back to vectors.

    vector<int> my_vector;
We just declared this vector, but we added nothing to it. Therefore, its size must be zero.
To get the size of a vector, use the `.size()` method.

    int size_of_my_vector = my_vector.size()
    cout << size_of_my_vector << endl;
    // The above code will print out `0` to the screen.
Remember that vectors are like lists. Let's try adding an item to our "list"!
We declared `my_vector` to hold integers, so it can only hold integers.
Let's try adding an integer to the vector. We have to use `.push_back(something)`.

    my_vector.push_back(22);
    my_vector.push_back(8);
    my_vector.push_back(42);
Alternatively, you could also use the following syntax with braces `{}`:

    my_vector = {22, 8, 42};
Every item in a vector is given an *index*. You can think of indices (plural for "index") as
"page numbers". Indices keep track of the order of elements in a vector. In order to use them,
we have to use `.at(index)`.

    // Indices start at 0, and increase by 1 for every element added afterwards.
    int first_element = my_vector.at(0);
    cout << first_element << endl;
    // The above code will print out `22` to the screen, since that was the first thing added.
    cout << my_vector.at(1) << endl;
    cout << my_vector.at(2) << endl;
    // The above code will print out `8` and then `42`.
You can use indices to remove elements from a vector. The syntax is as follows:

    vec.erase(vec.begin() + index);
So with our vector, `my_vector`, if we wanted to remove the second element (which is at index 1),
we should do the following:

    my_vector.erase(my_vector.begin() + 1)
***
NOTE: This syntax may seem strange at first, but don't worry. The short story is that it relies on
objects called *pointers*, which we will learn about later in this chapter. For now, we just want
to get you to speed with these basic operations!
***
Now let's remove the other elements in our vector! We already took away the second element, `8`,
which means that the new element in that index is `42`. Let's remove that and the first element,
`22`.

    my_vector.erase(my_vector.begin() + 1)
    my_vector.erase(my_vector.begin() + 0)  // The `+ 0` is optional.
    cout << my_vector.size() << endl;  // This will print `0` since everything's gone now.
## 4.2 - Vectors w/ Other Datatypes
Everything we talked about in `4.1` is relevant to other datatypes as well! Nothing fundamentally
changes when operating with other datatypes. Here, we present some code snippets of vectors holding
commonly-used datatypes. We do some of the same operations we talked about in `4.1`.

With *strings*:

    vector<string> vec;
    vec.push_back("hello world");
    // Prints out `hello world`.
    cout << vec.at(0) << endl;
With *floats*:

    vector<float> vec;
    vec.push_back(3.14);
    // Prints out `Pi is approximately 3.14`.
    cout << "Pi is approximately: " << vec.at(0) << endl;
With *booleans*:

    vector<bool> vec;
    vec.push_back(true);
    vec.push_back(false);
    // Prints out `2`.
    cout << vec.size() << endl;
    vec.erase(vec.begin() + 1);
    vec.erase(vec.begin());
    // Prints out `0`
    cout << vec.size() << endl;
You can even make vectors out of vectors!

    vector<vector<string>> groceries;
    vector<string> produce;
    vector<string> dairy;
    groceries.push_back(produce);
    groceries.push_back(dairy);
    // Adding `apples` to the first vector in `groceries`, which is `produce`.
    groceries.at(0).push_back("apples");
    // Prints out the first element of the first vector: `apples`
    cout << groceries.at(0).at(0) << endl;
    // Prints out `2` since there are two vectors inside of `groceries`.
    cout << groceries.size() << endl;
## 4.3 - Range Based `for` Loops
You can use indices to loop through vectors. Let's say you have a vector:

    vector<string> fruits = {"apple", "banana", "cherry", "peach", "strawberry"};
The following code will print every element in `fruits`:

    for (int i = 0; i < fruits.size(); i++) {
        cout << fruits[i] << endl;
    }
This is a typical `for` loop like the one we learned about in the last chapter, but there's also
another way you can loop through the elements of a vector; a special kind of `for` loop called a
"range-based `for` loop". Let's check out the syntax:

    // Here `fruit` is just a placeholder variable that will be filled in with each element.
    // You could replace `fruit` with any name!
    // `fruits` is the name of the vector from which we are getting each element.
    for (string fruit : fruits) {
        cout << fruit << endl;
    }
When looping through elements of a vector, we recommend using this type of `for` loop. This loop is
much simpler than the previous one, and it avoids having to keep track of indices. It's also much
more readable!

Let's see one more example:

    vector<int> vec;
    vec = {1, 2, 3, 4, 5};
    cout << "Let's count to five!" << endl;
    for (int the_number : vec) {
        cout << the_number << endl;
    }
## 4.4 - Sorting Vectors
One of the most fundamental operations you can perform on a vector is *sorting it* from either
smallest to biggest or the other way around. In this section, we will implement and go over a
handful of algorithms that you can use to sort vectors.

We'll test each algorithm on the following vector:

    vector<int> vec = {42, 22, 64, 76, 16, 8, 99};
## 4.4.1 - Regarding Efficiency
As we're now talking more about datastructures and algorithms that are performed on them, it's a
good time to talk about time complexity.

Mathematically, we can represent the performance of an algorithm with a notation called
*Big O Notation*. This notation expresses how an algorithm's performance scales with its inputs.
More specifically, it expresses the *worst case scenario*. What exactly does that mean? We'll talk
about it for each sorting algorithm! For now, let's go over some basic definitions.

If an algorithm always takes a constant amount of time to perform, regardless of the amount of
inputs, we express that as: `O(1)`.

If an algorithm scales linearly as the input grows, we express that as: `O(N)`.

If an algorithm scales with the square of the input's size, we express that as: `O(N^2)`. The `^2`
is supposed to represent a superscript.

Don't worry if you don't understand this right now; we just want to introduce the concept, and
we'll talk about it more throughout the book.
## 4.4.2 - Insertion Sort
Let's try sorting this vector from smallest to biggest using an algorithm called
**insertion sort**.
This is a very simple algorithm that we can implement using what we've taught so far:

    for (int i = 1; i < vec.size(); i++) {
        for (int j = i; j > 0; j--) {
            // If the current value is greater than the previous value...
            if (vec.at(j) < vec.at(j - 1)) {
                // Swap the values!
                int backup_before_overwriting = vec.at(j - 1);
                vec.at(j - 1) = vec.at(j);
                vec.at(j) = backup_before_overwriting;
            } else {
                break;
            }
        }
    }
We start with the outer `for` loop, where we tell C++ to iterate over every value in the array, but
starting at the second value.

Now we have the inner `for` loop, where things get more complicated. We tell C++ to take the
current index that the outer `for` loop is at, and repeatedly do *something* until we've reached
the zeroth index. What is that *something*?

That *something* turns out to be quite simple—all we're doing is swapping the current value at
index `j` with the one before it, under the condition that the current value is *smaller*. Let's
assume that condition was `true`.

After that, the inner `for` loop repeats. Now we look at the same value that we looked at before
(whose index `j` is one smaller than it used to be, thanks to the `for` loop), and once again 
compare it with the value before it. If our condition is true, we swap the values, and loop over
again!

But let's go back to the scenario where we first did our comparison with the value at `j`. What if
it was bigger (i.e. it and the value before it are sorted)? Then, we `break` the inner `for` loop
because the vector (up to that point) is already sorted.

If your head is spinning right now, don't worry! We have another, more *intuitive* and *visual*
explanation for this. Let's take the numbers from our vector:

    42, 22, 64, 76, 16, 8, 99
We start by looking at 22, which is at index `1`. Is it smaller than 42? Yes, so we swap them.

    22, 42, 64, 76, 16, 8, 99
Okay, what's at index `2`? We have a 64. Is 64 smaller than 42? No, so we're fine. Since we started
our sorting process by looking at the *first two* numbers, we know that *up to this point*, the
list is completely sorted. Let's increment our index and move on!

    Our list remains the same, for now.
    22, 42, 64, 76, 16, 8, 99
What's at index `3`? We have a 76. 76 isn't smaller than 64, so we once again move on.

    Once again, nothing changes.
    22, 42, 64, 76, 16, 8, 99
What's at index `4`? We have a 16, which is smaller than 76, the value before it. So we swap them!

    22, 42, 64, 16, 76, 8, 99
But wait! We're not done! We have to take the 16 and *keep moving left* until the value before it
is smaller! Right now, the value before it is 64, which is clearly bigger.

    22, 42, 16, 64, 76, 8, 99
Is 42 smaller than 16? No. Move again!

    22, 16, 42, 64, 76, 8, 99
Once again, we have to move!

    16, 22, 42, 64, 76, 8, 99
Now nothing is before the 16, because 16 is now the first element in the list! Now we can stop
iterating. In the code, this is controlled by the `j > 0` part of the inner `for` loop.

Now we would go back to where we originally saw the 16, which was at index `4`. We increment that
index to `5` and begin the comparison process over again. At index `5`, we have an 8. The value
before it is 76, which isn't smaller than 8, so we do our process of shoving a number over to the
left all over again! At the end of this, we'll have:

    8, 16, 22, 42, 64, 76, 99
Now we go back to the index where the 8 was originally, which was index `5`. We increment that and
look at index `6`, which is a 99. 76 is smaller than 99, so we're good. It's finally over!

Let's ensure that everything worked out fine:

    for (int i : vec) {
        cout << i << endl;
    }
Sure enough, we get:

    8
    16
    22
    42
    64
    76
    99
So we've went over what insertion sort is... but why should we use it in the first place? Let's go
over the pros and cons.

Pros:
* It's simple and easy to understand; trivial to implement.
* It's memory-efficient because it can be performed without needing additional memory. 
* It's online, which means it can sort a list as it receives it, one item at a time.
* It's very fast for lists that are nearly sorted.

Cons:
* I
## 4.4.3 - Selection Sort
TODO

TODO finish this part
also talk about adding into middle of vector or beginning
also ask quiz question about efficiency of removing from beginning vs last of vector
