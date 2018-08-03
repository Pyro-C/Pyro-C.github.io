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
Every item in a vector is given an *index*. You can think of indices (plural for "index") as
"page numbers". Indices keep track of the order of elements in a vector. In order to use them, we
have to use square brackets like so: `[index]`.

    // Indices start at 0, and increase by 1 for every element added afterwards.
    int first_element = my_vector[0];
    cout << first_element << endl;
    // The above code will print out `22` to the screen, since that was the first thing added.
    cout << my_vector[1] << endl;
    cout << my_vector[2] << endl;
    // The above code will print out `8` and then `42`.
You can use indices to remove elements from a vector. The syntax is as follows:

    vec.erase(vec.begin() + index);
So with our vector, `my_vector`, if we wanted to remove the second element (which is at index 1),
we should do the following:

    my_vector.erase(my_vector.begin() + 1)
***
NOTE: This syntax may seem strange at first, but don't worry. The short story is that it relies on
objects called *pointers*, which we will learn about later in chapter 5, where we talk about
functions and "call by reference" parameters. For now, we will move on.
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
    cout << vec[0] << endl;
With *floats*:

    vector<float> vec;
    vec.push_back(3.14);
    // Prints out `Pi is approximately 3.14`.
    cout << "Pi is approximately: " << vec[0] << endl;
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
    groceries[0].push_back("apples");
    // Prints out the first element of the first vector: `apples`
    cout << groceries[0][0] << endl;
    // Prints out `2` since there are two vectors inside of `groceries`.
    cout << groceries.size() << endl;
## 4.3 - Vector Initialization & Looping
TODO

TODO finish this part
also talk about adding into middle of vector or beginning
also ask quiz question about efficiency of removing from beginning vs last of vector
