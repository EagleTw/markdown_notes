# [Tips] Tmux tips

## Sessions

* New session `tmux new -s <session name>`
* Check sessions `tmux ls`
* Attach
  * `tmux attach <session name>`
  * `tmux at <session name>`
* Detach `tmux detach <session name>`
* Rename sesson `Ctrl + b $`
* Session and Window Preview `Ctrl + b w`
* Move to session
  * previous session `Ctrl + b (`
  * next session `Ctrl + b )`

## Windows

## Planes

* Toggle last active pane `Ctrl + b ;`
* Split pane with horizontal layout `Ctrl + b %`
* Split pane with vertical layout `Ctrl + b "`
* Move the current pane left `Ctrl + b {`
* Move the current pane right `Ctrl + b }`
* Switch to pane to the direction `Ctrl + b <arrow key>`
* Show pane numbers `Ctrl + b q`
* Switch/select pane by number `Ctrl + b q 0...9`
* Toggle pane zoom `Ctrl + b z`
* Close current pane `Ctrl + b x`

## Copy Mode

* Enter copy mode `Ctrl + b [`
* Quit mode `q`
* Start selection `[Spacebar]`
* Copy selection `[Enter]`
* Paste contents of buffer_0 `Ctrl + b ]`
* display buffer_0 contents `:show-buffer`
* Save buffer contents to buf.txt `:save-buffer buf.txt`
* Show all buffers `:list-buffers`


## Other tips

* Change horizonal split to vertical split `<Ctrl+b> + space`
