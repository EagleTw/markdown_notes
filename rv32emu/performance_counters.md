# Performance & Conunters 

## Support Instructions (Timers and Counters)
* *RDCYCLE[H]
    * rdcycle用來讀取最低 31-bit cycle CSR，rdcycleh用來讀取最高 31-bit cycle數。

* RDTIME[H]
    * 用來讀取 time CSR。

* RDINSTRET
    * 用來讀取 instret CSR。


## ToDo
- [x] 1. Add new register in structure `riscv_t`
- [x] 2. Create an API for getting performance counter 
- [ ] 3. Implementing the incrementation of CSR_CYCLEH, CSR_TIME and CSR_INSTRT in `rv_step()`

## Little notes

* Before commit 
    * `clang-format -i <file>` before commit 
    * make check everything is good
