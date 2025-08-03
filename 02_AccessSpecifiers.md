## Access Specifiers

Access specifiers are used to assign the accessbility to the class members i.e. they set some restrictions on the class members so they can't be directly accessed by the outside functions. 

There are 3 types of access modifiers available in C++:

1. Public
2. Private (default)
3. Protected


#### 1. Public

- All the members declared under the public specifier will be available to everyone.

- The data members and member function declared as public can be accessed by other classes and functions too.

- The public members of a class can be accessed from anywhere in the program using the direct member access operator (.) with the object of that class

``` c++

class Circle {
    public:
        double radius;
        double area() {
            return 3.14*radius*radius;
        }
};

int main()
{
    Circle obj;
    obj.radius = 5.5;
    cout << "Radius is: " << obj.radius << "\n";
    cout << "Area is: " << obj.compute_area();
}
```

#### 2. Private Specifier

- The class members declared as private can be accessed only by the member functions inside the class. They are not allowed to be accessed directly by any object or function outside the class.

- Only the member functions or the friend functions/ friend class are allowed to access the private data members of the class.

``` c++
class Circle {    
private: 
    double radius;
    double  compute_area() {
        return 3.14*radius*radius;
    }
};

int main() {
    Circle obj;
    obj.radius = 1.5;  // trying to access private data member directly outside the class
    cout << "Area is:" << obj.compute_area();
}
```

#### How to access private members?

The standard way to access the private data members of a class is by using the public member functions of the class. The function that provides the access is called getter method and the function that updates the value is called the setter method. 

``` c++
class Circle {
    private: 
        double radius;
    public:
        double getRadius() {
            return radius;
        }
        void setRadius(double val) {
            radius = val;
        }
}
int main() {
    Circle obj;
    obj.setRadius(1.5);
    cout<<"Radius is "<<obj.getRadius()<<endl;
}
```

#### 3. Protected Specifier

- The protected access modifier is similar to the private access modifier in the sense that it can't be accessed outside of its class unless with the help of a friend class. 

- The difference is that the class members declared as Protected can be accessed by any subclass (derived class) of that class as well.

``` c++
class Parent {
    protected: 
        int pro_id;
};

class Child : public Parent {
    public:
        void setId(int id) {
            pro_id = id;
        }

        int getId() {
            return pro_id;
        }
};

int main() {
    Child obj1;
    obj1.setId(81);
    cout<<"ID : "<<obj1.getId();
}
```