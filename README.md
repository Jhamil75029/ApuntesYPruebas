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

### Git Ignore
Podemos crear un archivo llamado .gitignore, en el cual con nano podamos escribir adentro en cada línea, el nombre de algún archivo que querramos que git no tome en cuenta para hacer los commits. El .gitignore también se agrega a los commits.

### Preguntas de Examen:
* Qué hace --staged?


## Clase 3 - GitHub
Github con la cuenta institucional da muchos beneficios, el gran pero, es que al final de la carrera es probable que nos la quiten, sin embargo parece existir formas de vincular y no perder nuestro progreso.

### GitHub
Es lo que nos permite trabajar en equipo, no es lo mismo que git, GitHub es una plataforma en línea para subir nuestros proyectos y colaborar con otros.
Nos podemos conectar con github mediante http, pero siempre nos pedirá contraseña y es molesto, así que es mejor por este aspecto conectarse por ssh a git, para eso hay que preparar nuestro ssh en nuestra compu.

### SSH
Si estamos en linux, desde la terminal, y si estamos en windows, abrimos git-bash que es una terminal en bash y ejecutamos lo siguiente:
_ssh keygen -t ed25519 -C "nuestrocorreo@email.com"_
Esto genera un key de ssh, nos va a indicar donde se guardó, así que vamos y revisamos con cat la llave pública que creo (el .pub), y copiamos.

Con esa llave nos dirigimos a github, a settings, a donde dice SSH y algo más, y presionamos el botón de Add New ssh key. Le damos un título significativo, pegamos ahí la key, y volvemos a la terminal para ver si todo está en orden con este comando:
_ssh -T git@github.com_
Nos debería un salir un mensaje saludandonos si todo fue exitoso.

Dato Curioso: Se puede crear más de una llave en ssh, pero no es recomendable en la misma compu.

### HTTPS
Si usamos esto para intentar hacer commits, nos va a pedir siempre nombre de usuario y contraseña, y aunque coloquemos nuestra contraseña bien no nos va a dejar.
Esto pasa porque desde 2021, GitHub ya no acepta contraseñas normales para la terminal. Deberemos usar un Personal Access Token (PAT) en lugar de nuestra contraseña.

### Conectando nuestro repo local a GitHub
Se hace con los siguientes comandos:
_git remote add origin git@github.com:User/Repo.git_
Con esto guardamos una dirección de repositorio, y se la asignamos a la palabra origin para hacerlo simple.

### Comandos de Hoy
* git clone git@github...(dirección del repo con ssh): Este comando se ejecuta en la carpeta en la que se quiere bajar todo el proyecto de github hacia tu máquina, lo clona.
* git commit --ammend -m "mensaje": Cambia el nombre del último commit por el mensaje que colocamos, también cambia su hash.

### Apuntes diversos:
* Para ver los beneficios hay que buscar GitHub Student Developer Pack, dan un dominio gratis.
* El tamaño máximo de un commit es 100 megas
* El repositorio en github tiene un límite de 10Gb más o menos
* Si creamos un repositorio con nuestro nombre de usuario podremos usarlo como README de nuestro perfil, y con esto podemos crear una pequeña presentación o portafolio. Hacer esto vale 5 puntos de nota. En inglés 6 puntos, y tenemos permitido "inflarlo". 10pts si nos contrata una empresa.

### Preguntas de Examen:
* Comando para generar la llave ssh: ssh keygen -t ed25519 -C "nuestrocorreo@email.com"


## Clase 4 SSH Múltiple y Git Checkout

### Git Remote
Es el comando que nos permite gestionar nuestras conexiones con repositorios remotos, dice de donde traer, y a donde mandar.
* git remote -v : Nos muestra las url exacta a las que apunta nuestro repositorio local.
* git remote add <apodo> "url" : Vincula nuestro repo local a uno en la nube.
* git remote set-url <apodo> "url" : Cambia la url donde apunta nuestro repo.

