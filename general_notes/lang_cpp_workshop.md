# C++ 讀書會

## [2022/10/19] C++ Group Orientation

* Modern C++: C++11, C++14, C++17
  * Clean, fast, safe
  * Less easier to make error
  * > The are only two kinds of language:
    > the ones people complain abot and the ones nobody uses
  * Everything that needs performance can use C++
  * Power of C++: convert runtime error to compile time error
* Purpose: Enhance our coding skills
  * Usefull? It depends
* Concept of RAII
* Time scale
  * 1s  --> Desktop application: C#, Java
  * 1ms --> Most application: C++
  * 1us --> HFT (High Frequency Trading)
  * 1ns
* Comiler Support (三足鼎立)
  * GNU GCC
  * LLVM Clang
  * Microsoft Visual C++ (MSVC)
* Snopsys website: QSC
  * Add `-std=c++17` in `Master.make`
* Migration Stategy
  * Working efficiently with legacy code (book)
* [Compiler Explorer](godbolt.org)
  * Debugging message confused?
    * You can try differnt compiler and see other compiler message
  * Check how assembly works
  * Compare different ways of implmentation
* better use clangd --> Know it right away
* ToLearn:
  * CMake
  * Google Test

## [2022/10/26] Static Tools & IDE

### Tools

* Static Analysis Tools (靜態分析)
  * Clang-Tidy
  * CppCheck
  * Cloc --> 統計行數(評估 Code 規模)
* Runtme Tool
  * Valgring memcheck --> Check memeory leak
  * Sanitizers --> ASAN, TSAN, UBSAN check diffedent violations

### Clang-Tidy - [clang org](https://clang.llvm.org/extra/clang-tidy/)

