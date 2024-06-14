  

+++
title = 'Comandos Basicos en Linux - Parte 1'
description = "Introduccion para comenzar a usar sistemas GNU/Linux como un chad"
date = 2024-01-10
categories = [
    "Linux",
    "bash",
]
  
image = "wallpaper.jpg"
+++


En esta ocasión, como se menciona en el título, vamos a adentrarnos en el mundo de Linux. Este post está dirigido a aquellos que son nuevos en este sistema operativo, con el fin de ayudarles y guiarlos en el uso de la terminal sin temor a romper algo con algún comando.  

Este post será muy práctico, y para ello me guiaré de una página que considero increíble para aprender sobre los comandos en Linux. Para dar un breve resumen, esta página consiste en un juego de desafios en seguridad informatica. Tendrás que usar comandos en Linux para encontrar un archivo .txt donde se encuentra una contraseña para un usuario. A medida que subes de nivel, la dificultad aumenta. Para avanzar, deberás encontrar una "flag" para cada usuario, lo que representa los diferentes niveles y la flag la contraseña de acceso a los mismos.

Espero que este post te sea de gran ayuda y te anime a explorar más sobre el fascinante mundo de Linux. ¡Empecemos!

Nos diriguimos a la siguiente pagina [over the wire](https://overthewire.org/wargames/bandit/), nos llevara a esta pagina:

![Menu](/content/post/BasicCommandsOnLinuxPart1/img/level0/Menu.png)

# Level 0 -> Level 1

Aquí puedes leer más sobre lo que trata Bandit y en qué consiste. Nos dirigiremos al nivel 0, donde podemos ver las instrucciones para acceder como bandit0 y conectarnos al servidor mediante el comando SSH. Una vez que hemos leído las instrucciones, pasamos al siguiente nivel. En el siguiente nivel, podemos observar que nos dan las siguientes instrucciones.

![bandit0](/content/post/BasicCommandsOnLinuxPart1/img/level0/bandit0.png)

Aquí ya podemos observar que las instrucciones nos indican que la contraseña para el siguiente nivel se encuentra en un archivo llamado "_readme_", localizado en el directorio home de nuestro usuario "_bandit0_". Vamos a confirmarlo. Como aún no me he conectado al juego, vamos a hacerlo.

En el nivel 0 se especifica que se debe usar `ssh` para acceder al servidor. Nos proporcionan un nombre de host, un puerto y la contraseña. La estructura del comando para acceder al nivel cero es la siguiente: `ssh bandit0@bandit.labs.overthewire.org -p 2220`. Si es nuestra primera vez usando el comando ssh, nos preguntará si estamos seguros de acceder al servidor. Entonces, escribimos 'Y/y' o simplemente "yes". A continuación, nos pedirá la contraseña del usuario bandit0, la cual es **bandit0**.

Una vez dentro del servidor, comprobamos que somos el usuario bandit0 con el comando `whoami`. Este comando nos sirve para saber qué usuario está usando el sistema actualmente y, si todo está bien, podemos observar claramente que se trata del usuario "bandit0". Posteriormente, escribimos el comando `ls` para listar el contenido de nuestro directorio home y ahí es donde se encuentra el archivo "_readme_" que contiene la contraseña para acceder a "bandit1". Escribimos el comando `cat readme` para leer el contenido de este archivo y, como se puede observar, esa es la contraseña para el siguiente nivel, la copiamos en nuestro portapapeles y del servidor con el comando `exit`

![level0](/content/post/BasicCommandsOnLinuxPart1/img/level0/level0.png)

# Level 1 -> Level 2

Para el siguiente nivel, vamos a acceder como bandit1. Vamos a usar el mismo comando que usamos anteriormente con bandit0, pero cambiando el usuario. El comando es el siguiente: `ssh bandit1@bandit.labs.overthewire.org -p 2220`. La única diferencia será el número del usuario, todo lo demás se mantiene igual. Accedemos y, una vez que nos pida la contraseña y pegamos la que habíamos guardado anteriormente en nuestro portapapeles.

Las instrucciones para el siguiente nivel son las siguientes.

![instructions_level1](/content/post/BasicCommandsOnLinuxPart1/img/level1/instructions_level1.png)

Nos especifica que la contraseña está guardada en un archivo localizado en el directorio home con el nombre '-'.

El desafío parece simple, pero el problema surge cuando escribimos el comando `cat -`. Este se queda en espera, ya que lo toma como si fuera un parámetro de `cat`. Entonces, ¿cómo solucionamos esto? Para poder resolver este desafío, podemos hacerlo de varias formas:

1. **Desde la ruta absoluta:** `cat /home/bandit1/-`. De esta forma, indicamos la ruta completa del archivo, evitando que `cat` lo confunda con un parámetro.

1. **Forma alternativa:** `cat $(pwd)/-`. Usando este método, nos ahorramos escribir toda la ruta. El comando `pwd` nos da la ruta actual, y usamos esa salida para que `cat` interprete correctamente la ubicación del archivo. Esto se especifica usando los símbolos `$()`.

2. **Indicando la ruta actual:** `cat ./-`. De esta forma, indicamos que desde la ruta actual en la que nos encontramos (representada por un punto), y se lee el archivo con el nombre "-".

Observamos que, de cualquiera de estas maneras, obtenemos la contraseña.

![level1](/content/post/BasicCommandsOnLinuxPart1/img/level1/level1.png)

Aqui conluimos con este nivel, nos salimos y accedemos al siguiente.

# Level 2 -> level 3

![instructions](/content/post/BasicCommandsOnLinuxPart1/img/level2/instructions.png)

Para este nivel, observamos que hay un archivo llamado "_spaces in this filename_". Para poder leer este tipo de archivos con espacios, necesitamos escapar cada espacio con el carácter especial barra inversa `\`, quedando así el comando: `cat spaces\ in\ this\ filename`. De igual forma, podemos ahorrarnos esto usando la tecla tab, la cual nos autocompleta lo mencionado anteriormente.

Otra forma de hacer este proceso es usando comillas dobles, quedando de esta manera: `cat "spaces in this filename"`. De esta forma, le indicamos el nombre del archivo.

Pero además de hacer eso, también podemos ahorrarnos escribir el nombre. Para hacer esto más rápido, hacemos uso del carácter especial asterisco `*`, el cual interpreta cualquier cosa, quedando así el comando: `cat *filename`. De esta forma, le indicamos que queremos leer todos los archivos que terminen en "filename". Igualmente, se puede modificar el orden del asterisco, por ejemplo: `cat spaces*`, aquí se indica que queremos leer todos los archivos que comiencen con el nombre "spaces". Cabe aclarar que este comando es mejor usarlo cuando sabemos que solo existe un archivo con ese nombre; en caso contrario, listará el contenido de todos los archivos que encuentre.

![level2](/content/post/BasicCommandsOnLinuxPart1/img/level2/level2.png)

Ahora que tenemos la contraseña nos dirigimos al siguiente nivel.

# Level 3 -> Level 4

Para este nivel la contraseña esta guardada en un archivo oculto dentro del directorio "inhere"

Este nivel es muy simple, si listamos el contenido de la carpeta con el comando `ls`, sabremos que a simple vista nos e ve nada, para ello vamos a hacer uso de los parametros de dicho comando, usaremos el parametro `-a` para listar todo lo que se encuentre a dentro quedando asi el comando: `ls -a inhere`. Y ahora podemos observar que hay un archivo con el nombre "...Hiding-From-You", con el comando cat revisamos el contenido y tendremos la contraseña.

![download.png](/content/post/BasicCommandsOnLinuxPart1/img/level3/download.png)

# Level 4 -> level 5

Para este nivel, se nos indica que la contraseña está guardada en un archivo humanamente legible, dentro del directorio "inhere".

Si listamos el contenido del directorio, podemos notar que hay múltiples archivos con distintos nombres. Dado que no todos tienen contenido legible y para evitar abrir e inspeccionar uno por uno, vamos a identificar el archivo correcto con los comandos `file` y `find`.  

El comando `file` nos permite saber la clasificación de cada archivo: si es una imagen, un archivo de texto, un binario, un video, etc. El comando `find` es una alternativa al comando `ls`, con la diferencia de que `find` busca desde la raíz de la ruta que se le pase. Por ejemplo, si escribimos el comando `find inhere`, este nos listará el contenido en forma de lista usando un formato de árbol binario.

Lo que vamos a hacer a continuación es combinar los comandos `find` y `file`. ¿Y cómo hacemos eso? Fácil, con el comando `xargs` y el uso del carácter "pipe" `|`.

El comando `xargs` lee los argumentos desde la entrada estándar. Por ejemplo, si nosotros escribimos el siguiente comando:

`echo "file1.txt file2.txt file3.txt" | xargs touch`

Esto creará los archivos `file1.txt`, `file2.txt`, y `file3.txt`

![ejemplo.png](/content/post/BasicCommandsOnLinuxPart1/img/level4/ejemplo.png)

Lo que estamos haciendo es lo siguiente: dada la salida del comando `echo`, queremos crear archivos con el nombre de dicha salida. Entonces, se ejecuta `xargs touch` y el resultado es que se crean tres archivos con los nombres `file1.txt`, `file2.txt`, etc.

Usando el carácter "or/pipe" `|`, que es un carácter especial, se puede hacer que la salida de un comando sea la entrada de otro comando.

Bien, una vez explicado esto, utilizamos lo que sabemos con el comando `find`. Vamos a ejecutar la siguiente instrucción: `find . | xargs file`. Usamos el punto `.` en el comando `find` para especificar que queremos que busque archivos desde la ruta en la que estamos.

Si seguimos los pasos hasta aquí, ya tendremos listados todos los archivos y notamos que hay uno que es de tipo ASCII. Es el único dentro del directorio `inhere`. Por lo tanto, abrimos ese archivo con el comando `cat` y observamos que contiene la contraseña para el siguiente nivel.

![level4](/content/post/BasicCommandsOnLinuxPart1/img/level4/level4.png)

# Level 5 -> 6

Para este nivel, las instrucciones mencionan que el archivo que guarda la contraseña está en algún lugar dentro del directorio "inhere" y tiene las siguientes propiedades:

- Es humanamente legible.

- Tiene un tamaño de 1033 bytes.

- No es un archivo ejecutable.

Vamos a usar el comando `find`, ya que este comando tiene parámetros que nos pueden ayudar a encontrar el archivo siguiendo estas propiedades.

El comando que vamos a utilizar es el siguiente:

`find inhere/ -readable -size 1033c ! -executable`.

El parámetro `-readable` busca un archivo que sea legible. Con el parámetro `-size` especificamos que sea de un determinado tamaño; puede ser en megas, gigas, etc., pero en esta ocasión es en bytes, por lo tanto, se usa la letra 'c'. El carácter `!` es para negar una condición, así que especificamos que no queremos que sea ejecutable. Si quitamos el signo de exclamación, le estamos indicando que queremos que sea ejecutable.

Al ejecutar el comando, podemos ver que nos da un output de un archivo en la carpeta "maybehere07", dentro del archivo ".file2". Entonces, tenemos varias formas de leer este archivo.

Usando `cat` como lo haría un chad promedio, el comando es el siguiente:

`cat $(find inhere/ -readable -size 1033c ! -executable)`

Usando `cat` de manera normal, el siguiente comando seria este:

`cat inhere/maybehere07/.file2`

![metodos.png](/content/post/BasicCommandsOnLinuxPart1/img/level5/metodos.png)

Ambas maneras nos daran la contraseña, de igual manera puedes seguir buscando para tener un formato mas limpio con el comando xargs, como se ve a continuacion.

![ejemplo](/content/post/BasicCommandsOnLinuxPart1/img/level5/ejemplo.png)

Una vez obtuvimos la contraseña nos vamos para el siguiente nivel.  

HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

# Level 6 -> 7

En construccion . . .