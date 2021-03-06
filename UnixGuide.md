# Capítulo 1: introducción a un entorno gráfico de UNIX

### Exploración de ficheros y carpetas

Todos los exploradores de ficheros tienen una funcionalidad muy similar, permitiendo con el menú contextual (botón derecho) crear carpetas, ficheros, cambiar permisos, etc.

En la mayoría de los casos, se puede activar un modo para la escritura de rutas URI (identificador uniforme de recurso).

Un URI consta de las siguientes partes:

	1. Un identificador o protocolo seguido de “dos puntos”
	2. Un elemento jerárquico que identifica la autoridad de nombres precedido por //

En el caso de un fichero una URI válida podría ser:

	file:///home/usuario

file: → es el identificador
// → es obligatorio ponerlo
/home/usuario → es la ruta que indica en que lugar nos encontramos

En el caso de los exploradores, si no se introduce el identificador ni la // se entiende que hablamos de un fichero o carpeta en nuestro sistema: /home/usuario

Todas las rutas (path), entendiendo como ruta una URI en un sistema de ficheros, son un camino de un árbol.
Las rutas pueden ser de dos tipos:
	- Absolutas: si comienzan en /
	- Relativas: si no comienzan en /
Las rutas relativas tienen que ver con el punto en el que nos encontramos en el árbol actualmente, lo que se suele denominar como directorio actual.
Por defecto, el usuario tiene un lugar donde tiene permiso para crear, leer y ejecutar cualquier fichero y carpeta. Este lugar es denominado directorio home.


# Capítulo 2: Órdenes básicas de UNIX/Linux

Para saber que estamos trabajando con la Shell Bash tenemos que ver que en la terminal aparezca el símbolo $. Si no lo pone, debemos de escribir bash para que cambie.

### Órdenes Linux

##### man [ordenes, programas o funciones]

Es el manual de búsqueda que nos indica cómo funcionan las órdenes de UNIX.

##### ls [opciones] [directorio]

Lista los contenidos de un directorio
Opciones de ls:
	-a → muestra además los archivos ocultos que haya en el directorio (y los 		         empezados por .)
	-l → muestra un listado detallado de los archivos y directorios
	-r → muestra por pantalla los archivos ordenados en orden inverso
	-t → los muestra ordenados por fecha de modificación, los más recientes primero

##### cd [directorio]

Cambia de directorio de trabajo. Las abreviaciones . y .. se pueden utilizar como referencia de los directorios actual y padre, respectivamente. El símbolo ~ es el directorio HOME del usuario y el símbolo / al inicio de un camino es el directorio raíz del sistema.

##### pwd

Imprime el camino absoluto del directorio actual.

##### mkdir [opciones] directorio

Crea un directorio a partir del nombre dado como argumento.

Opciones de mkdir:
	-p → crea los directorios padre si son necesarios, y si ya existen no da error

##### rmdir [opciones] directorio

Borra un directorio existente (solo si está vacío).

Opciones de rmdir:
	-p → Si le damos una ruta, elimina el directorio actual y sus antecesores

##### cat [archivo(s)]

Orden mutipropósito: muestra el contenido de un archivo o varios, concatena archivos, copia un archivo, crea un archivo de texto o muestra los caracteres invisibles de control.

##### cp archivo1 archivo2

Copia el archivo1 en el archivo2. Si archivo2 no existe, se crea.

##### mv fuente destino

Renombra archivos o directorios y puede mover de lugar un archivo o directorio.

##### file archivo(s)

Muestra el tipo de archivo dado como argumento.

##### more archivo(s)

Visualiza un archivo fraccionándolo una pantalla cada vez. Antes de usar esta orden es conveniente usar la orden file para comprobar que se trata de un archivo ascii.

##### rm [opciones] directorio_archivos

Borra archivos y directorios con contenido.

Opciones de rm:
	-r → elimina directorios y sus contenidos recursivamente
	-d → elimina directorios vacíos

##### touch archivo(s)

Si existen los archivos dados como argumentos se modifican su fecha y hora a la actual. En caso contrario, se crean con la fecha actual del sistema.

Opciones de touch:
	-c → no crea ningún archivo

##### clear

Borra el contenido del terminal actual.