* `source ~blazar/envscript/workflow/gcc-9.2.0.csh`
* Give good modern code suggestion
* 缺點：時間很久
* looks for `compile_commands.json`
* check `.clang-tidy`
* [ ] OOP vs FP vs DOD
  [CppCon 2019: Matt Godbolt “Path Tracing Three Ways: A Study of C++ Style” - YouTube](https://www.youtube.com/watch?v=HG6c4Kwbv4I)
* Optimization Level

### Profile Tools

Valgrind

* CPU-Bound
  * Valgrind: Callgrind
* Data-Bound
  * Valgring: Cachegrind
* IO/System Bound
  * Valgrind: Callgrind --collect-systime=yes


* clang: -ftime-trace + Chrome Tracing
  * url `chrome://tracing` in browser

### IDE

* QtCreator
* Visual Studio Community

## [2022/11/09] ChienHau Hung - Type deduction Trailing Return Type

### `Auto` keyword

* blazar: cpp allmost always auto
  * 等號右的資訊是一樣的資訊的時候，直接用 auto

Typed variable are deduced by the complier according to the type of their initialier

```cpp
auto a = 3.14;  // double
auto b = 1;     // int
auto& c = b;    // int&
auto d = { 0 }; // std::initializer_list<int>

auto (*p)()->int; // declares p as pointer to function int
auto (*q)()->auto = p; // Complex design

auto x = vector.begin() // vector<int>::iterator

// trailing return type
// very useful for template
template <typename X, typename Y>
auto add(X x, Y y) -> decltype(x+y) {
  return x+y;
}
```

### `Decltype` keyword 型別推導

Intended use is in generic programming (泛型)

Link:

* [C++ decltype（型別推導）精講](https://tw511.com/a/01/3084.html)

Examples:

```cpp
int a = 1;
decltype(a) b = a;

// special usage for keeping references and cv-qualified
decltype(auto) c = a;
```

In template

```cpp
tamplate <typename T>
class Base {
  public:
  void func(T& container) { m_it = container.begin() };

  private:
  decltype(T().begin()) m_it;
}
```

### `Decltype` and `Auto`

```cpp
// return type is int
auto f(const int& i) {
  return i*i;
}

// return type is const int&
decltype(i) f(const int& i) {
  return i*i;
}
```

Deduction rule: (Google by myself)

* `auto` deduction rule is same as `template` deduction rule
  * [cppreference: template argument deduction](https://en.cppreference.com/w/cpp/language/template_argument_deduction#Other_contexts)

### `typeid(variable).name()` Check type information

Example:

```cpp
int age = 18;
cout << typeid(age).name() << endl;
```

## [2022/11/09] Arvid Hsieh - Range-based For Scoped Enum Misc QoL Improvement

### Range-based for `for (auto &e:c)​`

和 For each 是一樣的事, 避免用多過多的其他東西 Loop

* array
* list
* vector
* std::string
* map (but with no index)
* anything ???

```cpp
int x[5] = {1, 3, 5, 7, 9}
for (auto y : x) {
  y *= 2; // cannot mutate y becaute type y is int, not &int
          // output still is {1, 3, 5, 7, 9}
  std::count << y << " (with type: " << type_name<decltype(y)>() << ")" << std::endl;
}

int x[5] = {1, 3, 5, 7, 9}
for (auto &y : x) {  // reference y --> Make it mutable
  y *= 2; // good!
          // {2, 6, 10, 14, 18}
}
```

### Scope Enumeration `enum class​`

[使用 enum class 取代傳統的 enum](https://kheresy.wordpress.com/2019/03/27/using-enum-class/)

#### emum

enum is not stronly typed, it it a int

```cpp
enum EColor {
  RED,
  GREEN,
  BLUE,
};

EColor eColor = RED;
```

#### enum class

```cpp
enum class EColor {
  RED,
  GREEN,
  BLUE,
};

EColor eColor = EColor::RED // auto = EColor::RED;
EColor userColor = static_cast<EColor>(number);
```

### Right angle brackets `T<T<>>​`

paper reference: [Daveed Vandevoorde](https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2005/n1757.html)

In c++98/03

```cpp
#include <vector>​
​
typedef std::vector<std::vector<int> > Table1;    // Okay​
typedef std::vector<std::vector<int>>  Table2;    // Error
```

C++11 Solved

### Binary Literal `0b101010​`

C99

```cpp
int h1 = 0xff; // Equal to 255​
int h2 = 0XA8; // Equal to 168​
​
int o1 = 0777; // Equal to 511
// 八進位 前面由 0 開始
```

After C++11

```cpp
int b1 = 0b101010; // Equal to 42​
int b2 = 0B000111; // Equal to 7

int b3 = 0B00'0111; // with digit separators
```

### Digit Separators `1'234'567​`

From C++14/17, add code readibility

```cpp
#include <iostream>​

int main () {​
    long long int d1 = 12'34'56;​
    long long int d2 = 1'23'45'6;​
    long long int d3 = 123'456;​

    std::cout << d1 << std::endl << d2 << std::endl << d3 << std::endl;​

    return 0;​
}
```

## RVALUE REFERENCE AND MOVE SEMANTICS - Yu-chun (2022/11/23)

### Rvalue reference

* lvalue vs rvalue
  * lvaule is the id that can point to a memory space
  * rvalue is not lvaue

* rvalue reference
  * `A& a_ref1 = a;` --> lvalue reference
  * `A&& a_ref2 = A()` --> rvalue reference
  * `&&` is called
  * `std::is_rvalue_reference<decltype(rref)>` chenck whether is rvalue reference
  * usage
    * Elimiating spurious copies
      Copy can be expensive (e.g. std::vector, std::list)
    * example `void push_back(T&& value);`
    * rvalue reference gets the ownership
    * 如果可以讓 Compiler 知道後面 ownership 不要用，可以直接用 move 取代 Copy
    * example

    ```cpp
    int main(){
      A a;
      foo(a);
      foo(A());  // temp object: rvalue
    }
    ```

* `std::move()` cast to rvalue

  > blazar: std::move() 沒有 move 任何東西

  * 只是轉型 (沒有 搬移/轉發 任何東西)，不產生任何程式碼。
    i.e. swap pointer
  * std::move 無條件轉型 – 成為 rvalue (稱 rvalue_cast 也許較貼切)
  * 通常造成搬移
  * 但來源若 const 則無法搬移
    * 經 std::move 後 const Foo 成為 const Foo&&
    * 參數 Foo&& f 無法接受 (不可放寬限制) → 無法搬移
    * 但 const Foo& f 可以接受 → 改以複製

* C++ values
  * Primare values
    * lvalue
    * prvalue -> "pure" rvalue
    * xvalue -> "eXpiring" value
  * Mixed values
    * glvalue -> "generalized" lvalue
    * rvalue
  * summary
    * glvalue = lvalue + xvalue
    * rvalue = prvalue + xvalue

  > blazar:
  > This will exists in template,
  > if you write applicatino you might not need this

## Move semantics - Yuchen (2022/11/23)

* Copy semantics vs move semantics
  * `void push_back(const T& elem);` C++03 copy
  * Added `void push_back(const T&& elem);` C++11 move
* `std::move(s)` --> s 之後都用不到了
* Usually implemented in
  * move constructor `v.push_back(std::move(s))`
  * move assignment operator `a = std::move(b)`

* yipingp: 有點像 C 語言
  雖然 p 還存在，但不擁有原本指向物件了

  ```c
  int *p = 5;
  int *q = p;
  p = nullptr;
  ```
