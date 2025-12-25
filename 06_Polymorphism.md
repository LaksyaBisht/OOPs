## Polymorphism

Polymorphism is a core concept in object-oriented programming that means "many forms." It allows a single entity, such as a variable, a method, or an object, to take on different forms or have different behaviors in various contexts.


#### Function Overloading

C++ function overloading allows you to define multiple functions with the same name but different parameters. It is a form of compile time polymorphism in which a function can perform different jobs based on the different parameters passed to it.

#### Different Ways of Function Overloading

A function in C++ can be overloaded in three different ways:

1. By having different number of parameters.
2. By having different types of parameters.
3. By having both different number and types of parameters.


```c++
class Overload{
    public:
    int a;
    double b, c;
    
    int add(int a, double b)
    {
        return a+b;
    }
    
    double add(int a, double b, double c)
    {
        return a+b+c;
    }
};

int main()
{
    Overload obj;
    cout<<obj.add(5, 5.0);
    cout<<endl<<obj.add(5, 5.1, 10.2);
}
```

```output
10
20.3
```



#### Operator Overloading

C++ has the ability to provide the operators with a special meaning for a data type, this ability is known as operator overloading. Operator overloading is a compile-time polymorphism. For example, we can overload an operator '+' in a class like String so that we can concatenate two strings by just using +.


```c++
class Complex {
    private:
        int real, img;
    public:
        Complex(int r=0, int i=0)
        {
            real = r;
            img = i;
        }
        
        Complex operator+(Complex const& ob)
        {
            Complex res;
            res.real = real + ob.real;
            res.img = img + ob.img;
            return res;
        }
        
        void print()
        {
            cout << real << " + i" << img << '\n';        
        }
};

int main()
{
    Complex obj1(2, 6);
    Complex obj2(6, 3);
    Complex obj = obj1 + obj2;
    obj.print();
}
```


The Complex operator+(Complex const& ob) function is called when the + operator is used with a Complex object on its left side.

1. **Object Invoking the Function**: The Complex object on the left side of the + operator (e.g., obj1 in obj1 + obj2) is the object that calls this member function. Its private members, real and img, are directly accessible within the function.

2. **Parameter ob**: The Complex object on the right side of the + operator (e.g., obj2 in obj1 + obj2) is passed as a constant reference parameter named ob. This is efficient because it avoids making a copy of the object, and the const keyword ensures the original object isn't modified.

3. **Calculation**: A new Complex object, res, is created to store the result. The function then calculates the sum by adding the real and img components of the two Complex objects:

    - res.real = real + ob.real; (adds the real parts)
    - res.img = img + ob.img; (adds the imaginary parts)

4. **Return Value**: The function returns the resulting Complex object, res, by value. This returned object can then be used in the rest of the expression, as seen in Complex obj = obj1 + obj2;.



#### Some operators can't be overloaded in C++ to maintain the language's fundamental integrity and prevent ambiguity. Here's a quick summary of the operators you cannot overload:

- Scope Resolution Operator (::): This is used to specify a namespace or class scope. Overloading it would confuse the compiler's ability to resolve names.

- Member Access Operators (. and .*): These are for accessing members of a class. Allowing them to be overloaded could lead to unpredictable behavior and make the code difficult to understand. The compiler needs to know exactly how to access a member.

- Conditional Operator (?:): This is a ternary operator that requires three operands and has a very specific structure. Overloading it would break its unique syntax and purpose.

- sizeof: This is a compile-time operator that returns the size of a type or object. It's a fundamental part of the language and its behavior cannot be changed.

- typeid: This operator returns a std::type_info object about an expression. Like sizeof, it's a built-in feature of the language that's not meant to be modified.

- const_cast, static_cast, dynamic_cast, reinterpret_cast: These are the C++ casting operators. They serve specific, non-negotiable roles in type conversion and cannot be overloaded.




#### Function Overriding

Function overriding is a type of polymorphism in which we redefine the member function of a class which it inherited from its base class. The function signature remains same but the working of the function is altered to meet the needs of the derived class.

Function overriding is performed at the runtime, which means that function call will be binded to its definition during runtime (also known as late binding or dynamic binding). This can be done with the help of virtual functions.

The override keyword is a specifier that you place after the function signature in a derived class. It tells the compiler two things:

- This function is intended to override a virtual function from a base class.

- If it doesn't actually override a function (for example, due to a typo in the name, wrong parameters, or if the base class function isn't virtual), the compiler will generate a compile-time error.


```c++ 
class Base {
    public:
    virtual void display()
    {
        cout<<"Base class member function"<<endl;
    }
};

class Derived : public Base {
    public:
    void display() override {
        cout<<"Derived class member function"<<endl;
    }
};

int main()
{
  Base basept;
  basept.display();  //Base class member function
  Derived derivedObj;
  Base* baseptr = &derivedObj;  //Derived class member function
  baseptr -> display();
}
```
