# CPP Literals
## Predefined Literals

## User Defined Literals

### Concepts

* UDLs are just syntactic sugars
* It is based on operator loading
  * Example: `a+b` is syntatic sugar for `plus(a,b)`
* It is about readability

### Usefull User Define Literals

#### (1). Imaginary number UDLs

```cpp
using namespace std::literals::complex_literals;
auto x = 4if;           // complex<float>(0, 4.0)
auto x = 5.0 - 3.2i;    // complex<double>(5.0, -3.2)
```

#### (2). Crono duration UDL

```cpp
using namespace std::chrono::chrono_literals;
constexpr auto elapsed = 8min + 5.2s;
```

#### (3). Physical units

```cpp
using namespace si_literals;
auto d3  = 15.0_m   // idstance in meters
auto t3  = 4.0_s    // time in seconds
auto m   = 2045.0_g // mass expressed as g but stored in kg
auto mkg = 2.045_kg // mass express in kg
```

### Do you really need UDLs

* Make code more readible
* Comutation to compile time - faster code
* Overflow -> compile time error

* You need to handle overflow by yourself (REALLY?)

> ""<br>
> -Pablo Halpern

### Details for UDL

`operator"" _udl` defines a UDL suffix

4 Types

* Cooked UDL operator
* Raw UDL opearator
* Numeric UDL operator template
* String UDL operator tempalte

Priority 4 > 2 = 3 > 1

#### Type (1). Cooked UDL operator

Note:

* Check cooked UDL operator prototype
* cannot work for all type
* define mutiple types
* ALLWAYS consider this first!
* If overflows, compiler will throw error

#### Type (2). Raw UDL opearator

* only takes `const char*` as parameter
* for numeric UDLs only
* `T operator"" _udl(const char*);`
* Need to handle overflow and type problems by yourself
* Error might be in runtime

```cpp
Code Here
```

#### Type (3). Numeric UDL operator template

* for numeric UDLs only
* prototype`template <char... c> T operator"" _udl`

#### Type (4). String UDL operator tempalate (C++20 only)

* prototype `tempoate <StructType S> T operator"" _udl`

## Conclusion