```cpp
// include enum reflect header you wish to use (are split by compiler capabilities)
#include <iostream>
#include <string>
#include <vector>

int main(int argc, char* argv[])
{
  std::cout << enum_reflect::value_exists<A, static_cast<A>(1)>() << '\n';
  std::cout << enum_reflect::value_exists<A, static_cast<A>(3)>() << '\n';

  std::cout << std::string(enum_reflect::name<A>(), enum_reflect::name_size<A>()) << '\n';
  std::cout << std::string(enum_reflect::value<A, A::a>(), enum_reflect::value_size<A, A::a>()) << '\n';
  std::cout << std::string(enum_reflect::value<A, A::b>(), enum_reflect::value_size<A, A::b>()) << '\n';
  std::cout << std::string(enum_reflect::value<A, A::c>(), enum_reflect::value_size<A, A::c>()) << '\n';

  std::cout << int(enum_reflect::from_string<A>("a", A::c)) << '\n';
  std::cout << int(enum_reflect::from_string<A>("b", A::c)) << '\n';
  std::cout << int(enum_reflect::from_string<A>("c", A::c)) << '\n';
  std::cout << int(enum_reflect::from_string<A>("d", A::c)) << '\n';

  std::vector<std::string> items;
  enum_reflect::stringify<A>(items);
  for (auto const& i : items)
    std::cout << i << ',';
  std::cout << '\n';

  return 0;
}
```
