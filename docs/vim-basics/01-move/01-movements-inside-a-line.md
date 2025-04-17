# Movements - Within a Line

Let's learn the basic skills to move withing a line.

## Jump by words in the same line - using motions

- 1. Jump from word to word : w
- 2. Jump back word to word : b
- 3. Jump to end of word : e
- 4. Jump to end of word back : ge
- Words in vim doesn't include . ( {
- To include them use capital equivalents of the above 1 to 4 like w, B, E, gE


## Move to horizontal extremes
- 0 Move to the first character of a line
- ^ Move to the first non-blank char of a line
- $ Move to the end of a line
- g_ Move to the non-blank char at the end of a line


## Move to specific charracter - IN A LINE

- Use f{char} to move to the next occurence of char
- Use F{char} to move to the prev occurence of char
- Use t{char} to move to just b 4 the next occurence of char
- After using f{char} your can type : to next occurence or , to go to prev occurence
