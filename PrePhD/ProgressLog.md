# Progress Log

Starting date: 2023/09/23

## 2023/09/23 (六)

I asked Jersv wheter it is possible to focus on branch prediction on rv32emu.

> 你看[這篇論文](https://research.manchester.ac.uk/en/publications/evaluating-the-impact-of-optimizations-for-dynamic-binary-modific?fbclid=IwAR0D1Mej_z6l6IVULspspPKKXuw2I1idvFhstq4_MIT2UDFbIladm-6wpVI)，主要講 branch optimization。這篇論文的題材比你想像中更窄，但依舊是很好的研究。--Jserv

### 讀書筆記 - Evaluating the Impact of Optimizations for Dynamic Binary Modification on 64-bit RISC-V

- **Question 1**: What is the question of the paper?
  - **Answer:**
  Target in the code cache exceed ±1MB range, but the original address in the original binaray did not. `jump trampollines` - Remove JALR with JALs, avoiding overhead with register jumps

  - **Subquestion:** What is register jump overhead?
   "register jump overhead," it means that using jump instructions (like conditional jumps or branches) can introduce additional processing time or computational overhead because the CPU needs to perform tasks like saving and restoring the program counter or updating the branch prediction.

- **Question 2:**: What is **Dynamic Binary Modification**?
  - **Answer:**

    Sub-questions:

    - When does it happen?
      - **Answer:**
      Runtime

    - What applicaiton can be done?
      - **Answer:**
      Binary instrumentation(DBI), binary translation, virtualization, error detection

    - Disadvantages?
      - **Answer:**
      performance overhead - load, execute, modify a binary. Mostly in **handling iposition depentent instructions**.

    - Frameworks:
      - **Answer:**
      MAMBO

- **Question 3:** What is the purpose of **jump trampolines** and how do they affect performance?
  - **Answer:**
  1234567