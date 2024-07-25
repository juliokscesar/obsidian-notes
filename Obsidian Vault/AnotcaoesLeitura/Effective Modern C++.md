**Start**: 2024-07-01
**End**: ...

**Current page**: 30

## `rvalues` and `lvalues`
Generally, rvalues indicate objects eligible for move operations, while lvalues generally don't.
In concept (not always in practice) rvalues correspond to temporary objects returned from functions, while lvalues correspond to objects you can refer to, either by name or by following a pointer or lvalue reference.

A usefult heuristic way to determine whether an expression is an lvalue is to ask if you can take its address. If you can, it usually is. Otherwise, it's usually an rvalue.

Copies of rvalues are generally move constructed, while copies of lvalues are usually copy constructed.

# Deducting Types
C++98 had only type deduction for templates. C++11 then adds two more, `auto` and `decltype`. C++14 then extends the usage contexts in which `auto` and `decltype` may be used, and there is also `delctype(auto)`.

## Template type deduction
An example of pseudocode using function template:
```cpp
template <typename T>
void f(ParamType param);
[...]
f(expr); // call f with some expression
```
During compile time, compilers use `expr`to deduce one type for `T` and one for `ParamType`. *They are frequently not the same*. For example:
```cpp
template<typename T>
void f(const T& param); // ParamType is const T&
```
If we have a call such as:
```cpp
int x = 0;
f(x);
```
Then `T` is deduced to be `int`, but `ParamType` is deduced to be `const int&`.
It is expected that the type deducted for `T` is the same as the type of `expr` passed. But the type deduced for `T` is dependent not just on the type of `expr`, but also on the form of `ParamType`.

There are 3 main cases for the type deduction for `T` based on the form of `ParamType`.
### Case 1: `ParamType` is a reference or a pointer, but not a Universal Reference
Universal references will be explained later, but it is not the same as lvalue references or rvalue references.

In this case, if `expr`'s type is a reference, ignore the reference part. Then pattern-match `expr`'s type against `ParamType` to determine `T`.

For example:
```cpp
template<typename T>
void f(T& param); // param is a reference

[...]

int x = 27;        // x is an int
const int cx = x;  // cx is a const int
const int& rx = x; // rx is a reference to x as a const int

f(x);  // T is int, param's type is int&
f(cx); // T is const int, param's type is const int&
f(rx); // T is const int, param's type is const int&
```
In the second and third calls, `cx` and `rx` designate `const int` values, so `T`is deduced to be `const int`, yielding a parameter of type `const int&`.
These examples work the same way for deducing rvalue reference parameters.

This is how it would change if `param` was changed to a ref-to-const:
```cpp
template<typename T>
void f(const T& param); // param is now ref-to-const

[...]

f(x);   // T is int, param's type is const int&
f(cx);  // T is int, param's type is const int&
f(rx);  // T is int, param's type is const int&
```
Things would work essentially the same way if `param` was a pointer.

### Case 2: `ParamType` is a Universal Reference
Such Universal Reference parameters are declared like rvalue references (`T&&`).
- If `expr` is an lvalue, both `T`and `ParamType` are deduced to be lvalue references.
- If `expr` is an rvalue, the normal (case 1) rules apply.

For example:
```cpp
template<typename T>
void f(T&& param);  // param is now a universal reference

[...]

int x = 27;
const int cx = x;
const int& rx = x;

f(x);  // x is lvalue, so T is int&. param's type is also int&.
f(cx); // cx is lvalue, so T is const int&. param's type is also const int&
f(rx); // rx is lvalue, so T is const int&. param's type is also const int&
f(27); // 27 is rvalue, so T is int. param's type is int&&.
```

### Case 3: `ParamType` is neither a pointer nor a reference
In this case we're dealing with pass-by-value:
```cpp
template<typename T>
void f(T param); // param is now passed by value
```
That means that `param` will be a copy of whatever is passed in (a completely new object).
- If `expr`'s type is a reference, ignore the reference type.
- If, after ignoring `expr` reference-ness, `expr` is const, ignore that too. If it's volatile, ignore that.
For example:
```cpp
int x = 27;
const int cx = x;
const int& rx = x;

f(x);  // T's and param's types are both int
f(cx); // T's and param's types are again both int
f(rx); // T's and param's types are still both int
```

In the case of array values, when passing it as argument the array decays to a pointer to its first elements, so if the array is passed by value, then `T` is deduced to be a pointer.
But, if `param` is a reference (`T&`) and we pass an array, then the type deduced for `T`is the actual type of the array, including the size of the array.
For example:
```cpp
template<typename T>
void f(T& param);

const char name[] = "Julio Cesar" // name's type is const char[12]

f(name); // T is deduced to be const char[12], and param's is const char(&)[12]
```

The same thing would happen if we were to pass a function. That is, if the type specifier was simply `T`, then the function would decay into a pointer and `T` is deduced to be a pointer. If the type specifier was `T&`, then `T` would be a ref-to-func.

# `auto` type deduction
`auto` type deduction is basically the same as for template type deduction (with only one exception). Although template deduction involves templates and functions and parameters, while `auto` doesn't, there is a direct mapping between template type deduction and `auto` type deduction.
There is literally an algorithmic transformation from one to the other.

