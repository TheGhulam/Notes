### Notes
- C-b c (that’s Ctrl and b at once, then c)

## Starting you session
```shell
tmux
```

## Splitting panes
```
C-b % #Left & Right
C-b " #Top & bottom
```

## Navigating panes
```shell
C-b <arrow key>
```

## Closing panes
```shell
C-d or exit
```

## Creating Windows
```shell
C-b c
```

## Switching windows
```shell
C-b p #Previous
C-b n #Next
C-b <number> 
```

## Session handling
```shell
C-b d #Detach current session
C-b D #Interactive detach
tmux ls #View running sessions
tmux attach -t <number> #Connect to session number <number>
tmux atach -t database #Connect to session database
tmux new -s database #Create session "database"
tmux rename-session -t 0 database #Rename "session 0" to "database"
```

## View all available commands
```shell
C-b ?

#Popular commands
C-b z #Make a pane go full screen. Hit `C-b z` again to shrink it back to previous size
C-b C-<arrow key> #Resize pane in direction of <arrow key>
C-b , #Rename the current window
```
