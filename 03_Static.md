## Static

#### 1. Static Variables in a Function

- In a function, when a variable is declared as static, space for it gets allocated for the lifetime of the program. Even if the function is called multiple times, space for the static variable is allocated only once and the value of the variable in the previous call gets carried through the next function call.

- A static local variable is stored in the program's data segment, not on the stack. The memory for this variable is allocated only once when the program starts and is never deallocated until the program terminates.

- Because the memory address is fixed and the data is never deallocated, the value persists and can be accessed or modified by every subsequent function call.

```c++
void f()
{
    static int count=0;
    count++;
    cout<<count<<" ";
}
int main() {
    
    for(int i=0; i<5; i++)
        f();
    return 0;
}
```

``` Output
1 2 3 4 5
```

#### 2. Static data member in a class

- A static data member is not unique to the object of the class, it is shared by all the objects of the class.

- There is only one copy of a static data member, doesn't matter how many objects you create. All the objects of the class access and share this variable.

- Static data member belong to the class and can be accessed without creating object.

- They can be public, protected and private.

```c++
class Car{
    public:
    static int car_count;
    
    Car() {
        car_count++;
    }
};

int Car::car_count=0;

int main() {
    Car car1;
    Car car2;
    cout<<Car::car_count;
    return 0;
}
```

```output
2
```

#### 3. Static member function

- They also do not depend on the object of the class

- We are allowed to invoke a static member function using the object and the '.' operator but it is recommended to invoke the static members using the class name and the scope resolution operator.

- Static member functions are allowed to access only the static data members or other static member functions, they cannot access the non-static data members or member functions of the class. 

```c++
class Car{
    public:
        static void start() {cout<<"Car has started"; }
};
int main() {
    Car::start();
}
```

#### 4. Global Static Variable

- The global static variable has a global lifetime but a file scope. This means it is allocated once the program starts and persists until the program ends, but it can only be accessed from within the file in which it is declared.
 
-  This behavior is due to internal linkage. The compiler ensures that the name of a global static variable is not exported to the linker, so it cannot be linked to code in other files. Regular global variables have external linkage.

```c++
static int count = 0;

void increment() {
    count++;
    cout << count << " ";
}

int main() {
    increment();
    increment();
    return 0;
}
```

``` output
1 2
```

