```cpp
// include enum reflect header you wish to use (are split by compiler capabilities)
#include <cassert>
#include <iostream>

enum class A
{
  a,
  b,
  c
};

enum class B
{
  a = -3,
  b = -2,
  c = -1,
  d = 0,
  e = 1
};

int main(int argc, char* argv[])
{
  {
    assert((enum_reflect::value_exists<A, static_cast<A>(1)>() == true));
    assert((enum_reflect::value_exists<A, static_cast<A>(3)>() == false));

    assert((std::string(enum_reflect::name<A>(), enum_reflect::name_size<A>()) == "A"));
    assert((std::string(enum_reflect::value<A, A::a>(), enum_reflect::value_size<A, A::a>()) == "a"));
    assert((std::string(enum_reflect::value<A, A::b>(), enum_reflect::value_size<A, A::b>()) == "b"));
    assert((std::string(enum_reflect::value<A, A::c>(), enum_reflect::value_size<A, A::c>()) == "c"));

    assert((enum_reflect::from_string<A>("a", A::c) == A::a));
    assert((enum_reflect::from_string<A>("b", A::c) == A::b));
    assert((enum_reflect::from_string<A>("c", A::c) == A::c));

    assert((enum_reflect::from_string<A, A::a, A::c>("a", A::c) == A::a));
    assert((enum_reflect::from_string<A, A::a, A::c>("b", A::c) == A::b));
    assert((enum_reflect::from_string<A, A::a, A::c>("c", A::c) == A::c));

    assert((enum_reflect::from_string<A>("d", A::c) == A::c));
    assert((enum_reflect::from_string<A, A::a, A::c>("d", A::c) == A::c));

    std::vector<std::string> items;
    enum_reflect::stringify<A>(items);
    assert((items == std::vector<std::string>{"a", "b", "c"}));
  }


  {
    std::vector<std::string> items;
    enum_reflect::stringify<B, B::a, B::e>(items);
    assert((items == std::vector<std::string>{"a", "b", "c", "d", "e"}));
  }
}
```
