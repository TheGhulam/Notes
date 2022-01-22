Notation
- CTRL = ^
- same command pressed twice applies it to the line (e.g. dd)

Modes
* Normal 
* Insert (i)
* Replace (R)
* Visual (plain, line, or block) (v, V, ^v)
* Command line (:)

Command-line
```
:q quit (close window)
:w save (“write”)
:wq save and quit
:e {name of file} open file for editing
:ls show open buffers
:help {topic} open help
:help :w opens help for the :w command
:help w opens help for the w movement
```

## Movement
```
Basic movement: hjkl (left, down, up, right)
Words: w (next word), b (beginning of word), e (end of word)
Lines: 0 (beginning of line), ^ (first non-blank character), $ (end of line)
Screen: H (top of screen), M (middle of screen), L (bottom of screen)
Scroll: Ctrl-u (up), Ctrl-d (down)
File: gg (beginning of file), G (end of file)
Line numbers: :{number}<CR> or {number}G (line {number})
Misc: % (corresponding item)
Find: f{character}, t{character}, F{character}, T{character}
find/to forward/backward {character} on the current line
	, / ; for navigating matches
Search: /{regex}
	n / N for navigating matches
```

## Edits
```
i enter Insert mode
	but for manipulating/deleting text, want to use something more than backspace
o / O insert line below / above
d{motion} delete {motion}
	e.g. dw is delete word, d$ is delete to end of line, d0 is delete to beginning of line
c{motion} change {motion}
	e.g. cw is change word
	like d{motion} followed by i
x delete character (equal do dl)
s substitute character (equal to xi)
Visual mode + manipulation
	select text, d to delete it or c to change it
u to undo, <C-r> to redo
y to copy / “yank” (some other commands like d also copy)
p to paste
Lots more to learn: e.g. ~ flips the case of a character
	. repeats previous edit
```


Modifiers
```
ci<character> => Change inside character
di<character> => Delete inside character
da<character> => Delete including character
```

Copy & Paste
```
y => copy
yy => copy line
yw => copy word

p => paste
```

Misc.
```
~ => Switch case of letters
```

## Vim windows
```
Ctrl+W, S (upper case) for horizontal splitting

Ctrl+W, v (lower case) for vertical splitting

Ctrl+W, Q to close one

Ctrl+W, Ctrl+W to switch between windows

Ctrl+W, J (xor K, H, L) to switch to adjacent window (intuitively up, down, left, right)
```

