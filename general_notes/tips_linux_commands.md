# [Tips] Linux Command Tips 
* Author: Yi-Ping Pan

###### tags: `SNPS`, `Tips`


## General Tips

* Out to file
  * `>>` operator is used for utilizing the command’s output to a file, including the output to the file’s current contents.
  * `>` operator is used to redirect the command’s output to a single file and replace the file’s current content. 
* 資料流
  * 標準輸入（standard input，代碼為 0）：程式執行所需要的輸入資料。
  * 標準輸出（standard output，代碼為 1）：程式正常執行所產生的輸出資料。
  * 標準錯誤輸出（standard error output，代碼為 2）：程式出錯時通知使用者用的訊息，或是呈現程式狀態用的訊息。
  * Example: 
    * `ls non_exist > output.txt 2> error.txt`
    * `ls non_exist > output.txt 2>&1` 
      2>&1 就是把標準錯誤輸出（2）導入標準輸出（1）的意思，然後再靠著 > 把所有的資料全部導入 output.txt，這樣所有的輸出訊息就會一起存入 outpupt.txt 中了。
* `chmod -R u+w`
* `watch -n 2 tail -n 15 mylogfile.txt` --> monitor only the last n lines of a log file
* `watch -n 1 cat file` --> Cat appending log every 1 second
*  `【Ctrl】; + 【z】` -->  `fg`
* `awk 'NR>=10 && NR<=15' file1.txt > file2.txt` --> copy line to line to new file
* Loop through folder and do sth

  ```shell@
  for dir in */;
  do
    echo "Clean reg files: $dir"
    ( cd "$dir" && sh /remote/us01home50/yipingp/MyUtils/cleanReg )
  done;
  ```

  * `(`,`)` create a subshell, so the current directory isn't changed in the main script.
* `p4 changes -L | ripgrep -C10 TOCTOU` --> grep changelist with particular sting

* `du -sh .` --> Check used space
* `patch -p4 < <*.diff>` --> patch diff file

## Grep

* `grep -rnw '/path/to/somewhere/' -e 'pattern'` --> Search text in directory
  * `-r` or `-R` is recursive,
  * `-n` is line number, and
  * `-w` stands for match the whole word.
  * `-l` (lower-case L) can be added to just give the file name of matching files.
  * `-e` is the pattern used during the search

## Ctags

1. 首先先在source code的最外層目錄輸入指令: `ctags -R *`
2. vim中輸入以下指令來載入對應的tag: `:set tags=/home/sway/src/tags`
3. function call上時
  * 跳到function的定義: `【Ctrl】+【]】`
  * 回到function call的地方: `【Ctrl】+【t】`

By default vim will jump to the first result, but the following commands can be used to sort through the list of tags:

* `:ts or :tselect shows the list`
* `:tn or :tnext goes to the next tag in that list`
* `:tp or :tprev goes to the previous tag in that list`
* `:tf or :tfirst goes to the first tag of the list`
* `:tl or :tlast goes to the last tag of the list`

* `fprintf(stderr, "sth", &sth)`
* qdf -s .

## Tmux

### Copy and pastek

1. C-b +\[  --> to copy mode
2. _space-  --> select
3. C-w    --> copy to clipboard
4. C-b + \] --> paste
