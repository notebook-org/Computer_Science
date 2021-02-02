# Vim
* [Notes](./vim.pdf)
## Additional Nodes:
* A                 --> Append at the End.
* Ctrl + g          --> Display the name of the current file
* .                 --> To repeat the previous commands
* c                 --> (Change) Delete and enter into insert mode
* \>                 --> Indent Forward
* <                 --> Indent Backward
* :<Line Number\>   --> Goto <Line Number\>
* ctrl + r <reg no\>--> Paste from register
* m<char\>          --> Set marker at the current cursor location and with key <char/> 
* '<char\>          --> Goto marker with key <char\>
## Auto completion
* Ctrl + p          --> Search previous for auto-completion
* Ctrl + n          --> Search next for auto-completion
## Nouns in vim
1. Text Object
  * iw              --> Inner word
  * it              --> Inner tag
  * i"              --> Inner quotes
  * ip              --> Inner paragraph  
  * as              --> A Sentence
2. Parametrized text object
  * f             --> find the next character
  * t             --> find the next character
  * /             --> Search upto next match
## Surround Plugin
* cs"'            --> Change surround from " to '
* ds"             --> Delete surround "
* ysiw"           --> Add surround to word "
## vim-commentary Plugin
* gcl             --> Comment line
