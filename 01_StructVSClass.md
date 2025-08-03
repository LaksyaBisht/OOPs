## Struct vs Class

- members of struct are public by default and members of the class are public by default.

- class is normally used for data abstraction and inheritance and struct is used for grouping of different datatypes.

``` c++
class Test1 {
    int a;
};

struct Test2 {
    int b;
};

int main()
{
    Test1 t1;
    Test2 t2;

    // cout<<t1.a;  Private within this context  
    cout<<t2.b;
}
```

### When to choose struct over class

The C++ Standard Library and most experienced developers follow a common convention: use struct for simple data aggregates.
Consider a struct when:

- You are creating a Plain Old Data (POD) type. These are types with no user-defined constructors, destructors, virtual functions, or private members. They are easily copied and manipulated.

- The members should all be public.

- The struct contains only data, with perhaps a few simple helper functions to operate on that data.

- The intent is to pass a simple value-like object.

- struct is ideal for bundling together a small number of related variables into a single unit, particularly when that unit represents a Plain Old Data (POD) type.

Example: A point in 2d space

``` c++
struct Point {
    double x;
    double y;
}
```

#### Why a struct works here:

- **Simple data aggregate:** Point is just a bundle of two coordinates.

- **Public members:** There's no need to hide the x and y values. You want to access them directly, for example, to get the coordinates of a mouse click: Point click_pos = getMouseClick(); std::cout << click_pos.x;.

- **No complex logic:** A Point doesn't need to protect its state or perform complex calculations to maintain integrity.

