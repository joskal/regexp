# Regular Expressions
Una expresión regular es una secuencia de caracteres que definen un patrón de búsqueda.
La secuencia de caracteres a buscar va englobada entre dos caracteres slash `/regexp/`

## Sintaxis:
```
/regexp/mode
```
Donde `mode` puede ser uno o varios de los siguientes caracteres:
* **/regex/**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;No mode 
* **/regex/g**&nbsp;&nbsp;&nbsp;Global
* **/regex/i**&nbsp;&nbsp;&nbsp;Case insensitive 
* **/regex/s**&nbsp;&nbsp;&nbsp;Single line 
* **/regex/m**&nbsp;&nbsp;&nbsp;Multiline

## Metacharacters
Un metacarácter es un carácter que tiene un significado especial (al contrario que un carácter literal).
Los metacaracteres se usan en expresiones regulares para criterios de búsqueda y manipulación de caracteres.

Los metacaracteres básicos son los siguientes:

> ### \
> **Backslash**. Localiza un metacarácter o carácter no-alfanumérico como carácter literal. <br>
`/\$/g` :arrow_right: **$**


> ### ^ <br>
> **Negating**

> ### |

> ### . 
> **Wildcard** (Carácter comodín). Equivale a cualquier carácter literal.<br>
`/.ar/g` :arrow_right: bar tar jar par


> ### $ 

> ### ?
> **Quantifier** (Cuantificador). Localiza el carácter o grupo que le precede entre cero y una veces. <br>
`/colou?r/g` :arrow_right: color colour <br>
`/o?esophagus/g` :arrow_right: oesophagus esophagus <br>
`/jan(uary)?/g` :arrow_right: jan january

> ### * 
> **Quantifier** (Cuantificador). Localiza el carácter o grupo que le precede entre cero y más veces. <br>
`/colou*r/g` :arrow_right: color colour colouuur <br>
`/oh*/g` :arrow_right: o oh ohh ohhh ohhhh ohhhhh <br>
`/[0-9]*word/g` :arrow_right: word 1word 22word 333word 4444word

> ### + 
> **Quantifier** (Cuantificador). Localiza el carácter o grupo que le precede entre una y más veces. <br>
`/colou+r/g` :arrow_right: colour colouuur

> ### ( )

> ### [ ]
> `bat pat pad metal pan par medal cat` <br>
> `file-A file-B file-C file-D file-E file-F` <br>
> **Character set** o **Character class**. Localiza los caracteres incluidos entre `[]`en conjunción con otros.<br>
`/[bc]at/g`  :arrow_right:  bat cat <br>
`/pa[tdnr]/g`  :arrow_right:  pat pad pan par <br>
`/me[td]al/g`  :arrow_right:  metal medal<br><br>
**Character range [start-end]**. Localiza un rango de caracteres.<br>
`/file-[A-F]/g` :arrow_right:  file-A file-B file-C file-D file-E file-F <br><br>
**Negating character set or range**. Devuelve un resultado que no **[^]** coincida con el carácter o rango especificado <br>
`/file[^AB]/g` :arrow_right: file-C file-D file-E file-F <br>
`/file[^A-D]/g` :arrow_right: file-E file-F <br>


> ### { }
>**Limiting the repetition** (limitando la repetición). **{n}** Localiza el elemento precedente exactamente **n** veces.<br>
> `192882 998 288 3484848 488ASD 39222 22 333 34566 23567`<br>
> `/\d{3}/g` :arrow_right: `192 882 998 288 348 848 488 392 333 345 235`

## Shorthand character set:
```
\d  [0-9]         Localiza cualquier dígito decimal
\D  [^0-9]        Localiza cualquier carácter que no sea numérico
\w  [a-zA-Z0-9_]  Localiza cualquier carácter alfanumérico o subrayado _
\W  [^\w]         Localiza cualquier carácter no alfanumérico
\s  [\t\n\r\f\v]  Localiza espacios en blanco
\S  [^\s]         Localiza aquellos que no sean espacios en blanco
```
