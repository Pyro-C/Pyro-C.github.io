# Chapter 4: Vectors
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
The program above declares a vector, then exits out of the program; let's dive deeper. For
brevity's sake, we won't be typing this boiler plate code in future examples:

    #include<iostream>
    #include<vector>
    using namespace std;
    int main() {
        // A bunch of code.
        return 0;
    }
Assume that all code is written in `main`.

Now, let's get back to vectors.

    vector<int> my_vector;
    // We just declared this vector, but we added nothing to it.
    // Therefore, its size must be zero.
    // To get the size of a vector, use the `.size()` method.
    int size_of_my_vector = my_vector.size()
    cout << size_of_my_vector << endl;
    // The above code will print out `0` to the screen.
