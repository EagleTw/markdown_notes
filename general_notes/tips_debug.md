# [Tips] Debugging Note

###### tags: `SNPS`, `Tips`

## cgdb

### Commands available during CGDB mode

- [3.1 Commands available during CGDB mode](https://cgdb.github.io/docs/cgdb.html#CGDB-Mode)
- 左右分割 Toggle the window orientation (horizontal <-> vertical)
  1. &lt;Esc&gt;
  2. &lt;Ctrl&gt; + w

### Breakpoints

- break &lt;where&gt; (b) --> Set a new breakpoint.
- delete &lt;breakpoint&gt; --> Delete a breakpoint.
- clear --> Delete all breakpoints.
- enable &lt;breakpoint#&gt; --> Enable a disabled breakpoint.
- disable &lt;breakpoint#&gt; --> Disable a breakpoint.

- `break file:line if strcmp(y, "hello") == 0`

### Stepping

- step (s) --> Go to next instruction (source line), diving into function
- next (n) -->Go to next instruction (source line) but donʻt dive into functions.
- finish --> Continue until the current function returns.
- continue (c ) --> Continue normal execution
- `target record-full` --> Turn on reverse stepping

### Variables and Memory

- `whatis` --> Show C variable type
- print/format &lt;what&gt; --> Print content of variable/memory location/register.
- display/format &lt;what&gt; --> Like „print“, but print the information after each stepping instruction.
- undisplay &lt;display#&gt; --> Remove the „display“ with the given
  number.
- enable display &lt;display#&gt;
- disable display &lt;display#&gt; --> En- or disable the „display“ with the given number

### Manipulating the program

- set var &lt;variable_name&gt;=&lt;value&gt; --> Change the content of a variable to the given value.
- set environment FOO = 1 --> Environment
  - show environment Foo
- return &lt;expression&gt; --> Force the current function to return immediately, passing the given value
- Setting number-of-elements to zero means that the printing is unlimited.
  - `set print elements 0`

### Informations

- disassemble
- disassemble &lt;where&gt; --> Disassemble the current function or given location.
- info args --> Print the arguments to the function of the current stack frame.
- info breakpoints --> Print informations about the break- and watchpoints.
- info display --> Print informations about the „displays“.
- info locals --> Print the local variables in the currently selected stack frame.
- info sharedlibrary --> List loaded shared libraries.
- info signals --> List all signals and how they are currently handled.
- info threads --> List all threads.
- **info line** --> Show filename and line.
- show directories --> Print all directories in which GDB searches for source files.
- show listsize --> Print how many are shown in the „list“ command.
- whatis &lt;variable_name&gt; --> Print type of named variable

## GDB TUI Mode

- `Ctrl+X`, `A` to enable/disable.
- `Ctrl+X`, `O` to switch between active windows SourceCode(upside) / GdbCommand(downside).
- `Ctrl+L` to redraw windows if text display strangely.

## pstack

1. `<Ctrl+z>` stop the stuck process
2. `ps` check the stuck process pid
3. `pstack <pid>`
4. `gdb -pid <pid>`
