# Cpp ISO/IEC 14882:2017

## 5.13 Literals

- Built-in
  - integer-literal (5.13.2)
    - integer-literal
    - binary-literal (base 2) `0b0000'0100 --> 8`
    - octal-literal (base 8) `010`
    - decimal-literal (base 10) `0x10 --> 16`
    - hexadecimal-literal (base 16)
    - binaray-digits
  - character-literal (5.13.3)
  - floating-literal (5.13.4) `1e+6f`
  - string-literal (5.13.5)
  - boolean-literal (5.13.6) `true`, `false`
  - pointer-literal (5.13.7) `nullptr`
- user-defined-literal

Example

```Cpp
int d = 42;
int o = 052;
int x = 0x2a;
int X = 0X2A;
int b = 0b101010;
int B = 0B101010;

// the use of '
unsigned long long l2 = 18'446'744'073'709'550'592llu; // C++14
```