### Múltiples SSH
Si por alguna razón tenemos multicuentas tendremos que tomar en cuenta lo siguiente:
Cada "cuenta" debe tener llaves ssh diferentes, no podemos usar la misma llave ssh ya que tiende a errores, y tampoco es seguro así que:
#### 1. Generamos otra llave ssh
Ejecutamos:
_ssh keygen -t ed25519 -C "correosecundario@email.com" -f ~/.ssh/id-secundario_
El detalle es agregar la banderilla -f al final, ya que esta le dice donde crear y con qué nombre crear la llave, sino hacemos esto se sobreescribiría la llave que ya tenemos.
#### 2. Creamos un archivo config en la carpeta .ssh
Y por cada cuenta tenemos que colocar y cambiar este bloque de texto de configuraciones:
_Host github.com_
_HostName github.com_
_User git_
_IdentityFile ~/.ssh/id-secundario_
**Qué significan?**
* Host: Es el apodo o alias que le pones a la conexión. Es lo que escribes en la terminal después de git@.
    Dato extra: Podrías ponerle cualquier apodo. Si le pusieras Host mi-github, tendrías que clonar repositorios escribiendo git clone git@mi-github:usuario/repo.git. Dejarlo como github.com es lo más cómodo porque te permite usar los comandos de Git normales y copiar las URLs tal cual te las da la página. Para las conexiones SSH tanto en GitHub como en GitLab, el usuario siempre es literalmente la palabra git.
* HostName: Es la dirección real del servidor a donde nos conectamos. Aquí entra gitlab.com o github.com, o cualquier otra plataforma que usemos.
* User: Es el nombre de usuario del sistema remoto. Para GitHub, siempre, siempre es git. Para las conexiones SSH tanto en GitHub como en GitLab, el usuario siempre es literalmente la palabra git.
    Dato extra: No debes poner tu nombre de usuario de la plataforma (no pongas "juanperez", ni tu correo). La plataforma (GitHub/GitLab) sabrá quién eres tú basándose en la llave secreta que le vas a mostrar en el siguiente paso.
* IdentityFile: Es la ruta exacta hacia la "escalera" (la llave privada) que quieres usar para ese Host específico. Esta es la parte más importante. Le dice a tu computadora: "Cuando vayas a esta dirección, usa esta llave en específico para identificarte, y no ninguna de las otras que tengas guardadas". Es lo que evita que tu llave del trabajo se mezcle con tu llave personal.

**En resumen: ¿Qué pasa cuando haces git push o git pull?**
Cuando escribes un comando en tu terminal, SSH lee ese bloque de texto y hace lo siguiente automáticamente en milisegundos:

"Veo que quieres ir a github.com (Host). Perfecto, me dirigiré a la dirección de internet github.com (HostName). Tocaré la puerta diciendo que soy el usuario git (User) y cuando me pidan mi identificación, les mostraré la llave que está guardada en ~/.ssh/id_ed25519_github (IdentityFile)."

Un ejemplo más claro suponiendo que tenemos una cuenta para github y otra para gitlab:
#Cuenta de GitHub
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_github

#Cuenta de GitLab
Host gitlab.com
  HostName gitlab.com
  User git
  IdentityFile ~/.ssh/id_ed25519_gitlab

#### 3. Configurando SIN --Global
Al configurar git al inicio siempre se nos dice definir nuestro nombre y email con la flag --global, esto le dice a toda la computadora que cada que cree un repositorio de git, se use ese email y ese nombre. Sin embargo ya que estaremos usando dos o más cuentas, por repositorio debemos después de clonarlo o crearlo ejecutar los siguientes comandos para asignarle un nombre y email a cada repositorio individualmente, dependiendo de que cuenta o plataforma querramos usar.
##### Para GitHub
git config user.name "Tu Nombre en GitHub"
git config user.email "tu_correo_github@email.com"
##### Para GitLab
git config user.name "Tu Nombre en GitLab"
git config user.email "tu_correo_gitlab@email.com"

Notemos que ninguno lleva flag --global. Estos se ejecutan luego de un git clone, o de un git init, para configurar el repositorio local. Git pone por encima estos al global, si es que existen, entonces no hay ningún problema en dejar el global como lo hayamos dejado.

Y claramente luego de crear la llave ssh, hay que conectarlo en la plataforma que toque conectarla.

#### Fuentes:
Como se puede apreciar me ayude de Gemini para complementar estos apuntes porque particularmente me será muy útil, el Los prompt fueron:
_Que se debe hacer para tener en mi git 2 o más cuentas? digamos que una es para subir cosas a github y otra es para gitlab_
Y luego:
_en el paso 4, explicame por fa que son cata una de esas líneas y que se pone y por que_

### Git CheckOut
Nos permite cambiar la ubicación de nuestro puntero HEAD a otro commit, es decir podemos volver a otros commits, a esos puntos de guardado.
Cuando nos encontramos en el último commit de una rama, es igual a decir que estamos apuntando a esa rama.
Cuando volvemos en el tiempo NO estamos apuntando a la rama, sino a un punto en el tiempo, eso significa Detached Head.

