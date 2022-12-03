# [lang] SystemVerilog Learning
* Author: Yi-Ping Pan

## Keywords
* Chap 6. -- Data types
* Chap 7. -- Aggregate data types
* Chap 8. -- Classes
* Chap 9. -- Processes
* Chap 10. -- Assignment statements
* Chap 11. -- Operators and expressions
...
* Chap 23. -- Modules and hierachy
* Chap 25. -- Interfaces
* Chap 26. -- package (包)
    ```
    package p;
        int x1, x2, x3;
    endpackage;
    ```
    * `import p1::f;` --> explicit import
    * `import p1:::*;` --> wildcard import
* Chap 27. Generate constructs --> 快速實力話
    * generate block有点类似for循环，可以减少重复代码。比for高级的地方在于，for只能用在普通的不同index信号的赋值，而generate还可以用于多个module、always、function、task、assign、case、if等等更复杂语句的创建。
    * Syntax
        ```SystemVerilog
        genvar i;
        generate for (i=0; i<=7; i=i+1)
            begin
                assign SIO_model[i] = !spi_oen_mux[i] ? spi_out_mux[i] : 'dz;
            end
        endgenerate;
        ```
    * 在 Elaboration 才動作
    * if, if-else-if, case

* Chap 28. Gate-level and switch-level modeling




## Notes

### Escaped Identifier
![Escaped_Name_verilog](../images/EscapeName_Verilog.png)
