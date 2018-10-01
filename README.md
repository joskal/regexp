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

### \
> Localiza un metacarácter o carácter no-alfanumérico como carácter literal <br>
`/\$/g` Busca el signo **$** en el texto.


### ^
### |
### . 
> Carácter comodín (wildcard). Equivale a cualquier carácter literal.<br>
`/./g`


### $ 
### ? 
### * 
### + 
### ( )
### [ ]
### { }

Otros metacaracteres:
```
\d    Localiza cualquier dígito decimal
\D    Localiza cualquier carácter que no sea numérico
\w    Localiza cualquier carácter alfanumérico
\W    Localiza cualquier carácter no alfanumérico
\s    Localiza espacio en blanco
\S    Localiza aquellos que no sean espacios en blanco
```
