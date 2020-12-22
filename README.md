# Caralibro

![Portada](assets/portada.jpg)

## Antes de empezar: algunos consejos

El enunciado tiene **mucha** información, van a necesitar leerlo varias veces. La sugerencia es que lo lean entero una vez (para tener una idea general) y luego vuelvan a consultarlo las veces que hagan falta.

Concentrensé en los requerimientos y, excepto que se traben mucho, respeten el orden sugerido. No es necesario que hagan TDD, pero sí sería interesante que vayan creando las distintas clases y métodos a medida que resuelven cada requerimiento y no antes. 

En otras palabras: trabajen completando cada requerimiento antes de pasar al siguiente, con los tests que aseguran que funciona incluidos. Si al avanzar en los requerimientos les parece necesario refactorizar, adelante, van a tener los tests que garantizan que no rompieron nada. :smirk: 

## Descripción del dominio

Un grupo de inversores, que no quiere dar la cara, nos contrató para llevar a cabo una red social. Caralibro permite a los usuarios publicar diferentes tipos de contenidos, los cuales incluyen texto, fotos y videos. 

Por cuestiones de almacenamiento en los servidores, nos interesará saber cuánto espacio ocupa cada publicación, en Bytes:

* Las **fotos** tienen un alto y ancho dado en pixels; el espacio que ocupan se calcula como `alto * ancho * factor de compresión`. El factor de compresión actual para las fotos es de 0.7, pero debe poder modificarse (para todas las fotos a la vez). Como de esta cuenta muy probablemente resulte un número con coma, vamos a redondear para arriba en todos los casos (ejemplo: `99.85` se volvería `100`, y lo mismo para `99.12`).
* Las publicaciones de **texto** son mucho más fáciles de calcular, ya que el espacio que ocupan es igual a la cantidad de caracteres que tienen.
* Los **videos** tienen un tamaño que depende de la calidad con la cual el usuario elija publicarlo. Para la calidad SD, el tamaño es igual a la duración del video en segundos. Para los videos HD 720p el tamaño es igual al triple de la duración en segundos del video y para los videos de HD 1080p el tamaño es el doble de los HD 720p. Debe poder modificarse la calidad sin tener que volver a hacer la publicación.

Los usuarios que pueden ver una publicación pueden indicar que esa publicación les gusta, aumentando el número de _me gustas_ de la misma. A nuestra aplicación le importa tanto la cantidad de _me gustas_ que recibió una publicación, como saber quiénes le dieron _me gusta_. No es posible que una misma persona le de _me gusta_ más de una vez.

Nuestros usuarios tienen **amigos**, pero no quieren compartir todas sus publicaciones con todos ellos. Por ejemplo, hay fotos y videos que no quieren que sus familias vean, por alguna extraña razón. Para satisfacer esa necesidad, cada publicación tiene asignado un permiso, que puede ser:

* **público**: cualquier usuario puede ver la publicación,
* **sólo amigos**: sólo los amigos pueden verla,
* **privado con lista de permitidos**: el usuario configura una lista que vale para esa publicación, y solo los usuarios que pertenezcan a esa lista pueden verla,
* **público con lista de excluidos**: similar al anterior, pero en este caso todos pueden ver la publicación excepto quienes están en la lista.

Cada publicación tiene uno de estos permisos asociados, que debe poder modificarse en cualquier momento. Sea cual sea la configuración, un usuario siempre puede ver sus propias publicaciones.

## Requerimientos

Se pide implementar la solución a este problema en Kotlin, junto con los tests que prueben cada uno de los requerimientos.

1. Saber cuánto espacio ocupa el total de las publicaciones de un usuario.
2. Poder darle _me gusta_ a una publicación, y conocer cuántas veces fue votada de esta forma.
3. Saber si un usuario es más amistoso que otro: esto ocurre cuando el primero tiene más amigos.
4. Saber si un usuario puede ver una cierta publicacion.
5. Determinar los mejores amigos de un usuario: el conjunto de sus amigos que pueden ver todas sus publicaciones.
6. Saber cual es el amigo más popular que tiene un usuario. Es decir, el amigo que tiene mas _me gusta_ entre todas sus publicaciones.
7. Saber si un usuario stalkea a otro. Lo cual ocurre si el stalker le dio _me gusta_ a más del 90% de sus publicaciones.

## Créditos

Enunciado original creado por Carlos Lombardi y Leonardo Gassman para UNQ. Transformado a Markdown, reformateado, reorganizado el texto y agregados nuevos requerimientos por Federico Aloi para UNaHur.

[![CC BY-SA 4.0][cc-by-sa-image]][cc-by-sa]

Esta obra está bajo una [Licencia Creative Commons Atribución-CompartirIgual 4.0 Internacional][cc-by-sa].

[cc-by-sa]: https://creativecommons.org/licenses/by-sa/4.0/deed.es
[cc-by-sa-image]: https://licensebuttons.net/l/by-sa/4.0/88x31.png
