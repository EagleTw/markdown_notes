# Progress Log

**Starting Date:** 2023/09/23

## 2023/09/23 (Saturday)

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

  - **Question 3:** What is the purpose of jump trampolines and how do they affect performance?
    - **Answer:**
      NYI

  - **Question 4:** What benchmark is used?
    - **Answer:** SPEC CPU2006

  - **Question 5:** What are the steps to perform branch optimization?

  - **Question 6:** What data structures are needed?

  - **Question 7:** RV32I 的 JAL 最遠可以跳多遠?
    - **Answer:**

      在 RISC-V 的 RV32I 指令集中，JAL（Jump and Link）指令使用的立即值（即跳躍偏移量）是 20 位，用來計算目標地址。這個 20 位的立即值代表的是跳躍目標相對於下一條指令的偏移量，以字節（byte）為單位。

      計算跳躍目標地址的方法：

      將 20 位的立即值（imm）左移 1 位（乘以 2），以變為 21 位，再將這 21 位的立即值加上下一個指令的地址（PC + 4），得到跳躍目標地址。
      所以，JAL 指令的最大偏移量就是能夠表示的最大 20 位二進制數的一半，再乘以 2，即：

      最大偏移量 = (2^19 - 1) * 2 bytes = 524,286 bytes = 0.52 MB

      這代表 JAL 指令可以跳躍到目標地址的最遠範圍是 524,286 個字節。這個範圍是相對於當前指令位置的偏移量，並且可以向前或向後跳躍。


  - **ENGLISH VOCABULARIES**
    1. necessitate 使成為必需 (你ㄙㄟ捨tate)
    2. exploit 利用;開發;發揮