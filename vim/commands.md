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

## Replace a word with yanked word
[link](https://vim.fandom.com/wiki/Replace_a_word_with_yanked_text)

### Generate a number sequence in file

Go to line #4, use Ctrl-v to blockwise select the first character, go down 4 lines, press Shift i, enter 0  (this is 0, followed by Space) and Esc to exit insert mode.

Now use gv to re-select the previously selected area. Press g Ctrl-a to create a sequence.

I start with a 0 here, so I can re-select by gv. If you start with a 1, you need to re-select by hand while omitting the first 1.

Use 2g Ctrl-a to use a step count of 2.

[link](https://stackoverflow.com/questions/9903660/how-to-generate-a-number-sequence-in-file-using-vi-or-vim)
