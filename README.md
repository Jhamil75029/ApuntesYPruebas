# Apuntes del Curso
Hecho por Jhamil Arnez Hidalgo
## Clase 1 - Introducción
Git es un Sistema de Control de versiones distribuido, distribuido ya que todos los miembros del equipo tendrán una copia del proyecto, es decir que la persistencia del proyecto no depende de un servidor central que si falla se pierde todo, sino de muchas personas. 
El creador de git es Linus Torvalds, el mismo que creó Linux, porque ningún sistema de control de versiones en su momento le convencieron, así que decidió crear el suyo.
### Instalación
#### Linux: 
Para instalar git en linux es tan simple como colocar en la terminal:
_sudo apt install git_ 
y muchas distros de linux ya traen git incluso, a veces solo es necesario actualizarlo

#### Windows:
Se busca Git en nuestro navegador de preferencia, se va a la pestaña de git install, damos click y esperamos a que se instale un instalador. Una vez descargado, lo ejecutamos con doble click, normalmente se le da a todo next, hasta la parte en la que nos ofrece como nombre predeterminado de la rama principal master, cambiamos a la otra opción y escribimos main. La siguiente opción luego de esa es para poder usar git en múltiples terminales y no solo en bash.
Windows maneja los saltos de línea de manera diferente a Linux y Mac, entonces hay que elegir una opción la cual soluciona esto porque sino, no se podrá trabajar en multiplataforma. Luego se da Next hasta que descargue.

### Configuraciones Básicas
Para usar git necesitamos modificar nuestro archivo config, necesitamos colocar un nombre y correo globales para que git sepa identificar quién realizó cambios y los commiteó. Esto se hace abriendo una terminal y escribiendo:
_git config --global user.name "nombre de la persona"_
_git config --global user.email "correo@gmail.com"_
Es importante que el correo sea el mismo con el cuál nos registremos en github para que no existan errores inesperados.

### Preguntas de Examen:
* Quién fue el creador de GIT?

## Clase 2 - States y Commits
Primero se realiza un git init para iniciar el monitoreo de git a la carpeta.
### States
Tenemos 3 estados de git que son:
* Modified: Has hecho alguna modificación que git notó ya sea que creaste un nuevo archivo o cambiaste algo de un archivo existente, en un git status te saldrá de color rojo los archivos que has modificado.
* Prepared: Hemos hecho un git add archivo, y añadimos este cambio al área de preparación, en esta área está todo lo que va a entrar al siguiente commit.
* Confirmado: Se hizo un git commit y se guardaron los cambios, en un git status no saldrá nada, si volvemos a cambiar o agregar algo se repite el ciclo volviendo a modified.

Git cataloga nuestros archivos como Modified si tiene una versión anterior de este archivo, o Untracked si no tiene una versión antigua del archivo, es decir un archivo recién creado.

### Comandos Comunes
* git status: nos muestra los states de todos los archivos del directorio
* git add archivo o git add .: Pasa los archivos de modified a state, y con un punto, añadimos todos los archivos al área de prepared.
* git restore --staged archivo: Quita el archivo del área staged o prepared, vuelve a modified.
* git restore archivo: Descarta y elimina físicamente el cambio que se hizo a un archivo.
* git log: Nos muestra el historial de los commits que hicimos y sus hashes.
* git reset: Hace que el HEAD retroceda un punto al anterior commit, todos los archivos vuelven a su estado anterior. Usar con precaución.
* git commit: Es el comando estrella y la razón de ser de git, este crea un commit, el cual es un punto de guardado, es como tomar una foto de todo tu código, así como una foto congela el tiempo en una imagen y puedes ver el pasado, el commit saca una foto de todo el código.

### Buenas Prácticas
* Commit Atómico: Hacer commits cada que hagamos algo pequeño que añada o altere algo. Y no cuando terminos una tarea grande y compleja. O luego de varios cambios.
* Buenos Nombres de commits: En inglés, verbos imperativos, y tienen que explicar claramente qué cambios o añadidos trajo el commit. Son muchas cosas para tomar en cuenta así que dejo el enlace de una página que me ayudó mucho por su simpleza  en explicar esto" https://midu.dev/buenas-practicas-escribir-commits-git/
* Si el commit incluye muchos cambios que no se pueden commitear por separado por x razón, se puede escribir un commit largo colocando un título general y abajo especificando los cambios, el ejemplo que el auxi dio en clases:
_feat: Add math operations_
_- Add sum fuction_
_- Add mult function_
Esto solo en casos excepcionales, es mala práctica hacer commits largos.

### Preguntas de Examen:
* Qué hace --staged?

### Git Ignore
Podemos crear un archivo llamado .gitignore, en el cual con nano podamos escribir adentro en cada línea, el nombre de algún archivo que querramos que git no tome en cuenta para hacer los commits. El .gitignore también se agrega a los commits.



## Clase 3
## Clase 4 

### Git CheckOut
Nos permite cambiar la ubicación de nuestro puntero HEAD a otro commit, es decir podemos volver a otros commits, a esos puntos de guardado.
Cuando nos encontramos en el último commit de una rama, es igual a decir que estamos apuntando a esa rama.
Cuando volvemos en el tiempo NO estamos apuntando a la rama, sino a un punto en el tiempo, eso significa Detached Head.

Si commiteamos estando en detached head se nos advertirá que ese commit quedará al aire ya que no puedes cambiar el pasado, no se puede cambiar un commit ya hecho, así que no es recomendado hacer esto. La solución es crear una rama y guardar ahí los cambios, ya que si quieres cambiar algo en el pasado, probablemente amerite crear una nueva rama. (No entrará en el examen tanto el checkout)
### Preguntas de Examen:
* Cuál es la diferencia en usar --Global y no usar?

## Clase 5

### Ramas
Las ramas branches, existen, para trabajar de mejor manera, en específico para no afectar código que sí funciona o código que no queremos tocar. Por dar un ejemplo, es similar a escribir apuntes a la quete en un cuaderno, y luego de apuntar todo, pasarlo a limpio a otro cuaderno, sería similar a tener 2 ramas, una con código listo para deployar, limpio, normalmente en la rama Main, y otra rama donde se va experimentando normalmente se llama Develop.

Las ramas más comunes en un proyecto son:

* main: Es la rama principal, es el cuaderno en limpio.
* develop: Es la rama de producción es nuestro cuaderno borrador para hacer todas las modificaciones que querramos ya que no afectará al código ya funcional en main.
* feature: Esta rama dura poco, se usa para desarrollar funciones o características en específico, nacen de develop y se fusionan a develop.
* hotfix: Esta rama igual dura poco, se usa para corregir bugs o errores menores que ya están en main, y que no pueden esperar a una próxima actualización, nacen del main y se fusionan en el main también.
* release: Esta rama se usa para preparar una nueva versión de código estable, es decir una nueva versión de main, nace en develop y se fusiona tanto en main como en develop de nuevo.