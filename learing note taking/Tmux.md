# What is Tmux
--> Its a virtual terminal for Linux command which help user for improving performance. 

# Install TMUX

```bash
sudo apt install tmux
```
or
```bash
sudo nala install tmux
```
# basic command

1. start 1st session
```bash
tmux 
```
2. To exit session
```
Ctrl + b then x then y to exit
```
3. start session with name
```
tmux new-session -s <name>
```
4. detach session
```
Ctrl + b then d
```
5. check current session
```
tmux ls
```
6. attach to session
```
tmux attach -t <session id or session name> 
```
7. Kill session or server
```
tmux kill-session    #tmux kill-session
tmux kill-session -t <session id>
tmux kill-server   # kill all sessions
tmux kill-session -a # kill all except recent session
```
## short-cut keys
- **Ctrl+B D** — Detach from the current session.
- **Ctrl+B %** — Split the window into two panes horizontally.
- **Ctrl+B "** — Split the window into two panes vertically.
- **Ctrl+B Arrow Key** (Left, Right, Up, Down) — Move between panes.
- **Ctrl+B X** — Close pane.
- **Ctrl+B C** — Create a new window.
- **Ctrl+B N** or **P** — Move to the next or previous window.
- **Ctrl+B 0 (1,2...)** — Move to a specific window by number.
- **Ctrl+B :** — Enter the command line to type commands. Tab completion is available.
- **Ctrl+B ?** — View all keybindings. Press **Q** to exit.
- **Ctrl+B W** — Open a panel to navigate across windows in multiple sessions.