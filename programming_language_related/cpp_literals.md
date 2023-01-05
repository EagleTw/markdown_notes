# CPP Literals

## Predefined Literals

## User Defined Literals

### Concepts

* UDLs are just syntactic sugars
* It is based on operator overloading
  * Example: `a+b` is syntatic sugar for `plus(a,b)`
* It is about readability



### Why you need UDLs

* Make code more readible

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

(This is the only thing you really need)

#### Type (1). Cooked UDL operator

```cpp
Type operator"" _udl (Type Value)
T operator"" _udl(const char*);
```

```cpp
constexpr int operator"" _m (long double value)
{
	return value * 100;
}

auto distance_in_cm = 3.2_m;   // 320

```

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

```
'
```

```cpp
int operator"" _base3eval(const char* digits) {
    int result = 0;

    while (*digits) {
        result *= 3;
        result += *digits - '0';
        ++digits;
    }

    return result;
}
```

```cpp
auto n1 = 21_base3eval;    // OK, return (int)7
auto n2 = 23_base3eval;    // Bug, return (int)9
auto n3 = 21.1_base3eval;  // Bug, returns (int)58
auto n4 = 2111111111111111111111_base3eval // Bug, overflow
```

```cpp
int operator"" _base3eval(const char* digits) {
    int result = 0;

    while (*digits) {
        if ('\'' == *digits) continue;

        if (*digits < '0' || *digits > '2')
            throw std::out_of_range("Invalid base-3 digit");
        // if overflow ...
        // if is a floating point ...

        result *= 3;
        result += *digits - '0';
        ++digits;
    }

    return result;
}
```

#### Type (3). Numeric UDL operator template

* for numeric UDLs only
* prototype`template <char... c> T operator"" _udl`

#### Type (4). String UDL operator tempalate (C++20 only)

* prototype `tempoate 

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

## Conclusion