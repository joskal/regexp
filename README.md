# Regular Expressions
Una expresión regular es una secuencia de caracteres que definen un patrón de búsqueda.
La secuencia de caracteres a buscar va englobada entre dos caracteres slash `/regexp/`

## Sintaxis:
```
/regexp/mode
```
Donde `mode` puede ser uno o varios de los siguientes caracteres: 
* `/regex/g` Global
* `/regex/i` Case insensitive 
* `/regex/s` Single line 
* `/regex/m` Multiline

## Metacharacters
Un metacarácter es un carácter que tiene un significado especial (al contrario que un carácter literal).
Los metacaracteres se usan en expresiones regulares para criterios de búsqueda y manipulación de caracteres.

Los metacaracteres básicos son los siguientes:

> # \
> **Backslash**. Localiza un metacarácter o carácter no-alfanumérico como carácter literal. <br>
`!@#$%^&*()_+1234567890abcdef` <br>
`/\$/g` :arrow_right: `$`

<hr>

> # ^ <br>
> **Anchor** (Anclaje). Devuelve un resultado que coincida con el carácter o rango especificado y que esté al comienzo de la línea. <br>
> `file01begin file02 file03 file02 file01end` <br>
> `/^file01[a-z]+/g` :arrow_right: `file01begin`

<hr>

> # $
> **Anchor** (Anclaje). Devuelve un resultado que coincida con el carácter o rango especificado y que esté al final de la línea.<br>
> `file01begin file02 file03 file02 file01end` <br>
> `/file01[a-z]+$/g` :arrow_right: `file01end`

<hr>

> # |
> **Alternation**. Es similar al `[character set]` pero alternando secuencias completas dentro de grupos.
>
> `alternar.com alternar.net alternar.es`<br>
>`/alternar\.(com|es)/g` :arrow_right: `alternar.com alternar.es`

<hr>

> # . 
> **Wildcard** (Carácter comodín). Equivale a cualquier carácter literal.<br>
`/.ar/g` :arrow_right: bar tar jar par

<hr>

> # ?
> **Quantifier** (Cuantificador). Localiza el carácter o grupo que le precede entre cero y una veces. <br>
`color colour oesophagus esophagus jan january` <br>
`/colou?r/g` :arrow_right: `color colour` <br>
`/o?esophagus/g` :arrow_right: `oesophagus esophagus` <br>
`/jan(uary)?/g` :arrow_right: `jan january`

<hr>

> # * 
> **Quantifier** (Cuantificador). Localiza el carácter o grupo que le precede entre cero y más veces. <br>
`word 1word 22word 333word 4444word o oh ohh ohhh ohhhh ohhhhh color colour colouuur`
`/colou*r/g` :arrow_right: `color colour colouuur` <br>
`/oh*/g` :arrow_right: `o oh ohh ohhh ohhhh ohhhhh` <br>
`/[0-9]*word/g` :arrow_right: `word 1word 22word 333word 4444word`

<hr>

> # + 
> **Quantifier** (Cuantificador). Localiza el carácter o grupo que le precede entre una y más veces. <br>
`/colou+r/g` :arrow_right: colour colouuur

<hr>

> # [ ]
> `bat pat pad metal pan par medal cat` <br>
> `file-A file-B file-C file-D file-E file-F` <br><br>
> **Character set** o **Character class**. Localiza los caracteres incluidos entre `[]`en conjunción con otros.<br>
`/[bc]at/g`  :arrow_right:  bat cat <br>
`/pa[tdnr]/g`  :arrow_right:  pat pad pan par <br>
`/me[td]al/g`  :arrow_right:  metal medal<br><br>
**Character range [start-end]**. Localiza un rango de caracteres.<br>
`/file-[A-F]/g` :arrow_right:  file-A file-B file-C file-D file-E file-F <br><br>
**Negating character set or range**. Devuelve un resultado que no **[^]** coincida con el carácter o rango especificado <br>
`/file[^AB]/g` :arrow_right: file-C file-D file-E file-F <br>
`/file[^A-D]/g` :arrow_right: file-E file-F <br>

<hr>

> # { }
> `192882 998 288 3484848 488ASD 39222 22 333 34566 23567`<br> <br>
> **Limiting the repetition** (limitando la repetición).<br> 
> **{n}** Localiza el elemento precedente exactamente **n** veces.<br>
> `/\d{3}/g` :arrow_right: `192 882 998 288 348 848 488 392 333 345 235`<br>
> **{mín,}** Localiza el elemento precedente al menos un **mín**imo veces.<br>
> **{mín,máx}** Localiza el elemento precedente al menos un **mín**imo veces y no más de un **máx**imo veces.<br>

<hr>

> # (group)
> **Grouping**
> Podemos agrupar caracteres bajo esta forma **(group)**, para así tratarlo como un cuantificador.
> 
> `impossible possible possibles impossibles`<br>
> `/(im)?possible/g` :arrow_right: `impossible possible possibles impossibles`<br>
> `/\b(im)?possible\b/g` :arrow_right: `impossible possible`
>
>También podemos referenciar grupos numéricamente. Cada grupo que definamos está numerado internamente. La numeración comienza en `\1`.
>
> `123-567-8901-123`<br>
> `/(\d{3})-(\d{3})-(\d{4})-\1/g` :arrow_right: `123-567-8901-123`
>
> Mostrar dos palabras iguales consecutivas.
> ```
> near near is the city
> clear clear is the sky
> ```
> `/\b(\w+)\b\s+\1/g` :arrow_right: `near near clear clear`

<hr>

## Shorthand character set:
```
\d  [0-9]                 Localiza cualquier dígito decimal
\D  [^0-9]                Localiza cualquier carácter que no sea numérico
\w  [a-zA-Z0-9_]          Localiza cualquier carácter alfanumérico o subrayado _
\W  [^\w]                 Localiza cualquier carácter no alfanumérico
\s  [\t\n\r\f\v]          Localiza espacios en blanco
\S  [^\s]                 Localiza aquellos que no sean espacios en blanco
\b  (^\w|\w$|\W\w|\w\W)   Boundary. Localiza palabra completa \bpalabra\b
```

## Boundary 
Consiste en buscar palabras completas mediante la secuencia `/bpalabra/b`.

`gato perros cerdo vaca gata gatito gatitas gat agata eagle alma `<br>

Localizar palabras de cuatro caracteres de la lista.<br>
`/\b\w{4}\b/g` :arrow_right: `gato vaca gata`

Localizar palabras que comiencen por `gat`<br>
`/\bgat[a-z]+\b/g` :arrow_right: `gato gata gatito gatitas`

Muestra las palabras que comiencen por vocal<br>
`/\b[aeiou][a-z]+\b/g` :arrow_right: `agata eagle alma`
