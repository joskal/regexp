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

> # . 
> **Wildcard** (Carácter comodín). Equivale a cualquier carácter literal.<br>
`/.ar/g` :arrow_right: bar tar jar par

<hr>

> # ^ $
> **Anchors** (Anclajes)
> ```
> file01begin file02 file03 file02 file01end
> ```
> ## ^
> Devuelve un resultado que coincida con el carácter o rango especificado y que esté al comienzo de la línea. <br>
> `/^file01[a-z]+/g` :arrow_right: `file01begin`
>
> ## $
> Devuelve un resultado que coincida con el carácter o rango especificado y que esté al final de la línea.<br>
> `/file01[a-z]+$/g` :arrow_right: `file01end`

<hr>

> # ? * +
> **Quantifiers** (Cuantificadores). 
> ```
> color colour oesophagus esophagus 
> jan january
> word 1word 22word 333word 4444word 
> o oh ohh ohhh ohhhh ohhhhh
> color colour colouuur
> ```
> ## ?
>Localiza el carácter o grupo que le precede entre cero y una veces. <br>
> `/colou?r/g` :arrow_right: `color colour` <br>
> `/o?esophagus/g` :arrow_right: `oesophagus esophagus` <br>
> `/jan(uary)?/g` :arrow_right: `jan january`
> 
> ## * 
> Localiza el carácter o grupo que le precede entre cero y más veces. <br>
> `/colou*r/g` :arrow_right: `color` `colour` `colouuur` <br>
> `/oh*/g` :arrow_right: `o` `oh` `ohh` `ohhh` `ohhhh` `ohhhhh` <br>
> `/[0-9]*word/g` :arrow_right: `word` `1word` `22word` `333word` `4444word`
> 
> ## + 
> Localiza el carácter o grupo que le precede entre una y más veces. <br>
> `/colou+r/g` :arrow_right: `colour` `colouuur`

<hr>

> # [character-set]
> **Character set** or **Character class**. Localiza los caracteres especificados en conjunción con otros.<br>
> ```
> bat pat pad metal pan par medal cat
> file-A file-B file-C file-D file-E file-F
>```
> `/[bc]at/g`  :arrow_right:  `bat cat` <br>
> `/pa[tdnr]/g`  :arrow_right:  `pat pad pan par` <br>
> `/me[td]al/g`  :arrow_right:  `metal medal` <br><br>
> **Character range [start-end]**. Localiza un rango de caracteres.<br>
> `/file-[A-F]/g` :arrow_right:  `file-A` `file-B` `file-C` `file-D` `file-E` `file-F` <br><br>
> **Negating character set or range**. Devuelve un resultado que no **[^]** coincida con el carácter o rango especificado <br>
> `/file[^AB]/g` :arrow_right: `file-C` `file-D` `file-E` `file-F` <br>
> `/file[^A-D]/g` :arrow_right: `file-E` `file-F` <br>

<hr>

> # {n} {min,} {min,max}
> **Limiting the repetition** (limitando la repetición).<br> 
> `192882 998 288 3484848 488ASD 39222 22 333 34566 23567`<br> <br>
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
> `/\b(\w+)\b\s+\1/g` :arrow_right: `near near` `clear clear`<br>
> 
> **(?:group)** Non capturing group. Consiste en saltar la numeración de un grupo en concreto.
> ```
> I like seat and peugeot and seat
> I like seat and peugeot and peugeot
> ```
> `/I like (seat) and (peugeot) and \1/g` :arrow_right: `I like seat and peugeot and seat`<br>
> `/I like (?:seat) and (peugeot) and \1/g` :arrow_right: `I like seat and peugeot and peugeot`<br>

<hr>

> # |
> **Alternation**. Operador `OR`. Es similar al `[character set]` pero operando con secuencias completas dentro de `(grupos)`.
>
> ```
> alternar.com alternar.net alternar.es alternar.org
> gray grey
> hardworking man hardworking lady
> file.txt files12.xlsx file123.docx fileabc.pptx
> ```
>`/alternar\.(com|es|org)/g` :arrow_right: `alternar.com alternar.es alternar.org`<br>
>`/gr[ae]y/g` :arrow_right: `/gr(a|e)y/g` :arrow_right: `gray grey`<br>
>`/hardworking (man|lady)/g` :arrow_right: `hardworking man hardworking lady`<br>
> `/file\w*\.(txt|xlsx|docx|pptx)/g` :arrow_right: `file.txt files12.xlsx file123.docx fileabc.pptx` 
>
>**Nested Alternation**. Alternación anidada.
>```
> toyota 1600cc
> toyota 2400cc
> toyota 2000cc
> honda 1000cc
> honda 2400cc
> honda 5000cc
> ```
> `/(toyota (1600cc|2000cc)|honda (2400cc|5000cc))/g` :arrow_right: `toyota 1600cc` `toyota 2000cc` `honda 2400cc` `honda 5000cc`

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