##### tail [opciones] [archivo(s)]

Muestra la parte final del contenido de un archivo dado como argumento. Por defecto muestra 10 líneas.

Opciones de tail:
	- -bytes=k → Muestra los últimos k bytes del archivo
	-c +k → Le quita al archivo los primeros k bytes y muestra el resto
	- - lines=k → Muestra las últimas k líneas del archivo
	-n +k → Le quita al archivo las primeras k líneas y muestra el resto

##### head [opciones] [archivo(s)]

Muestra la parte inicial del contenido de un archivo dado como argumento. Por defecto muestra 10 líneas.

Opciones de head:
	- - bytes=[-]k → Muestra los k primeros bytes de un archivo. Si utilizamos el signo '-' 			    muestra todos los bytes menos los k últimos.
	- -lines=[-]k → Muestra las k primeras líneas de un archivo. Si utilizamos el signo '-' 			  muestra todas las líneas menos las k últimas.

##### sort [opciones] [archivo(s)]

Ordena, según un criterio elegido, el contenido de los archivos dados como argumentos.

Opciones de sort:
	-b → ignora los archivos que empiezan por espacio
	-d → ordena por orden alfanumérico (primero números, después alfabéticamente, 	          y por último los caracteres especiales)
	-g → ordena primero las letras, luego los caracteres y por último los números
	-n → hace igual que el de arriba
	-R → ordena de forma aleatoria
	-r → ordena de forma inversa a la que ordena sort sin usar opciones (inverso a -d)

##### setterm -r

Reestablece el estado normal del terminal en el caso de que se visualicen caracteres extraños.

##### who

Muestra qué usuario está conectado al sistema.

### Metacaracteres de archivo

Cuando se pretende aplicar determinadas acciones a un conjunto de archivos y/o directorios cuyos nombres contienen secuencias de caracteres comunes es muy útil poder nombrarlos a través de una expresión que los pudiera identificar a todos (patrón de igualación). El patrón nos permite pasarle a la orden que vayamos a utilizar una única expresión para poder manipular todo el conjunto.

##### ?

Representa cualquier carácter simple en la posición en la que se indique.

##### *

Representa cualquier secuencia de cero o más caracteres.

##### [ ]

Designan un carácter o rango de caracteres que representan un carácter simple a través de una lista de caracteres o mediantes un rango, en cuyo caso, mostramos el primer y último carácter del rango separados por un guión “-”.

##### { }

Sustituyen conjuntos de palabras separadas por comas que comparten partes comunes.

##### ~

Se usa para abreviar el camino absoluto del directorio HOME.


# Capítulo 3: Permisos y redirecciones

### Órdenes Linux

##### chmod permiso(s) archivo(s)

Esta orden permite cambiar los permisos de acceso a un archivo.
Primero se debe indicar a qué grupo de usuarios se va a aplicar el cambio con una letra minúscula:
	u → propietario
	g → grupo
	o → resto de usuarios
	a → todos los grupos de usuarios
Después, se debe indicar si se va a permitir el acceso o se va a denegar el acceso:
	+ → permite el acceso
	- → deniega el acceso
Por último, se indica qué tipo de permiso es el que estamos modificando:
	r → permiso de lectura
	w → permiso de escritura
	x → permiso de ejecución
Justo después de esto hay que escribir el nombre del archivo al que se le van a modificar los permisos.

También es posible juntar varios cambios en una única orden chmod si lo separamos por comas.
Ejemplo: chmod u+x,g-w ej2
	     chmod ug+r ej1
	     chmod a-w ej?

##### wc [opciones] archivo(s)

Imprime por pantalla el número de líneas, de palabras y de bytes de cada archivo.

Opciones de wc:
	-c → imprime el número de bytes
	-m → imprime el número de caracteres
	-l → imprime el número de líneas
	-w → imprime el número de palabras
	-L → imprime la longitud del la línea más larga

##### echo [texto]

Muestra una línea de texto. Puede ir entrecomillado o no.

Usos de echo:
	echo $variable → para mostrar el contenido de una variable
	echo “$(orden argumento(s))” → muestra la ejecución de la orden
	echo “`orden argumento(s)`” → igual que la anterior

##### date

Muestra la fecha y la hora del sistema.

