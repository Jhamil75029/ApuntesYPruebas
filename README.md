# Apuntes del Curso
## Clase 1 
## Clase 2
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