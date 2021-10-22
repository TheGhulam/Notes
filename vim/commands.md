### Deleting currently open file
Using an external tool such as *rm*(1) is fine, but Vim also has its own [`delete()`][1] function for deleting files. This has the advantage of being portable.

    :call delete(expand('%'))

An alternative way of expressing this is `:call delete(@%)`, which uses the [`%`][2] (current file) register (tip by @accolade).

To completely purge the current buffer, both the file representation on disk and the Vim buffer, append [`:bdelete`][3]:

    :call delete(expand('%')) | bdelete!
 https://stackoverflow.com/questions/16678661/how-can-i-delete-the-current-file-in-vim/16679182#16679182



### Fixing "TabError: inconsistent use of tabs and spaces in indentation?"

:retab

[link](https://stackoverflow.com/questions/48735671/use-vim-retab-to-solve-taberror-inconsistent-use-of-tabs-and-spaces-in-indentat)
### How to yank the text on a line and paste it inline in Vim?
Copy from beginning to end of line
^y$

Easier to reach:
_y$

[link](ttps://stackoverflow.com/questions/7774015/how-to-yank-the-text-on-a-line-and-paste-it-inline-in-vim)
