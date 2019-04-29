Basics
------ 
```yml
- i 		# insert
- a 		# append
- 0 		# move cursor to the beginning of the line
- $ 		# move cursor to the end of the line 
```

Undo & Redo
-----------
```yml
- u		# undo
- U		# undo line
- ctrl + r	# redo
```

`:jumps`
--------
```yml
- ctrl + o	# older locations
- ctrl + i	# newer locations
- 25ctrl + o	# 25th older location

- ctrl + g	# where am i
- G		# go to the end of file
- gg		# go to the beggining of file

- }		# next blank line
- {		# previous blank line
- )		# end of sentence
- (		# beg. of sentence
- H		# high of window
- M		# medium of window
- L		# low of window
```

`:changes`
----------
```yml
- g;		# go to previous change
- g,		# go to next change 
- 4g;		# go to 4th previous change
- c$		# change from cursor to the end of line 
- cw		# change word
```

`:marks`
--------
```yml
- ma		# mark line with label 'a'
- `a 		# go to mark 'a'
```

`:registers :reg`
-----------------
```yml
- "2p		# paste previously copied text
```

Delete
------
```yml
- dd		# delete line
- dw		# delete word
- db		# delete back
- d{		# delete end of paragraph
- D		# delete from cursor to the end of line
- r 		# replace
- R 		# replace and insert mod
- x		# remove char
```

Cut, copy, paste
----------------
```yml
- v		# visual one char
- V		# visual one line
- ctrl + v	# visual block
- y		# yank
- yw		# yank word
- p		# paste after cursor
- P		# paste before cursor
- I		# insert in visual mode
- gv		# get last visual
```

Time travel
-----------
`:earlier :ea`
--------------
```yml
- :ea		# earlier {count}	
- :ea		# earlier {N}s		
- :ea		# earlier {N}m		
- :ea		# earlier {N}h		
- :ea		# earlier {N}d		
- :ea		# earlier {N}f		
```
			
`:later :lat`
-------------
```yml
- :lat		# later {count}					
- :lat		# later {N}s					
- :lat		# later {N}m
- :lat		# later {N}h					
- :lat		# later {N}d					
- :lat		# later {N}f		
```
			
Search
------
```yml
- /		# search
- / \c		# search ignore case
- ?		# search backwars
- n		# next
- N		# previous
- f		# find char
- %		# search `(`
- :set hls	# highlight search
- :set nohls	# highlight search  
- :set ic	# case sensitive 
- :set noic	# case insensitive 
- :set is	# instant search
```

`:help`
-------
```yml
- ctrl + w	# switch window
```

`:map`
------
```yml
- :map		# recursive mapping
- :noremap 	# non-recursive mapping
- :nmap		# resurcive mapping in normal mode
- :nnoremap	# non-recursive mapping in normal mode
- :vmap 	# recursive mapping in visual mode
- :vnoremap	# non-recursive mapping in visual mode
```

``` yml
- :nnoremap <Space> i_<Esc>r	# insert one char on space
```
