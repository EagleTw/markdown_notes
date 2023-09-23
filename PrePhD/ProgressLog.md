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
    - **Answer:**
      Dynamic Binary Modification (DBM) involves modifying a program's binary code during runtime.

      - **Sub-questions:**
        - When does it happen?
          - **Answer:**
            DBM occurs during runtime.

        - What applications can be done?
          - **Answer:**
            DBM includes binary instrumentation (DBI), binary translation, virtualization, and error detection.

        - Disadvantages?
          - **Answer:**
            DBM has performance overhead, particularly in handling position-dependent instructions.

        - Frameworks:
          - **Answer:**
            One of the frameworks for DBM is MAMBO.

  - **Question 3:** What is the purpose of jump trampolines and how do they affect performance?
    - **Answer:**
      NYI

  - **Question 4:** What benchmark is used?
    - **Answer:**
      SPEC CPU2006