<hr>

## Greedy Regex vs Lazy Regex
```
<h1>heading</h1>
"rebelion" and "revolution"
```
Por defecto, los cuantificadores `= ? *` son de ámbito ambicioso (**greedy**); esto quiere decir que abarcará desde la primera hasta la última coincidencia seleccionando todo lo que haya por medio.

`/<.+>/g` :arrow_right: `<h1>heading</h1>`<br>
`/".+"/g` :arrow_right: `"rebelion" and "revolution"`

Sin embargo podemos hacer uso del ámbito perezoso (**lazy**) acotando aún más la búsqueda al indicarle que seleccione hasta la siguiente coincidencia.

`/<.+?>/g` :arrow_right: `<[^>]+>` :arrow_right: `<h1>` `</h1>`<br>
`/".+?"/g` :arrow_right: `"[^"]+"` :arrow_right: `"rebelion"` `"revolution"`

## Boundary 
Consiste en buscar palabras completas mediante la secuencia `/bpalabra/b`.

`gato perros cerdo vaca gata gatito gatitas gat agata eagle alma `<br>

Localizar palabras de cuatro caracteres de la lista.<br>
`/\b\w{4}\b/g` :arrow_right: `gato vaca gata`

Localizar palabras que comiencen por `gat`<br>
`/\bgat[a-z]+\b/g` :arrow_right: `gato gata gatito gatitas`

Muestra las palabras que comiencen por vocal<br>
`/\b[aeiou][a-z]+\b/g` :arrow_right: `agata eagle alma`

<hr>

## Assertions Lookaround
Esta técnica consiste en localizar un contexto alrededor de una palabra que puede ser hacia delante **(Lookahead)** o hacia atrás **(Lookbehind)**. El resultado que devuelve es la coincidencia buscada pero sin el contexto utilizado.
## **?=**
**Positive Lookahead Assertion**. Operador `==` en torno a la coincidencia hacia adelante.
```
bill paid
bill not paid
bill paid
bill paid
```
Buscar `bill` en el contexto de `bill paid`<br>
`/bill(?=\spaid)/g` :arrow_right: `bill` `bill` `bill` resultado: 3 coincidencias.

```
100 USD
150 JPY
900 YUA
750 ITL
800 USD
```
Buscar cantidades expresadas en `USD`<br>
`/\d+(?=\sUSD)/g` :arrow_right: `100` `800`

## **?!**
**Negative Lookahead Assertion**. Operador `!=` en torno a la coincidencia hacia adelante.

Buscar cantidades de 3 cifras que no estén en `USD` ni en `JPY`<br>
`/\d{3}+(?!\sUSD|JPY)/g` :arrow_right: `900` `750`

## ?<=
**Positive Lookbehind Assertion**. Operador `==` en torno a la coincidencia hacia atrás.
```
social worker
hard worker
lazy worker
poor worker
intelligent worker
```
Buscar `worker` en el contexto `social` hacia atrás.<br>
`/(?<=social)\sworker/g` :arrow_right: `worker` resultado: 1 coincidencia.

## ?<!
**Negative Lookbehind Assertion**. Operador `!=` en torno a la coincidencia hacia atrás.<br>
Buscar `worker` que no estén en el contexto `social` ni en `hard`, hacia atrás.<br>
`/(?<!social|hard)\sworker/g` :arrow_right: `worker` `worker` `worker` resultado: 3 coincidencias.


<hr>

## Ejemplos
### 1 - Buscar fechas en distintos formatos.
```
12 - 8 - 2013
8/12/2011
9 -9 - 2012
3/12/2008
4-2-2002
```
`/\d{1,2}\s*[-\/]\s*\d{1,2}\s*[-\/]\s*\d{4}/g`
