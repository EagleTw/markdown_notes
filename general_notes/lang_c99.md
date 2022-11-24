# C99

## Links

* ISO/IEC 9899
  * C11 [(ISO/IEC 9899:201x)](https://www.open-std.org/jtc1/sc22/WG14/www/docs/n1570.pdf) / [網頁版](http://port70.net/~nsz/c/c11/n1570.html)
* [你所不知道的 C 語言](https://hackmd.io/@sysprog/c-prog/%2F%40sysprog%2Fc-programming)

## Types

C99 Link - [(6.2.5 Types)](http://port70.net/~nsz/c/c11/n1570.html#6.2.5)

基本分類：

* Scalar types
  > 注意 "scalar type" 這個術語，日後我們看到 ++, --, +=, -= 等操作，都是對 scalar (純量)
  * Pointer types (reference type)
    > A pointer type may be derived from a function type, an object type, or an incomplete type, called the referenced type. A pointer type describes an object whose value provides a reference to an entity of the referenced type. A pointer type derived from the referenced type T is sometimes called "pointer to T". The construction of a pointer type from a referenced type is called "pointer type derivation".
  * Arithmetic types
    * Real
      * Bool: `_Bool`
      * Character type: `char`, `signed char`, `unsigned char`
      * Integer
        * Signed integer: `signed char`, `short int`, `int`, `long int`, `long long int`
          (check INT_MIN to INT_MAX as defined in the header `<limits.h>`)
        * Unsigned integer
      * Real floating: `float`, `double`, `long double`
    * Complex: `_Complex`, `double _Complex`, `long double _Complex`
  * enumeration
* Aggregate types
  * Array type
    > An array type of unknown size is an incomplete type. It is completed, for an identifier of that type, by specifying the size in a later declaration (with internal or external linkage). A structure or union type of unknown content (as described in 6.7.2.3) is an incomplete type. It is completed, for all declarations of that type, by declaring the same structure or union tag with its defining content later in the same scope.
  * structure types

另一種分類：

* **derived declarator types**：array, function, and pointer types
  > Array, function, and pointer types are collectively called derived declarator types. A declarator type derivation from a type T is the construction of a derived declarator type from T by the application of an array-type, a function-type, or a pointer-type derivation to T.

## lvalue (locator value)

C99 Link - [6.3.2.1 Lvalues, arrays, and function designators](http://port70.net/~nsz/c/c11/n1570.html#6.3.2.1)
Youtube - [lvalues and rvalues | C Programming Tutorial](https://www.youtube.com/watch?v=Ha-v53xIYXc)
[Understanding lvalues and rvalues in C and C++](https://eli.thegreenplace.net/2011/12/15/understanding-lvalues-and-rvalues-in-c-and-c)

* Definition: An lvalue is an expression (with an object type other than void) that potentially designates an object
* Any value is not lvalue is rvalue.

```C
int i = 20; /* i  --> modifialbe lvalue */
            /* 20 --> rvalue */

20 = i      /* ERROR! */
(i + 1) = i /* ERROR! */

const int j = 10;
j = 20;     /* Error: assignment of read-only variable */
```

Conversions between lvalues and rvalues

```C
int a = 1;     /* a is an lvalue */
int b = 2;     /* b is an lvalue */
int c = a + b; /* + needs rvalues, so a and b are converted to rvalues */
               /* and an rvalue is returned */
```

## Useful keywords

* `const` the value should not change
  In rust, all varialbe are default const
