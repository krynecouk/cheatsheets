Basics
------ 
```yml
- i 		# insert
- a 		# append
- 0 		# move cursor to the beginning of the line
- $ 		# move cursor to the end of the line 
- r 		# replace
- R 		# replace and insert mod
- c$		# change from cursor to the end of line 
- cw		# change word
```

## UNDO & REDO
- **u**(ndo)
- **U**(undo in line)
- CTRL + **r**(edo)

## JUMPS
- **:jumps**
- ctrl + **o**(lder locations)
- ctrl + **i** (newer locations)
- 25ctrl + **o**(25th older location)

- ctrl + **g** (where am i)
- **G**(o to the end of file)
- **gg**(o to the beggining of file)

- **}** (next blank line)
- **{** (previous blank line)
- **)** (end of sentence)
- **(** (beg. of sentence)
- **H**(igh of window)
- **M**(edium of window)
- **L**(ow of window)

## CHANGES
- **:changes**
- **g;**(o to previous change)
- **g,**(o to next change) 
- 4**g;**(o to 4th previous change)

## MARKS
- **:marks**
- **m**(ark) **a** (mark line with label 'a')
- **'a** (go to a line of mark 'a')
- **`a** (go to a location of mark 'a')

## DELETE
- **d**(elete) **w**(ord)
- **D**(elete from cursor to the end of line)
- **d**(elete) **{** (end of paragraph)
- **r**(eplace char)
- **x** (remove char)

## CUT, COPY, PASTE
- **v**(isual one char)
- **V**(visual one line) 
- ctrl + **v**(visual block)
- **y**(ank ~ copy)
- **y**(ank) **w**(ord)
- **v**(visual) + **:w**(rite) <file>
- **d**(elete ~ cut)
- **p**(aste after cursor)
- **P**(aste before cursor)
- **g**(et) **v**(isual ~ get last visual selection) 
- **I**(nsert in visual mode) 
- :reg "2**p**(aste previously copied text)

## TIME TRAVEL 
### :earlier :ea
- **:ea**(rlier) {count}	
- **:ea**(rlier) {N}s		
- **:ea**(rlier) {N}m		
- **:ea**(rlier) {N}h		
- **:ea**(rlier) {N}d		
- **:ea**(rlier) {N}f		
			
### :later :lat
- **:lat**(er) {count}					
- **:lat**(er) {N}s					
- **:lat**(er) {N}m
- **:lat**(er) {N}h					
- **:lat**(er) {N}d					
- **:lat**(er) {N}f		
			
## SEARCH 
- **/** (search)
- **/** (search)\c (ignore case)
- **?** (search backwars)
- **n**(ext)
- **N**(previous)
- **f**(ind char)
- **%** (search '(')
- :set **hl**(highlight)**s**(earch)
- :set **no** **hl**(highlight)**s**(earch)  
- :set **i**(gnore) **c**(ase)
- :set **no** **i**(gnore) **c**(ase)
- :set **i**(nsta) **s**(earch)

## HELP 
- **:help**
- ctrl-**w**(indow)
