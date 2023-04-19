# Usefull C tricks

## [Check Your Pointers at Runtime](https://www.youtube.com/watch?v=yM9zteeTCiI)

```c
int ismapped(const void *ptr, int bytes) {
    if (ptr == NULL) {
        return 0;
    }

    // create a pipe
    int fd[2];
    int valid = 1;

    pipe(fd);
    if (write(fd[1], ptr, bytes) < 0) {
        if (errno == EFAULT)
            valid = 0;
    }
    close(fd[0]);
    close(fd[1]);
    return valid;
}

void testptr(void *p, int bytes, char *name) {
    printf("%s:\t%d\t%p\n", name, ismapped(p, bytes), p);
}

int main() {
  int *null = NULL;
  int *p = malloc(50);
  int *ran = (int*)((uintptr_t)0x312412314);
  int x = 5;
  int *px = &x;

  testptr(null, 1, "null");
  testptr(px, sizeof(int), "px");
  testptr(ran, sizeof(int), "ran");

  return 0;
}

```