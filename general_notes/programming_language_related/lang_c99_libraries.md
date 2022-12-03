# [lang] C99 Libraries 筆記

## `string.h` C-String

`#include <string.h>`
[Source Code](https://code.woboq.org/gtk/include/string.h.html)

### `strlen()` Get lengh of str

* size_t strlen(const char *s)
* `strlen()` vs `sizeof()`
  * `strlen()` --> function by string.h (Find '\0')
  * `sizeof()` --> operator

### String Copy

* `strcpy` 將字串 s2 拷貝到 `s1	char *strcpy(char *s1, const char *s2);`
* `strncpy`	將字串 s2 最多 n 個字元拷貝到 `s1	char *strncpy(char *s1, const char *s2, size_t n);`

### String cat 字串相接

* `strcat` 將字串 s2 接到 s1 的尾端	`char *strcat(char *s1, const char *s2);`
* `strncat`	將字串 s2 最多 n 個字元接到 s1 的尾端	`char *strncat(char *s1, const char *s2, size_t);`

### String Compare

* `strcmp`	比較 s1 與 s2 兩個字串是否相等 `int strcmp(const char *s1, const char *s2);`
* `strncmp`	比較 s1 與 s2 兩個字串前 n 個字元是否相等	`int strncmp(const char *s1, const char *s2, size_t n);`

### String search

* `strchr` 回傳在字串 s 中，字元 c 第一次出現位置的指標	`char *strchr(const char *s, int c);`
* `strcspn` 計算經過幾個字元會在字串 s1 中遇到屬於 s2 中的字元	`size_t strcspn(const char *s1, const char *s2);`
* `strspn` 計算經過幾個字元會在字串 s1 中遇到不屬於 s2 中的字元	`size_t strspn(const char *s1, const char *s2);`
* `strpbrk` 回傳在字串 s2 中的任何字元在 s1 第一次出現位置的指標	`char *strpbrk(const char *s1, const char *s2);`
* `strrchr` 回傳在字串 s 中，字元 c 最後一次出現位置的指標	`char *strrchr(const char *s, int c);`
* `strstr` 回傳在字串 s2 在 s1 第一次出現位置的指標 `char *strstr(const char *s1, const char *s2);`
* `strtok` 以字串 s2 的內容切割 s1 `char *strtok(char *s1, const char *s2);`

### Memory operation

* `memcpy` 從 s2 所指向的資料複製 n 個字元到 `s1	void *memcpy(void *s1, const void *s2, size_t n);`
* `memmove`	從 s2 所指向的資料複製 n 個字元到 `s1	void *memmove(void *s1, const void *s2, size_t n);`
* `memcmp` 比較 s1 與 s2 前 n 個字元的資料 `int memcmp(const void *s1, const void *s2, size_t n);`
* `memchr` 找出字元 c 在 s 前 n 個字元第一次出現的位置 `void *memchr(const void *s, int c, size_t n);`
* `memset` 將 s 中前 n 個字元全部設定為 c	`void *memset(void *s, int c, size_t n);`