Metacaracteres de redirección

Los metacaracteres de redirección permiten alterar el flujo por defecto de entrada y salida y, por tanto, redireccionar la entrada estándar desde un archivo, y redirigir tanto la salida estándar como el error estándar hacia archivos, además de poder enlazar la salida de una orden con la entrada de otra permitiendo crear un cauce (pipelines) entre varias órdenes.

##### < nombre

Redirecciona la entrada de una orden para que la obtenga del archivo nombre.

##### > nombre

Redirige la salida de una orden para que la escriba en el archivo nombre. Si dicho archivo ya existe, lo sobreescribe. Si dicho archivo no existe, lo crea.

##### &> nombre

La salida estándar se combina con la salida de error estándar y ambas se escriben en el archivo nombre.

##### >> nombre

Funciona igual que el metacarácter “>” pero añade la salida estándar al final del contenido del archivo nombre.

##### &>> nombre

Igual que el metacarácter “&>”, pero añadiendo las dos salidas combinadas al final del archivo nombre.

##### 2> nombre

Redirige la salida de error estándar a un archivo (sólo funciona en shells de “bash”).

##### |

Crea un cauce entre dos órdenes. La salida de una de ellas se utiliza como entrada de la otra. Se va leyendo de izquierda a derecha.

##### |&

Crea un cauce entre dos órdenes utilizando las dos salidas (estándar y error) de una de ellas como entrada de la otra.

### Metacaracteres sintácticos

Sirven para combinar varias órdenes y construir una única orden lógica.

##### ;

Separador entre órdenes que se ejecutan secuencialmente.

##### ( )

Se usan para aislar órdenes separadas por “;” o por “|”. Las órdenes dentro de los paréntesis son tratadas como una única orden.

##### &&

Separador entre órdenes, en la que la orden que sigue al metacarácter “&&” se ejecuta sólo si la orden precedente ha tenido éxito (no ha habido errores).

##### | |

Separador entre órdenes, en la que la orden que sigue la metacarácter “| |” se ejecuta sólo si la orden precedente falla.


# Capítulo 4: Variables, alias, órdenes de búsqueda y guiones

### ¿Cómo se crean variables?

variable=expresion
vector=(elemento1 elemento2 elemento3)
variable=`orden o expresion`

### Órdenes Linux

##### env

Muestra todas las variables de entorno o globales que hay definidas y que son comunes a todos los shells.

##### printenv

Realiza lo mismo que la orden anterior.

##### set

Muestra las variables locales que están definidas en la shell actual.

##### help variables

Muestra el nombre y el significado de algunas variables del shell.

##### unset nombre_de_variables

Elimina las variables listadas.

##### declare [opciones] [variable]=[expresion]

Se utiliza para crear variables con ciertos atributos (tipo numérica, etc.).

Opciones de declare:
	-i → Se utiliza para definir variables de números enteros
	-p → Se utiliza para mostrar los atributos de la variable indicada
	-g → Se utiliza para crear una variable que sea global

##### export variable

Con esta orden podemos exportar las variables que sean locales para poder utilizarlas en otras shells distintas de la actual.

##### expr expresion

Evalúa la expresión dada, ya sea matemática o lógica.

##### printf formato [argumentos o mensaje]

Imprime un mensaje en la pantalla utilizando el formato que se le especifica.

Secuencia de escape:
	\b → Espacio atrás
	\n → Nueva línea
	\t → Tabulador
	\' → Carácter comilla simple
	\\ → Carácter barra invertida
	\0n → n = número en octal que representa un carácter ASCII de 8 bits

Código de formato:
	%d → Un número con signo
	%f → Un número en coma flotante (decimal) sin notación exponencial
	%q → Entrecomilla una cadena
	%s → Muestra una cadena sin entrecomillar
	%x → Muestra un número en hexadecimal
	%o → Muestra un número en octal

##### alias nombre='orden'

Se utiliza para definir un comportamiento por defecto de una orden o cambiar el nombre de una orden por estar acostumbrado a usar otro sistema.

##### unalias nombre_del_alias

Borra o elimina un alias definido previamente.

##### find lista_de_directorios [expresiones]

Sirve para buscar archivos en función de las características externas de éste, que pueden ser el tamaño, el nombre, la último fecha de modificación, etc.

