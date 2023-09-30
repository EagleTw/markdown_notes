# Progress Log

**Starting Date:** 2023/09/23

## 2023/09/23 (Sat) ~ 2023/09/24 (Sun)

- **Conversation with Jersv:**
  I asked Jersv whether it is possible to focus on branch prediction on rv32emu.

  > "你看[這篇論文](https://research.manchester.ac.uk/en/publications/evaluating-the-impact-of-optimizations-for-dynamic-binary-modific?fbclid=IwAR0D1Mej_z6l6IVULspspPKKXuw2I1idvFhstq4_MIT2UDFbIladm-6wpVI)，主要講 branch optimization。這篇論文的題材比你想像中更窄，但依舊是很好的研究。--Jserv

- **Reading Notes - Evaluating the Impact of Optimizations for Dynamic Binary Modification on 64-bit RISC-V:**

  - **Question 1:** What is the question of the paper?

    - **Answer:**

      Target in the code cache exceeds ±1MB range, but the original address in the original binary did not. They discuss "jump trampolines" to remove JALR with JALs, avoiding overhead with register jumps.

      - **Subquestion:** What is register jump overhead?

        - **Answer:**

          "Register jump overhead" refers to the additional processing time or computational overhead caused by using jump instructions, like conditional jumps or branches, which requires the CPU to perform tasks like saving and restoring the program counter or updating branch prediction.

  - **Question 2:** What is Dynamic Binary Modification?

    - **Answer:** Dynamic Binary Modification (DBM) involves modifying a program's binary code during runtime.

      - **Sub-questions:**

        - When does it happen?

          - **Answer:** DBM occurs during runtime.

        - What applications can be done?

          - **Answer:** DBM includes binary instrumentation (DBI), binary translation, virtualization, and error detection.

        - Disadvantages?

          - **Answer:** DBM has performance overhead, particularly in handling position-dependent instructions.

        - Frameworks:

          - **Answer:** One of the frameworks for DBM is MAMBO.

        - "Dynamic Binary Modification" 會降低執行效率，為什麼還值得做?

          - **Answer:**

            > Jserv: 因為某些指令序列的執行成本更高

  - **Question 3:** What is the purpose of jump trampolines and how do they affect performance?

    - **Answer:**
      (NYI)

  - **Question 4:** What benchmark is used?

    - **Answer:** SPEC CPU2006

  - **Question 5:** What are the steps to perform branch optimization?

    - **Answer:** (NYI)

  - **Question 6:** What data structures are needed?

    - **Answer:** (NYI)

  - **Question 7:** RV32I 的 JAL 最遠可以跳多遠?

    - **Answer:**

      在 RISC-V 的 RV32I 指令集中，JAL（Jump and Link）指令使用的立即值（即跳躍偏移量）是 20 位，用來計算目標地址。這個 20 位的立即值代表的是跳躍目標相對於下一條指令的偏移量，以字節（byte）為單位。

      計算跳躍目標地址的方法：

      將 20 位的立即值（imm）左移 1 位（乘以 2），以變為 21 位，再將這 21 位的立即值加上下一個指令的地址（PC + 4），得到跳躍目標地址。
      所以，JAL 指令的最大偏移量就是能夠表示的最大 20 位二進制數的一半，再乘以 2，即：

      最大偏移量 = (2^19 - 1) \* 2 bytes = 524,286 bytes = 0.52 MB

      這代表 JAL 指令可以跳躍到目標地址的最遠範圍是 524,286 個字節。這個範圍是相對於當前指令位置的偏移量，並且可以向前或向後跳躍。

      [When to use J, JAL, JR, JALR?](https://www.reddit.com/r/RISCV/comments/13rcn8e/when_to_use_j_jal_jr_jalr/)

  - **ENGLISH VOCABULARIES**
    1. necessitate 使成為必需 (你ㄙㄟ捨 tate)
    2. exploit 利用;開發;發揮

### MAMBO

Download [MAMBO](https://github.com/beehive-lab/mambo)

```bash
git clone --recurse-submodules https://github.com/beehive-lab/mambo.git
cd mambo

cd pie
make all

cd ../
make
```

Run First Example:

```bash
% ./dbm /bin/ls -g
# ./dbm <path_to_executable> <args>
drwxrwxr-x 2 clarity    4096 Sep 24 15:00 api
drwxrwxr-x 4 clarity    4096 Sep 24 14:57 arch
-rw-rw-r-- 1 clarity   10887 Sep 24 14:57 common.c
-rw-rw-r-- 1 clarity    3378 Sep 24 14:57 common.h
-rwxrwxr-x 1 clarity 1254064 Sep 24 15:04 dbm
-rw-rw-r-- 1 clarity   21143 Sep 24 14:57 dbm.c
-rw-rw-r-- 1 clarity   12409 Sep 24 14:57 dbm.h
-rw-rw-r-- 1 clarity    3173 Sep 24 14:57 dispatcher.c
drwxrwxr-x 2 clarity    4096 Sep 24 15:00 elf
-rw-rw-r-- 1 clarity     440 Sep 24 14:57 kernel_sigaction.h
-rw-rw-r-- 1 clarity   11358 Sep 24 14:57 LICENSE
-rw-rw-r-- 1 clarity    3358 Sep 24 14:57 makefile
drwxrwxr-x 2 clarity    4096 Sep 24 15:04 pie
drwxrwxr-x 4 clarity    4096 Sep 24 14:57 plugins
-rw-rw-r-- 1 clarity    1226 Sep 24 14:57 plugins.h
-rw-rw-r-- 1 clarity    9892 Sep 24 14:57 README.md
-rwxrwxr-x 1 clarity    4566 Sep 24 14:57 scanner_common.h
-rw-rw-r-- 1 clarity    7419 Sep 24 14:57 scanner_public.h
-rw-rw-r-- 1 clarity   20265 Sep 24 14:57 signals.c
-rw-rw-r-- 1 clarity   16254 Sep 24 14:57 syscalls.c
-rw-rw-r-- 1 clarity    1349 Sep 24 14:57 syscalls.h
drwxrwxr-x 3 clarity    4096 Sep 24 14:57 test
-rw-rw-r-- 1 clarity   27466 Sep 24 14:57 traces.c
-rw-rw-r-- 1 clarity    1975 Sep 24 14:57 util.h
-rw-rw-r-- 1 clarity    7031 Sep 24 14:57 util.S
We re done; exiting with status: 0 #<-- by dbm
```

## 2023/09/25 (Mon.)

Jserv: 你要先了解模擬器的類型

### [Banshee: A Fast LLVM-Based RISC-V Binary Translator](https://pulp-platform.org/docs/Banshee_ICCAD_2021.pdf?fbclid=IwAR0RzIDLto_-bNwb0w8FSCVlJ32VrIUMbV5qNzvEoDkHKVg8F3j6dZqrXvg)

Github Link -- [[link]](https://github.com/pulp-platform/banshee)

- **Question 1:** 文中分三種 Simulator? 哪三種

  - **Answer:**

    1. **Cycle-accurate**

       - Verilator[7], Questa Advanced Simulator[8]
       - Very slow for large systems (tens of kIPS)

    2. **Event-based**

       - gem5[9], GVSoC[10]
       - Few MIPS, still too slow

    3. **Functional**
       - QEMU[11,12], rv8[13], R2VM[24]
       - Few GIPS, but only for a handful of cores

**None are well-suited for manycore!**

- **Question 2:** What strategy Banshee take?

  - **Answer:**

    (Banshee is a functional emulator)

    1. Static binary translation
    2. RISC-V binary &rarr; \[Binary to IR Translator\] &rarr; LLVM IR &rarr; Opt
       &rarr; \[IR to Host Translator\] &rarr;

    3. Emulation: Using host's parallism

- **Question 3:** What evaluation is done?

  - **Answer:**
    1. performance estimation
    2. Benchmark: LFSR (Compute bound)
    3. With or without ISA extensions
       - Floating-point repetition
       - (Indirect) Stream Semantic Registers (Xssr & Xissr)
    4. Scaling with manticore
    5. Scaling with MemPool
    6. Comparrison to related work
    7. Latency modeling

- **Question 4:** Single thread binary how to scale with multicore?
  - **Answer:**
    - NYI

## 2023/09/30 (Sat.)

### Reading nots:

#### **Towards a High-Performace RISC-V Emulator**

- RISC-V 目前可以用的 Emulator 不多，想要最快，所以使用 DBT (Dynamic Binary Translation) / SBT (Static Binary Translation)。

DBT 其中一種技巧叫 Region Formation Technique (RFT) - Region formation is the process of dividing the binary code into segments or blocks, referred to as regions, based on certain criteria.

- **Question 1:** What are the contributions?
  - **Answer:**
      1. Show that it is possible to perform a high-quality translation of RISC-V binaries to x86 and ARM
      2. Compare the performance of their SBT with performance of other RISC-V emulators and argue that **there is a lot of room for performce improvements.**

- **Question 2:**


- **Related work**
  - OpenISA
  - RISC-V Emulators
    - Spike (RISC-V Foundation)
      - Iterpreted simulator, 15x to 75x slower than native
    - ANGEL (Javascript RV64 simulator)
  - RISC-V DBT Engines
    - Pydgin (3.3x to 4x slower than native)
    - RV8 (3.16x slower than nativ)
    - QEMU (7x slower)

- **Question 3:** How to achieve RISC-V SBT?
  - **Answer:**
  
  ![RISC_V SBT Archetechure](../Images/RISC-V_SBT-archetechure.jpg)