Si commiteamos estando en detached head se nos advertirá que ese commit quedará al aire ya que no puedes cambiar el pasado, no se puede cambiar un commit ya hecho, así que no es recomendado hacer esto. La solución es crear una rama y guardar ahí los cambios, ya que si quieres cambiar algo en el pasado, probablemente amerite crear una nueva rama. (No entrará en el examen tanto el checkout)

### Preguntas de Examen:
* Cuál es la diferencia en usar --Global y no usar?

## Clase 5 Ramas

### Ramas
Las ramas branches, existen, para trabajar de mejor manera, en específico para no afectar código que sí funciona o código que no queremos tocar. Por dar un ejemplo, es similar a escribir apuntes a la quete en un cuaderno, y luego de apuntar todo, pasarlo a limpio a otro cuaderno, sería similar a tener 2 ramas, una con código listo para deployar, limpio, normalmente en la rama Main, y otra rama donde se va experimentando normalmente se llama Develop.

Las ramas más comunes en un proyecto son:

* main: Es la rama principal, es el cuaderno en limpio.
* develop: Es la rama de producción es nuestro cuaderno borrador para hacer todas las modificaciones que querramos ya que no afectará al código ya funcional en main.
* feature: Esta rama dura poco, se usa para desarrollar funciones o características en específico, nacen de develop y se fusionan a develop.
* hotfix: Esta rama igual dura poco, se usa para corregir bugs o errores menores que ya están en main, y que no pueden esperar a una próxima actualización, nacen del main y se fusionan en el main también.
* release: Esta rama se usa para preparar una nueva versión de código estable, es decir una nueva versión de main, nace en develop y se fusiona tanto en main como en develop de nuevo.

## Clase 6 Flujo de Trabajo
Hoy vimos una práctica de como realizar Pull Request, como mandarlos y como aprobarlos. Estos evitan conflictos, ya que para estos se crean ramas para realizar cambios, sin afectar a la principal, luego de hacer todos los cambios se solicita que se apliquen y si los colaboradores aprueban estos cambios, se hace. 

Sino hacemos pull request, es decir sino creamos una rama para hacer los cambios, sino que subimos directo a la principal, tendremos que resolver conflictos.

El flujo para realizar un pull request es el siguiente:
#### 1. Actualizamos nuestro repo local
Nos dirigimos a la rama principal en la que querramos hacer cambios y traemos todo el estado actual del código para no generar conflictos, con:
_git checkout develop(rama a cambiar)_
_git pull origin (rama)_
#### 2. Creamos una nueva rama
En esta rama vivirán los cambios que hagamos al código, la hacemos con:
_git checkout -b(si la estamos creando) nombre-de-rama_
#### 3. Hacemos todos los cambios en la rama
#### 4. Preparamos los cambios
Como ya sabemos, git add ., y git commit, con un nombre significativo que represente los cambios que hicimos.
#### 5. Subimos la rama a github
Una vez commiteado, lo subimos al repo con:
_git push origin nombre-de-rama_
#### 6. Abrimos github y solicitamos pull request
Abrimos github, usualmente debería detectar que se acaba de crear una nueva rama y que agrega algunas cosas a la rama principal, entonces deberíá salir automáticamente un botón verde que diga "Compare & Pull Request".
Sino aparece este botón nos dirigimos a la pestaña "Pull Request" y le damos al botón "New Pull Request", y seleccionamos nuestra rama, y la rama con la que la queremos comparar, que es la principal.
Escribimos un título y una pequeñá descripción para los cambios que hicimos, el problema que resolvimos y todos los datos relevantes de nuestros cambios.
Finalmente le damos al botón "Create Pull Request"
#### 7. Revisión y Merge
Una vez hecho esto los colaboradores verán la pull request y podrán ver las líneas que estás agregando y cambiando, y podrán aceptar la pull request, exigir que hagamos cambios antes de mergearlas, o abstenerse de votar a favor o en contra, dependiendo de las reglas que se coloque en el repositorio se podrá mergear si la mayoría vota que sí, como también solo se podrá mergear si todos votan que sí y demás configuraciones.

Una vez aprobado el pull request el owner del repo o nosotros, podremos hacerle merge a la rama principal.

### Comandos Usados:
* git fetch: Revisa si hay cambios en el repositorio al que estamos conectados.
* git pull: Trae (Si es que hay) todos los cambios hechos en el repositorio al que estamos conectados, es decir en el origin.

### Apuntes diversos:
* Para subir una carpeta vacía en un commit debemos crear en esa carpeta un archivo llamado ".gitkeep". 

### Para el Examen:
El Auxi recomienda estudiar las diapos y los comandos más usados.

## Clase 7 Final Commit 