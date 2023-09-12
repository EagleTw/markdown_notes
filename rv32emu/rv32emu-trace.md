# rv32emu trace code

###### tags: `Project`

by [\<ypaskell\>](https://github.com/ypaskell)

## 目標

完整了解 rv32emu 的 code

## Setup environment

### 1. Add debug flag to Makefile

Add `-g` in Makefile

```Makefile=
include mk/common.mk
include mk/toolchain.mk

OUT ?= build
BIN := $(OUT)/rv32emu

CFLAGS = -std=gnu99 -O2 -Wall -Wextra
CFLAGS += -Wno-unused-label -g    #<--- Add CFLAGS -g here
CFLAGS += -include src/common.h

# Set the default stack pointer
CFLAGS += -D DEFAULT_STACK_ADDR=0xFFFFF000

OBJS_EXT :=

# Control and Status Register (CSR)
ENABLE_Zicsr ?= 1
$(call set-feature, Zicsr)
```

### 2. Build debug build

```shell
make all
```

## Understanding elf files `hello.elf`

### Objdump `hello.elf`

Run `riscv32-unknown-elf-objdump -dhs build/hello.elf | less`

* `-d`: Display assembler contents of executable sections
* `-h`: Display the contents of the section headers
* `-s`: Display the full contents of all sections requested

```Text=
$ riscv32-unknown-elf-objdump -dhs build/hello.elf

build/hello.elf:     file format elf32-littleriscv

Sections:
Idx Name          Size      VMA       LMA       File off  Algn
  0 .text         00000050  00000000  00000000  00001000  2**2
                  CONTENTS, ALLOC, LOAD, READONLY, CODE
  1 .riscv.attributes 0000001a  00000000  00000000  00001050  2**0
                  CONTENTS, READONLY
Contents of section .text:
 0000 93020000 13035000 6f004000 13000000  ......P.o.@.....
 0010 63826202 93080004 13051000 97050000  c.b.............
 0020 93854502 1306d000 73000000 93821200  ..E.....s.......
 0030 6ff01ffe 9308d005 13050000 73000000  o...........s...
 0040 48656c6c 6f20576f 726c6421 0a000000  Hello World!....
Contents of section .riscv.attributes:
 0000 41190000 00726973 63760001 0f000000  A....riscv......
 0010 05727633 32693270 3100               .rv32i2p1.

Disassembly of section .text:

00000000 <.text>:
   0:	00000293          	li	t0,0
   4:	00500313          	li	t1,5
   8:	0040006f          	j	0xc
   c:	00000013          	nop
  10:	02628263          	beq	t0,t1,0x34
  14:	04000893          	li	a7,64
  18:	00100513          	li	a0,1
  1c:	00000597          	auipc	a1,0x0
  20:	02458593          	addi	a1,a1,36 # 0x40
  24:	00d00613          	li	a2,13
  28:	00000073          	ecall
  2c:	00128293          	addi	t0,t0,1
  30:	fe1ff06f          	j	0x10
  34:	05d00893          	li	a7,93
  38:	00000513          	li	a0,0
  3c:	00000073          	ecall
  40:	6548                	flw	fa0,12(a0)
  42:	6c6c                	flw	fa1,92(s0)
  44:	6f57206f          	j	0x72f38
  48:	6c72                	flw	fs8,28(sp)
  4a:	2164                	fld	fs1,192(a0)
  4c:	000a                	c.slli	zero,0x2
	...
```

### elf open

Run `riscv32-unknown-elf-readelf -h build/hello.elf`

```text=
$ riscv32-unknown-elf-readelf -h build/hello.elf
ELF Header:
  Magic:   7f 45 4c 46 01 01 01 00 00 00 00 00 00 00 00 00
  Class:                             ELF32
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              EXEC (Executable file)
  Machine:                           RISC-V
  Version:                           0x1
  Entry point address:               0x0
  Start of program headers:          52 (bytes into file)
  Start of section headers:          4240 (bytes into file)
  Flags:                             0x0
  Size of this header:               52 (bytes)
  Size of program headers:           32 (bytes)
  Number of program headers:         2
  Size of section headers:           40 (bytes)
  Number of section headers:         4
  Section header string table index: 3
```

上面的 Elf Header 是要在 rv32emu `elf_*` 的 function 處理的。

### Start using debugging tool (gdb or lldb)

我在 Apple Silicom M1 上跑，無法使用 gdb。但 lldb 和 gdb 大同小異，請自行轉換 Command

Navigate to main function

```text
(lldb) b main
Breakpoint 1: 25 locations.
(lldb) r
* thread #1, queue = 'com.apple.main-thread', stop reason = breakpoint 1.1
    frame #0: 0x000000010000bca4 rv32emu`main at main.c:112:5 [opt]
   109 	static bool parse_args(int argc, char **args)
   110 	{
   111 	    /* parse each argument in turn */
-> 112 	    for (int i = 1; i < argc; ++i) {
   113 	        const char *arg = args[i];
   114 	        /* parse flags */
   115 	        if (arg[0] == '-') {

(lldb) finish
Process 28894 stopped
* thread #1, queue = 'com.apple.main-thread', stop reason = step out
    frame #0: 0x000000010000bdf4 rv32emu`main(argc=<unavailable>, args=0x000000016fdff368) at main.c:209:18 [opt]
   206 	    }
   207
   208 	    /* open the ELF file from the file system */
-> 209 	    elf_t *elf = elf_new();
   210 	    if (!elf_open(elf, opt_prog_name)) {
   211 	        fprintf(stderr, "Unable to open ELF file '%s'\n", opt_prog_name);
   212 	        return 1;
```

Initialize `elf_t` for saving elf data

```text
(lldb) s
Process 28894 stopped
* thread #1, queue = 'com.apple.main-thread', stop reason = step in
    frame #0: 0x000000010000a81c rv32emu`elf_new at elf.c:137:16 [opt]
   134
   135 	elf_t *elf_new()
   136 	{
-> 137 	    elf_t *e = malloc(sizeof(elf_t));
   138 	    e->hdr = NULL;
   139 	    e->raw_size = 0;
   140 	    e->symbols = map_init(int, char *, map_cmp_uint);
   141 	    e->raw_data = NULL;
   142 	    return e;
   143 	}
```

`elf_t` declared in `elf.c`

```cpp=
typedef struct elf_internal elf_t; // fron elf.h
struct elf_internal {
    const struct Elf32_Ehdr *hdr;
    uint32_t raw_size;
    uint8_t *raw_data;

    /* symbol table map: uint32_t -> (const char *) */
    map_t symbols;
};
```


```cpp=
bool elf_open(elf_t *e, const char *path)
{
    /* free previous memory */
    if (e->raw_data)
        release(e);

#if defined(USE_MMAP)
    int fd = open(path, O_RDONLY);
    if (fd < 0)
        return false;

    /* get file size */
    struct stat st;
    fstat(fd, &st);
    e->raw_size = st.st_size;

    /* map or unmap files or devices into memory.
     * The beginning of the file is ELF header.
     */
    e->raw_data = mmap(0, st.st_size, PROT_READ, MAP_PRIVATE, fd, 0);
    if (e->raw_data == MAP_FAILED) {
        release(e);
        return false;
    }

#else  /* fallback to standard I/O text stream */
    FILE *f = fopen(path, "rb");
    if (!f)
        return false;

    /* get file size */
    fseek(f, 0, SEEK_END);
    e->raw_size = ftell(f);
    fseek(f, 0, SEEK_SET);
    if (e->raw_size == 0) {
        fclose(f);
        return false;
    }

    /* allocate memory */
    free(e->raw_data);
    e->raw_data = malloc(e->raw_size);

    /* read data into memory */
    const size_t r = fread(e->raw_data, 1, e->raw_size, f);
    fclose(f);
    if (r != e->raw_size) {
        release(e);
        return false;
    }
#endif /* USE_MMAP */

    /* point to the header */
    e->hdr = (const struct Elf32_Ehdr *) e->raw_data;

    /* check it is a valid ELF file */
    if (!is_valid(e)) {
        release(e);
        return false;
    }

    return true;
}
```

#### Q&A (2023/09/11)

* Question: 為什麼原本使用 fopen 現在使用 `mmap`.  [man mmap](https://man7.org/linux/man-pages/man2/mmap.2.html) ?
* Jserv: `mmap` 在開啟大檔案時會有優勢。On-demand paging。反之，fopen 遇到大檔案時，開啟時間較慢。
* Question: man `mmap` 説，mmap 是利用 virtual memory。Virtual Memory 在 Disk 不是會比較慢嗎。
* Jserv: virtual memory 不見得跟 disk 有關，請「不要」讀恐龍書來。[這本書可自由下載，品質比恐龍書好多了](https://pages.cs.wisc.edu/~remzi/OSTEP/)

#### ypaskell's study

[understanding mmap, the workhorse behind keeping memory access efficient in linux](https://www.youtube.com/watch?v=8hVLcyBkSXY)

一般使用 fopen 的方式：每一個 fopen, fread, 都是使用 system call，從 user space 轉到 kernel space。每一次的 system call 都要 Virtual Memory 查 TLB，去 Physical Memory 看。 每一個 system call 花的時間不算多，但的 file 大的時候，累積起來也是慢。

而 mmap 是把 file 映射到 Virtual Memory 中，直接可以讀取，少了 system call 的時間。

`struct stat` - [man](https://man7.org/linux/man-pages/man2/stat.2.html)

```cpp=
struct stat {
    dev_t     st_dev;     /* ID of device containing file */
    ino_t     st_ino;     /* inode number */
    mode_t    st_mode;    /* protection */
    nlink_t   st_nlink;   /* number of hard links */
    uid_t     st_uid;     /* user ID of owner */
    gid_t     st_gid;     /* group ID of owner */
    dev_t     st_rdev;    /* device ID (if special file) */
    off_t     st_size;    /* total size, in bytes */
    blksize_t st_blksize; /* blocksize for file system I/O */
    blkcnt_t  st_blocks;  /* number of 512B blocks allocated */
    time_t    st_atime;   /* time of last access */
    time_t    st_mtime;   /* time of last modification */
    time_t    st_ctime;   /* time of last status change */
};
```

下面這一段是一個很神奇的操作，固定大小的資料，可以直接 Assign 成 Structure。就可以非常簡單的 Abstract 資料。

```cpp
/* point to the header */
e->hdr = (const struct Elf32_Ehdr *) e->raw_data;

/* Elf32 header */
struct Elf32_Ehdr {
    uint8_t e_ident[EI_NIDENT];
    Elf32_Half e_type;      /* Object file type */
    Elf32_Half e_machine;   /* Architecture */
    Elf32_Word e_version;   /* Object file version */
    Elf32_Addr e_entry;     /* Entry point virtual address */
    Elf32_Off e_phoff;      /* Program header table file offset */
    Elf32_Off e_shoff;      /* Section header table file offset */
    Elf32_Word e_flags;     /* Processor-specific flags */
    Elf32_Half e_ehsize;    /* ELF header size in bytes */
    Elf32_Half e_phentsize; /* Program header table entry size */
    Elf32_Half e_phnum;     /* Program header table entry count */
    Elf32_Half e_shentsize; /* Section header table entry size */
    Elf32_Half e_shnum;     /* Section header table entry count */
    Elf32_Half e_shstrndx;  /* Section header string table index */
};

typedef uint32_t Elf32_Addr;
typedef uint32_t Elf32_Off;
typedef uint16_t Elf32_Half;
typedef uint32_t Elf32_Word;
```


## TODO

- [] Understand the code
- [] Improve comments in `riscv_private.h`
