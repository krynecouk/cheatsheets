## Window
- `M-x`     split-window
- `M-x`     windmove
- `C-x 1`   only
- `C-x 2`   split
- `C-x 3`   vert split
- `C-x o`   toggle window

> TIP: There is a whole series of commands that start with CONTROL-x; many of
them have to do with windows, files, buffers, and related things.

- `C-x`    	Character eXtend.  Followed by one character.
- `M-x`     Named command eXtend.  Followed by a long name.

## Moving
- `C-v`     go down screen
- `M-v`     got up screen
- `C-l`     text around cursor
- `C-p`     previous line
- `C-n`     next line
- `C-f`     forward one char
- `C-b`     backward one char
- `M-f`     forward one word
- `M-b`     backward one 
- `M-g M-g` go to line

> C operate on basic units (char, lines, blocks).
> M operate on language units (word, sentence, paragraph).

- `C-a`     beginning of a line
- `M-a`     beginning of a sentence
- `C-e`     end of a line
- `M-e`     end of a sentence
- `M->`     end of text
- `M->`     beginning of text

```yml
         Previous line, C-p
                  :
                  :
  Backward, C-b .... Current cursor position .... Forward, C-f
                  :
                  :
            Next line, C-n
```

## Cut/Copy/Delete
- C-spc		visual selection
- `C-w`     cut (killing)
- `M-w`     copy (yanking)
- `C-y`     paste (yank)
- `M-y`     paste different yanks
- `C-d`     delete char
- `M-d`     delete word
- `C-k`     cut from cursor to end of line
- `M-k`     cut from cursor to end of sentence

## Cancelling/Exiting
- `C-g`     cancels query
- `C-x C-c` save and exit
- `C-x C-s` save
- `C-z`     exit temporarily
- `fg`      returns to emacs
- `%emacs`  returns to emacs
- `M-x rec` recovers file from unsaved exit

## Undo/Redo
- `C-/`     undo
- `C-g C-/` redo

## Buffers
- `C-x b`   switch to buffer
- `C-x C-b` show all buffers
- `C-x C-s` save current buffer
- `C-x s`   save buffer cross window

## Macro
- `C-x (`   start macro
- `C-x )`   end macro
- `C-x e`   play last macro

## Numeric arguments
- `C-u`     add number
- `M-<num>` hold M and add number

> example: `C-u 8 C-f` moves cursor 8 forward

## Search and replace
- `M-x repl s` replace string
- `C-s`        search forward
- `C-r`        search backward

## Help
- `C-h k`   find doc of command
- `C-h f`   find doc of function
- `C-h a`   search of commands
- `C-h r`   manual

> example: `C-h k C-f` show docs for `C-f`
