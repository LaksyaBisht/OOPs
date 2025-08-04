## Destructors

Destructor is an instance member function that is invoked automatically whenever an object is going to be destroyed

#### Characteristics of a Destructor
All the points mentioned below show the characteristics of a destructor:

- Destructor has the same name as their class name preceded by a tilde (~) symbol.

- It is not possible to define more than one destructor.

- The destructor is only one way to destroy the object created by the constructor. Hence, destructor cannot be overloaded.

- It cannot be declared static or const.

- Destructor neither requires any argument nor returns any value.

- It is automatically called when an object goes out of scope. 

- Destructor release memory space occupied by the objects created by the constructor.

- In destructor, objects are destroyed in the reverse of an object creation.


#### When is the destructor called?

A destructor function is called automatically when the object goes out of scope or is deleted. Following are the cases where destructor is called:

- Destructor is called when the function ends.
- Destructor is called when the program ends.
- Destructor is called when a block containing local variables ends.
- Destructor is called when a delete operator is called.


#### Private Destructors

Destructors with the access modifier as private are known as Private Destructors.

#### What is the use of private destructor?

Whenever we want to control the destruction of objects of a class, we make the destructor private.

When you declare a destructor as private, the compiler enforces access control.

- **Stack Objects**: The compiler needs to call the destructor at the end of the object's scope. Since the destructor is private, this call fails, leading to a compile-time error.

```c++
class Test {
private:
    ~Test() {}
};
int main() { Test t; }
```

```error
The above program fails in the compilation. The compiler notices that the local variable 't' cannot be destructed because the destructor is private.
```

- **Heap Objects**: Creating a heap object with new is fine, as new doesn't call the destructor. However, trying to call delete on the object's pointer from outside the class will also result in a compile-time error, as delete implicitly calls the destructor.

```c++
class Test {
private:
    ~Test() {}
};

int main()
{
    Test* t = new Test;
    delete t;
}
```

```error
The above program fails in the compilation. When we call delete, destructor is called. 
```

- The only way to delete an object with a private destructor is by having a public static or friend function that has access to the destructor.

```c++
class Test {
private:
    ~Test() {}

public:
    friend void destructTest(Test*);
};

void destructTest(Test* ptr) { delete ptr; }

int main()
{
    Test* ptr = new Test;

    destructTest(ptr);

    return 0;
}
```


#### Virtual Destructor

A virtual destructor is a destructor declared with the virtual keyword in a base class. Its main purpose is to ensure that when a derived class object is deleted through a base class pointer, the correct destructor (i.e., the derived class's destructor) is called first, followed by the base class's destructor.

By making the base class destructor virtual, you enable polymorphic destruction. This means the program will correctly identify the actual type of the object being pointed to and call the appropriate destructor chain, starting from the most derived class and moving up the hierarchy.

```c++
class Base {
public:
    virtual ~Base() { 
        std::cout << "Base destructor called" << std::endl;
    }
};

class Derived : public Base {
private:
    int* data;
public:
    Derived() {
        data = new int[10];
    }
    ~Derived() {
        delete[] data;
        std::cout << "Derived destructor called" << std::endl;
    }
};

int main() {
    Base* ptr = new Derived();
    delete ptr; 
    return 0;
}
```

```Output
Derived destructor called
Base destructor called
```

Making a destructor virtual in a base class automatically makes it virtual in all derived classes. You don't need to use the virtual keyword again in the derived classes.


#### Pure Virtual Destructor

- A pure virtual destructor is a destructor declared as a pure virtual function in a base class using the = 0 syntax. While it's declared as pure, it must also have an implementation because the destructors of the derived classes will automatically call the base class's destructor. It's used to make a base class abstract while ensuring that derived class objects can be properly destroyed.

- The main purpose of a pure virtual destructor is to make a base class non-instantiable (abstract) when it doesn't have any other pure virtual functions. This enforces that any class inheriting from it must be a concrete class that can be instantiated.

- If a class has a pure virtual function, it becomes an abstract class, which means you cannot create objects of that class directly. By making the destructor pure virtual, you achieve the same result. The key is that even though it's pure, it still needs to be defined.

- The implementation must be provided outside the class definition, in the source file. If you forget to provide a definition, the linker will throw an error when it tries to link the derived class's destructor, which will implicitly call the base class's pure virtual destructor.

```c++
#include <iostream>

class Base {
public:
    // Pure virtual destructor
    virtual ~Base() = 0;
};

Base::~Base() {
    std::cout << "Base destructor called" << std::endl;
}

class Derived : public Base {
public:
    ~Derived() {
        std::cout << "Derived destructor called" << std::endl;
    }
};

int main() {
    // This line would cause a compile-time error
    // Base b; 

    Base* b_ptr = new Derived(); 
    delete b_ptr;
}
```

In this example, Base is an abstract class because its destructor is pure virtual. The delete b_ptr call correctly invokes the destructor chain: Derived's destructor is called, followed by Base's pure virtual destructor, which is why it must have an implementation.


#### Why only one destructor?

The primary reason is that a destructor's purpose is to clean up resources, and this process is always the same regardless of how the object was created. A destructor doesn't take any parameters, so there's no way for the compiler to differentiate between multiple destructors.



