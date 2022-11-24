# [Tips] 常見的 VIM 指令整理
###### tags: `SNPS`,`Programming`, `Tips`


## 編輯模式

 | 指令  | 說明                                   |
 | ----- | -------------------------------------- |
 | i     | 在游標位置進入編輯模式                 |
 | a     | 在游標位置後進入編輯模式               |
 | A     | 在游標行的最後一個字元進入編輯模式     |
 | I     | 在游標行的第一個非空白字元進入編輯模式 |
 | o     | 向下新增一行，並進入編輯模式           |
 | O     | 向上新增一行，並進入編輯模式           |
 | [ESC] | 取消指令或退出編輯模式                 |

## 游標移動

| 指令           | 說明              |
| -------------- |:----------------- |
| gg             | 移到第一行        |
| G              | 移到最後一行      |
| 行數 → G       | 移動到第 n 行     |
| 0              | 移動到該行最前面  |
| $              | 移動到該行最後面  |
| 字數 → [Space] | 向右移動 n 個字元 |
| 行數 → [Enter] | 向下移動 n 行     |
| <ctrl> + o     | 去上一個位置      |
| <ctrl> + i     | 去下一個位置      |
|                |                   |
|                |                   |

| 指令 | 說明             |
| ---- |:---------------- |
| gd   | Go to definition |
| gt   | go to next tab   |
|:qa   | quit all         |


## 多行註解

### A. vim加上多行註解的步驟：

1. 將游標移到要開始註解的那一列。
2. 按下ESC、然後按下Ctrl + V ，切換成區塊選取的模式(就是反白啦)。
3. 將游標向下移到要加上註解的最後一列，此時你可以發現這幾列都被反白了。
4. 按下大寫I，游標跑回步驟(2)的那一列了，這時就可以直接輸入要用的註解了，假設輸入'//'。
5. 按下ESC，大功告成。
6. 千萬不要忘記步驟(5)。

### B. vim 取消多行註解的步驟：

1. 方法和加上多行註解一樣，先將游標移到開始註解的那一列。
2. 按下ESC、然後按下Ctrl + V ，切換成區塊選取的模式。
3. 將游標向下移到要加上註解的最後一列，再按左、右的方向鍵，將要delete掉的註解都反白。
4. 按下delete，大功告成。

### C. Vim Plugin

只要簡單的 \x 就可以註解或取消註解了。

Github: [vim-addon-manager ](https://github.com/MarcWeber/vim-addon-manager)

只要安裝
`sudo aptitude install vim-addon-manager vim-scripts`
然後
`vim-addons install enhanced-commentify`  
  
接著就可以很輕鬆的操作
"\x" (反斜線+x)
你就會發現這些文字全部被註解掉了！

取消註解，同樣地選取起來，再按一下"\x"就可以了。
也可以用"\c"，會自動跳到下一行。

### D. 使用替換命令

## Flags for Search and Replace

* `g` replace all occurrences within line
* `c` ask for confirmation before each replacement
* `i` ignore case for searchpattern
* `I` don't ignore case for searchpattern

### Pattern atom

* `^ start matching from beginning of a line
  * `/^` This match This only at beginning of line
* `$` match pattern should terminate at end of a line
  * `/)`$ match ) only at end of line
  * `/^$` match empty line
* `.` match any single character, excluding new line
  * `/c.t` match 'cat' or 'cot' or 'c2t' or 'c^t' but not 'cant'

For more info, :h pattern-atoms

### Pattern Qualifiers

* `*` greedy match preceding character 0 or more times
  * `/abc*`` match 'ab' or 'abc' or 'abccc' or 'abcccccc' etc
* `\+` greedy match preceding character 1 or more times
  * `/abc\+` match 'abc' or 'abccc' but not 'ab'
* `\?` match preceding character 0 or 1 times (\= can also be used)
  * `/abc\?` match 'ab' or 'abc' but not 'abcc'

For more info, `:h pattern-overview`

#### Character Classes

For more info, `:h /character-classes`

#### 常用例子

在 VIM normal mode 中輸入

* `:% s/^/#/g`   在全部內容的行首添加 # 號註解 
* `:1,10 s/^/#/g`   在1~10 行首添加 # 號註解
* `:%s/-.*//g` 刪除全部的 "-abcd1234" Option
* `:%s/\<foo\>//g`On each line, delete all occurrences of the whole word "foo".
* `:%s/^\s*//g` Clear all white space in the begin
* `:%s/\d\{2}//g`
