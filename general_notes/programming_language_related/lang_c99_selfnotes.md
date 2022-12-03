# [lang] c99 ypporg notes

## Tips from Eskil Steenberg

YouTube - Eskil Steenberg - [How I program C](https://www.youtube.com/watch?v=443UNeGrFoM)

* Ambiguity is the enimy
  * Readibility is more important
  * It takes most of time reading code than implementing
  * operator overloading is evil
  * do not hide stuff

* Crashes are good
  make you fix things faster

* Naming
  * fuctions `my_function()`
    For better search `object_...`, 
    just like search assignment `a = ...` or `a == ...`

    ```c
    // not preferred
    create_object(); 
    edit_object();

    // good
    object_create();
    object_edit();

    // best!
    module_object_create();
    module_object_edit();
    ```

  * types `MyTypes`
  * variable `my_variable`
  * Define words

    ```C
    array
    type
    node
    entity
    handle
    func
    internal

    i, j, k, /* integers */
    f        /* floats */
    count, length, found
    next, previous, array, list,
    ```

* Long functions are good
  * a little controvertial, but I think this way too.
  * Alert names: `manager`, `controller`, `handler`, this means the code here is not directly do with datas

* API Design
  * Start from outside to inside

* Object orientation in C
  * Code and data are stored in different parts (most oop language user does not know that)
  * In C

    ```C
    thing = object_create();
    object_do_something(thing);
    ```

* Macro are general bad
  * You won't have any debug message
  * only reason to use macros

    ```C
    __FILE__  /* String with file name */
    __LINE__  /* int with line number */

    f_debug_mem_print(uint abc, __FILE__, __LINE__)
    ```

* Memory & pointers
  * is like house and address
  * Pointer have types
    We need to know how big is the house

    ```C
    void *p; /* p is an untyped pointer */

    short *short_pointer = p;
    int *int_pointer = p;

    a = *short_pointer; /* read 2 bytes as a short */
    b = *int_pointer;   /* read 4 bytes as a int */

    short_pointer++;    /* add 2 bytes --> sizeof(short) */
    int_pointer++;      /* add 4 bytes --> sizeof(int) */
    ```

  * malloc

    ```C
    double *a;

    a = malloc(sizeof(double));    /* most people */
    a = malloc((sizeof *a));      /* recommended */

    /* because if we change type of a from double to float
       hmmm...
    */
    ```

  * Arrays with pointers
    Using pointers as counters

    ```C
    uint i;
    /* slow */
    for (i = 0; i < 10; i++) {
      p[i] = 0;
    }

    /* faster */
    void *end;
    for(end = &p[10]; p != end; p++) {
      *p = 0;
    }
    ```

  * Structs are just a sizeof and a bunch of offset types
    * Remember padding in structure!!
    * Beware of the size of structure

    ```C
    typedef struct {
      uint type;      /*  1 byte */
      char name[32];  /* 32 byte */
      float size;     /*  4 bute */
    } MyStructType;

    /* how to get offset
       we can play polymorphism with this
    */
    offset = (uint)(&((MyStructType *)NULL)->size);
    ```

  * `realloc()` is awsome!!!
    * C-string

  1:32:54 <-- video to here

## Fuction pointers

Example

```C
int sum(int a, int b) {
  return a + b;
}

int main() {
  int (*ptr)(int, int) = &sum;
  result = *ptr(10, 20);
  printf("%d", result);
  return 0;
}
```

Why are function pointers useful? - [[link]](https://www.youtube.com/watch?v=ewBBRaF0oEA)

```C
#include <stdio.h>

int sum(int a, int b) {
  return a + b;
}

int prod(int a, int b) {
  return a * b;
}

int wrapperFunction(int (*operation)(int, int)) {
  int a = 10;
  int b = 20;
  printf("The result of the operation between %d and %d is %d\n",
          a, b, operation(a, b));
}

int main() {
  wrapperFunction(&sum);
  wrapperFunction(&prod);
}
```
