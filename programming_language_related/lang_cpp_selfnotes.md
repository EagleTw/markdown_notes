# [lang] Cpp ypprog notes

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

    ```C
    typedef struct {
      uint type;
      char name[32];
      float size;
    } MyStructType;

    /* how to get offset
       we can play polymorphism with this
    */
    offset = (uint)(&((MyStructType *)NULL)->size);
    ```

    1:15:21 <-- video to here

## Templates

Youtube - The Cherno - [Templates in C++](https://www.youtube.com/watch?v=I-hZkUa9mIs&t=4s)
cppreference - [Template](https://en.cppreference.com/w/cpp/language/templates)

Template is like generices(java), but more powerful.

In C we use overloading functions

```C
void print(int value) {
    print("%d\n", value);
}

void print(char *value) {
    print("%s\n", value);
}
```

Using templates

```Cpp
template<typename T>
void print(T *value) {
  cout << value << endl;
}
```