Opciones de find:
	-name “[nombre_archivo]” → Busca los archivos que tienen el nombre_archivo. Se 	pueden utilizar metacaracteres de archivo para buscar los que tengan algo en 	común.
	-atime [[signo]k] → Busca los archivos a los que se accedió hace justo k días, hace 	menos de k días (signo -) o hace más de k días (+k).
	-type [letra] → Busca archivos de un determinado tipo. Si la letra es f busca 	archivos regulares, si es d busca directorios. (Hay otras opciones pero menos 	útiles. Se puede ver en el man find).
	-size [[signo]n][letra] → Busca archivos con n bloques de memoria, con menos de n 	bloques de memoria (-n) o con más de n bloques de memoria (+n). Además, si justo 	seguido del número se pone una letra la búsqueda se puede hacer en función de 	los bytes del documento:
		c: el tamaño es en bytes
		k: el tamaño es en kilobytes
		M: el tamaño es en megabytes
		G: el tamaño es en gigabytes
	Se pueden utilizar comando lógicos como la negación (!), la conjunción (-a) o la 	disyunción (-o).

##### grep [opciones] patron_de_búsqueda archivos

Ejemplo: `grep manolo $HOME/Escritorio/*``

Sirve para buscar en el interior de los archivos, es decir, para algún dato o cualquier otra cosa que esté escrita en el interior de un archivo.

Opciones de grep:
	-x
	-v
	-c
	-i
	-n
	-l
	-e

### Variables especiales

***$BASH*** → Contiene la ruta de acceso completa usada para ejecutar la instancia actual de bash.

***$HOME*** → Almacena el directorio raíz del usuario; se puede emplear junto con la orden cd sin argumentos para ir al directorio raíz del usuario.

***$PATH*** → Guarda el camino de búsqueda de las órdenes, este camino está formado por una lista de todos los directorios en los que queremos buscar una orden.

***$?*** → Contiene el código de retorno de la última orden ejecutada, bien sea una instrucción o un guión. Sale 0 si se ejecutó correctamente, o 1 si hubo algún error. (Hay que utilizarla precedida de echo).


# Capítulo 5: Expresiones con variables y expresiones regulares

### Expresiones con variables

$(( … ))
$[ … ]

Se utilizan para calcular expresiones.

### Operadores aritméticos

```bash
+	-	*	/	%	**	++	- -	( )	,	=
+=	-=	*=	/=	%=
```

### Operadores relacionales

```bash
=	==	-eq	!=	-ne	<	-lt	>	-gt	<=	-le	>=	-ge
!	&&	| |
```

### Comparaciones aritméticas y entre cadenas de caracteres

### Órdenes Linux

###### bc

Hace cálculos con una precisión decimal arbitraria.

Opciones de bc:
	-l → Muestra los números decimales en una división

let variable=expresión

Evalúa expresiones aritméticas.

Orden de los operadores que admite, en orden decreciente de precedencia:
```bash
id++, id--	post-incremento, post-decremento de variable
++id, --id	pre-incremento, pre-decremento de variable
-, +		menos, más unitarios
!, ~		Y logico y negacion binaria
**		exponenciación
*, /, %		multiplicación, división, resto
+, -		suma, resta
<<, >>		desplazamientos de bits a izquierda y derecha
<=, >=, <, >	comparación
==, !=		igualdad, desigualdad
&		Y binario
^		XOR binario
|		O binario
&&		Y lógico
||		O lógico
expr ? expr : expr	operador condicional
=, *=, /=, %=,
+=, -=, <<=, >>=,
&=, ^=, |=	asignación
```

###### test [ expresion ]

Esta orden evalúa una expresión condicional y da como salida el estado 0, en caso de que expresión se haya evaluado como verdadera, o el estado 1, si la evaluación ha resultado falsa o se le dio algún argumento no válido.

### Expresiones de test: (copiar de las prácticas)

```bash
if condición;
then
	declaraciones;
[elif condición;
	then declaraciones; ]...
[else
	declaraciones; ]
fi
```

Esta orden ejecuta una lista de declaraciones dependiendo de si cumple o no cierta condición.

***TO BE CONTINUED...***
