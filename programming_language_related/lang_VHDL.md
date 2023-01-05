# [lang] VHDL vs Verilog 

* Author: Yi-Ping Pan

###### tags: `SNPS`,`learning`

## Links

* [FPGA之道（38）VHDL与Verilog的比较](https://blog.csdn.net/Reborn_Lee/article/details/104320763?app_version=5.9.0&code=app_1562916241&csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22104320763%22%2C%22source%22%3A%22unlogin%22%7D&uLinkId=usr1mkqgl919blen&utm_source=app)
* [Learn VHDL in 24 hours](https://sites.google.com/site/learnvhdl/home)

* VHDL Versions
    * VHDL 1987—Directs the Compiler or Simulator to process VHDL Design Files using the IEEE Std 1076-1987 VHDL standard.
    * VHDL 1993—Directs the Compiler or Simulator to process VHDL Design Files using the IEEE Std 1076-1993 VHDL standard. By default, this option is selected.
    * VHDL 2008—Directs the Compiler or Simulator to process VHDL Design Files using the IEEE Std 1076-2008 VHDL standard.

* Keywords
    * is record --> Used as sturcture in C code 
        ```
        type t_FROM_FIFO is record
          wr_full  : std_logic;                -- FIFO Full Flag
          rd_empty : std_logic;                -- FIFO Empty Flag
          rd_dv    : std_logic;
          rd_data  : std_logic_vector(7 downto 0);
        end record t_FROM_FIFO;
        ```
    * subtype
    * generic(參數名:數據類型:=設定值);
    * Type 是 VHDL 語言中用來宣告訊號型式的指令


## Notes

### Extended Identifier
![Extended Identifier VHDL](../images/EscapeName_VHDL.png)
