# What are we doing today?

-   Classes in C++
-   Handling merge conflicts in `git`


# What are classes?

-   Definitions for objects, i.e. what data and methods they have
    -   In other words, a blueprint for how to create an object
-   An object is called an **instance** of a class
    -   An object has all the functions and data structures defined in its class
    -   Data schema is the same across all instances of a class, but values differ
    -   It's interchangeable with other objects from the same class


# A simple example

<div class="NOTES">
A class can have some data and some methods, which can either be public or private. Private means only visible to the class itself, public means visible to any other file. Drop to a terminal and use/modify this class.

</div>

```c++
class example {
    private:         // private is also implied if you don't specify visibility
	int a;
    public:
	int getA() { return a; }
};
```


# Why bother?

-   Software projects are easier to understand when related data and functions are grouped together
-   Abstracting data behind getters/setters allows you to validate inputs from other parts of your application
-   Abstracting complex tasks into class methods enables simpler, easier to read high-level code
-   Classes can be extended to add functionality with minimal extra code using inheritance


# Static members

<div class="NOTES">
Drop to a terminal and use this class.

</div>

-   For when you want data or functions to be part of your class, but they don't need to be "attached" to an instance of the class
-   Static data is shared between all instances of a class
-   Remember the `static` keyword means something else outside of class definitions!

```c++
class static_example {
    private:
	static int a;
    public:
	static int getA() { return a; }
};
```


# Inheritance

-   Classes can inherit members from other classes

```c++
class child: public example {
    // we get `a` and `getA()` from example
    private:
	int b;
    public:
	int getB() { return b; }
	int getAplusB() { return getA() + b; } // we can't use `a` directly since it's private
};
```


# Polymorphism

-   Now we can create `child` objects with all the properties of an `example` object
-   This means we can safely cast a `child` object to an `example` object
    
    ```c++
    child c;
    example& e = dynamic_cast<example&>(c);
    ```
-   But not the other way around
    
    ```c++
    example e;
    child& c = dynamic_cast<child&>(e);
    ```
    
    ```
    example.cpp: In function ‘int main()’:
    example.cpp:20:38: error: cannot dynamic_cast ‘e’ (of type ‘class example’) to type
    ‘class child&’ (source type is not polymorphic)
         child& c = dynamic_cast<child&>(e);
    				     ^
    ```


# Virtual functions

-   A parent class can specify that certain functions are **virtual**
-   Child classes can then implement their own versions of the function
-   The child implementation will be called even from a reference of the type of the parent
    -   If the function isn't marked virtual, which implementation is called depends on the type of the reference


# Questions?

-   Ask here or on Piazza!