When a variable is declared using `auto`, `auto` plays the role of T in the template, and the type specifier for the variable acts as `ParamType`.
For example
```cpp
auto x = 27; // T would be auto and ParamType would be auto as well
const auto cx = x; // T would be auto and ParamType would be const auto 
const auto& rx = x; // T would be auto and ParamType would be const auto&
```
In these examples, compilers act as if there were a template for each declaration as well as a call to that template with the corresponding expression.

The same cases in template type deduction work here too:
- Case 1: the type specifier is a pointer or reference, but not a universal reference
- Case 2: the type specifier is a universal reference
- Case 3: the type specifier is neither a pointer nor a reference

Examples:
```cpp
auto x = 27; // case 3 (x is int and is assigned a copy of 27)
const auto cx = x; // case 3 (cx is a const int and it's value is a copy of x)
const auto& rx = x; // case 1 (rx is a const int&)

// Cases of case 2
auto&& uref1 = x; // x is int and lvalue, so uref1's type is int&
auto&& uref2 = cx; // cx is const int and lvalue, so uref2's type is const int&
auto&& uref3 = 27; // 27 is int and rvalue, so uref3's type is int&&
```

The same thing that happens with array and function in template type deduction happens here too:
```cpp
const char name[] = "Julio Cesar"; // name is const char[12]

auto arr1 = name; // arr1's type is const char*
auto& arr2 = name; // arr2's type is const char(&)[12]

void someFunc(int, double); // someFunc is a function with type void(int, double)

auto f1 = someFunc; // f1's type is void(*)(int, double)
auto& f2 = someFunc; // f2's type is void(&)(int, double)
```

The only exception for `auto` is regarding uniform initialization (with `{}`), such as:
```cpp
int x1 = 27;
int x2(27);
int x3 = {27};
int x4{27};
```
all of these get the same result: `int` with value 27.
But using `auto` can change `x3` type:
```cpp
auto x1 = 27; // x1 is int
auto x2(27); // x2 is int
auto x3 = {27}; // x3 is deduced to be std::initializer_list<int>
auto x4{27}; // x4 is int
```

The treatment of braced initializers is the only way in which `auto` type deduction differs from template type deduction.
That is the full story for C++11.

C++14 permits `auto` to indicate that a function's return type should be deduced, and C++14 lambdas may use `auto` in parameter declarations. However, these uses of `auto` employ template type deduction, not `auto` type deduction.

# Understand `decltype`
Given a name or an expression, `decltype` tells you the name's or expression's type. Examples:
```cpp
const int i = 0; // decltype(i) is const int

bool f(const Widget& w); // decltype(w) is const Widget&, decltype(f) is bool(const Widget&)

struct Point {
	int x, y;  // decltype(Point::x) is int, decltype(Point::y) is int
};

if (f(w))... // decltype(f(w)) is bool
...
```

In C++11, perhaps the primary use for `decltype` is declaring function templates where the function's return type depends on its parameters types.

For example, a function that takes a container that supports indexing via [] plus an index, then authenticates the user before returning the result of the indexing operation. The return type should be the same as the type returned by the indexing operation.
`operator[]` on a container of objects of type `T` typically returns a `T&`. For `std::vector<bool>`, however, `operator[]` does not return a `bool&`, it returns a brand new object. That is, the type returned by a container's `operator[]` depends on the container.
Here's an example of the template for this function showing the use of `decltype` to compute the return type:
```cpp
template<typename Container, typename Index>
auto authAndAccess(Container& c, Index i) -> decltype(c[i])
{
	authenticateUser();
	return c[i];
}
```
Since it's C++11, the use of `auto` before the function name has nothing to do with type deduction. Rather, it indicates that C++11's *trailing return type* syntax is being used, that is, the function's return type will be declared after the parameter list (after the "->"). A trailing return type has the advantage that the function's parameters can be used in the specification of the return type (we use the parameters `c` and `i` to specify the return type, even though they were declared later).
With this declaration, `authAndAccess` returns whatever type `operator[]` returns.

In C++14 we can use `auto` as function return types without trailing return type:
```cpp
template<typename Container, typename Index>
auto authAndAccess(Container& c, Index i)
{
	authenticateUser();
	return c[i]; // return type deduced from c[i]
}
```
BUT this wouldn't work as expected. We would expect this function to return a reference to type type of `c[i]` (e.g. `int&`), but, because `auto` strips off the the reference, it would return a copy of the value of `c[i]` (e.g. simply `int`) so trying to assign it such as:
```cpp
std::vector<int> v;
authAndAccess(v, 5) = 10;
```
Won't compile, because `authAndAccess` will return an `int` that's a copy of the value of `v[5]`, so it will return a rvalue rather than the expected lvalue reference.

To get it to work as expected, we need to use `decltype` deduction so that we specify that `authAndAccess` should return exactly the same type the expression `c[i]` returns:
```cpp
template<typename Container, typename Index>
decltype(auto)
auto authAndAccess(Container& c, Index i)
{
	authenticateUser();
	return c[i];
}
```
`auto` specifies that the type is to be deduced, and `decltype` says that `decltype` rules should be used during the deduction.

The same works for declaring variables:
```cpp
Widget w;
const Widget& cw = w;

auto myWidget1 = cw; // myWidget1's type is Widget (copy of w)
decltype(auto) myWidget2 = cw; // myWidget2's type is const Widget&
```

Summary: applying `decltype` to a name yields the declared type for that name.

