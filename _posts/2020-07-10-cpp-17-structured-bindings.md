---
title: '[C++: 17] Using structured binding to unpack the returns values'
published: true
---  
  
## Intro

This note about new C++ 17 feature - Structured Bindings.

## Let's write some code

For example, We have the follow function:

```cpp
std::pair<unsigned int, unsigned int> increment_by_1(unsigned int x, unsigned int y)
{
    return {++x, ++y};
}
```

Before C++ 17, to unpack the returned values can be done in following way: 

```cpp
int main(void)
{
    unsigned int x = 5, y = 8;

    auto result = increment_by_1(x, y);
    std::cout << "x = " << result.first << " | y = " << result.second;

    return 0;
}
```

Here `result` is a `std::pair`.  
The C++ 17 allow us to make the code more readable:

```cpp
int main(void)
{
    unsigned int x = 5, y = 8;

    const auto [incremented_x, incremented_y] = increment_by_1(x, y);
    std::cout << "incremented_x = " << incremented_x << " | incremented_y = " << incremented_y;

    return 0;
}
```

Note: Because in this example We use feature of C++ 17 so the example need to be compile with `-std=c++17` flag.

`g++ -std=c++17 -Wall -Werror -Wpedantic stuctured_binding.cpp`  

Also, structured bindings can be applyed to the `std::tuple`  
Assume there is the function:

```cpp
std::tuple<std::string, unsigned int> name_and_id(void)
{
    return {"Phil", 99};
}
```  

Using in the same way:  

```cpp
const auto [name, id] = name_and_id();
```  

## What about the user-defined data?  

Structured binding may be applied to the user-defined data.  

```cpp
struct human
{
    std::string name;
    unsigned int age;
};

int main(void)
{
    std::vector<human> humans = {
        {"Bob", 33},
        {"Phill", 22},
        {"Sam", 40}};

    for (const auto &[name, age] : humans)
    {
        std::cout << "name = " << name << " | age = " << age << "\n";
    }
}
```  

## Conclusion  

Structured binding is a very useful feature. This one makes the code more readable.
