# Chapter 4: Vectors
## 4.1 - Adding, Removing, and Accessing Elements in a Vector
The vector is one of the simplest data structures in C++, but its usefulness knows no bounds. You
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
Every item in a vector is given an "index". You can think of indices (plural for "index") as
"page numbers". Indices keep track of the order of elements in a vector. In order to use them, we
have to use square brackets like so: `[index]`.

    // Indices start at 0, and increase by 1 for every element added afterwards.
    int first_element = my_vector[0];
    cout << first_element << endl;
    // The above code will print out `22` to the screen, since that was the first thing added.
    cout << my_vector[1] << endl;
    cout << my_vector[2] << endl;
    // The above code will print out `8` and then `42`.
You can use indices to remove elements from a vector. TODO finish this part
