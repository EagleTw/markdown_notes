
//************************************************* <br>
// Author:         ypprog                           <br>
// E-mail:         pan.yiping.fi@gmail.com          <br>
// Date:           2022-11-24                       <br>
// Description:                                     <br>
// Copyright 2022 by ypprog. All Rights Reserved    <br>
//************************************************* <br>

# Functional programming explained

Haskell Links
* [Haskell reference](http://zvon.org/other/haskell/Outputprelude/index.html)


## [Functional Programming 風格的 C 語言實作](https://hackmd.io/@sysprog/c-functional-programming)

Github Link
* [ypprog/Functional-Programming-in-C](https://github.com/ypprog/Functional-Programming-in-C)

[Why Functional Programming Matters](http://www.cs.kent.ac.uk/people/staff/dat/miranda/whyfp90.pdf) 是篇 1984 年的論文，在 1990 年做小幅度修改，主要凸顯出 FP 的優點與重要特質。
* 中文翻譯：[函數式程式設計為什麼至關重要](https://www.byvoid.com/zhs/blog/why-functional-programming)

Fuctional proramming 特點:

* 運算用的 function 大多只包含條件式及遞迴呼叫;
* [HOF (Higher-order fuctions)](https://en.wikipedia.org/wiki/Higher-order_function)特色
  * function 可當作參數傳入 function 之中
  * function 可以回傳 function
* No implicit [Side Effect](https://en.wikipedia.org/wiki/Side_effect_(computer_science)
* [lazy evaluation](https://en.wikipedia.org/wiki/Lazy_evaluation)

## Haskell 趣味指南

Link

* [Haskell 趣味指南](https://learnyouahaskell.mno2.org/)
* [英文版](http://learnyouahaskell.com/chapters)

Keywords to remember

* Chapter 3. Types and Typeclasses
  * Types: Int, Integer, Float, Double, Char, Bool
  * Type class: 可以支援不同 Type 的操作
    * `Eq`, `Ord`, `show`, `read` typeclasses
    * Bounded: `minBound`, `maxBound`
    * Num typeclass, Integral typeclass, Float typeclasses

* Chapter 4. Syntax in Functions
  * Pattern matching
  * Guards
  * Where
  * let
  * Case expression

* Chapter 5. Regression

* Chapter 6. Higher Order Functions
  * Curried functions
  * Maps and filter
  * Lambdas (Anonymous function)
    * `(\a -> a + 1) 4` answer is 5
  * `fold`
    * fold (+) [1,2,3,4,5] --> 15
    * Source code

      ```Haskell
      -- if the list is empty, the result is the initial value z; else
      -- apply f to the first element and the result of folding the rest
      foldr f z []     = z
      foldr f z (x:xs) = f x (foldr f z xs)

      -- if the list is empty, the result is the initial value; else
      -- we recurse immediately, making the new initial value the result
      -- of combining the old initial value with the first element.
      foldl f z []     = z
      foldl f z (x:xs) = foldl f (f z x) xs
      ```

  * `$` function (function application)

    ```Haskell
    ($) :: (a -> b) -> a -> b
    f $ x = f x
    ```

    * `$` 的優先順序則最低
    * `$` 則是右結合的 (用空格的函數呼叫符是左結合的，如 `f a b c` 與 `((f a) b) c` 等價)
