# Git workflow

En este documento se expondrá una guía a la metodología y las herramientas que necesitará conocer si quieres aportar cualquier evolutivo del proyecto. Como a estas alturas no tenemos claro el cómo trabajar en el proyecto, esta guía nace de esta necesidad de exponer un flujo de trabajo (o alternativa de ella) para comenzar a trabajar.  

Sin intención de que sea estático, este flujo debería ser al menos una base para empezar a trabajar y para nada pretende ser definitivo. De hecho, que estas indicaciones cambien con el tiempo es una buena señal pues significará que el flujo se ira adecuando con las necesidades de los integrantes y del proyecto.

Al escribir esta guía también soy consciente de los integrantes del grupo con menos experiencia técnica e intentaré adaptar mi redacción y forma de explicar los conceptos lo más conciso, claro y sencillo posible para que la curva de aprendizaje sea lo menos inclinada posible y cualquiera pueda entender cómo trabajamos en el proyecto.

## Herramientas

Para comenzar, ¿qué herramientas necesitaremos para empezar a aportar en los evolutivos del proyecto?

- **Git**. Es el programa que se encarga del **control de versiones**. No solo nos permite realizar seguimiento de todos los cambios de forma cronológica sino que además será la herramienta que nos permitirá trabajar de forma deslocalizada. Será necesario descargarlo desde https://git-scm.com/. 

	> Por defecto, podemos interactuar con git a través de una consola de comandos (tranquilo, no lo tendrás que hacer gracias a GitHub Desktop) por lo que es un programa que se instalará en tu máquina pero no tendrá parte visual. En otras palabras, instalamos Git para que el ordenador "entienda" los comandos.
	>  Le podemos pedir, por ejemplo, que inicialice un proyecto con `git init` y automáticamente, nos preparará el proyecto para que sea compatible con git y empezará a hacer el seguimientos de cambios que hagamos.

- **GitHub**. Normalmente accederemos a esta herramienta a través del [cliente web](https://github.com/) en el navegador y tendremos que tener un usuario creado. GitHub es una plataforma web que nos permite **alojar** gratuitamente un proyecto que use git en sus servidores y ponerlo a disposición de los integrantes del grupo de forma privada. Se pueden crear equipos de trabajo y se pueden revisar y aceptar o rechazar los cambios de los demás componentes del grupo.

- **GitHub Desktop**. Sirve para operar con nuestro repositorio de forma visual. Nos simplifica la interacción con GitHub, podemos ejecutar comandos de git fácilmente (sin tener que usar la consola), podemos ver de un vistazo los cambios que hemos hecho, el historial de *commits* y más. Aunque este software no es estrictamente necesario, recomiendo su uso y la guía se basará en él para ilustrar y ejemplificar los casos de uso. Se descarga desde https://github.com/apps/desktop .

- **Git LFS**. Es una "extensión" de Git con funciones extras. En el punto que estamos del proyecto no es muy necesario pero sí es recomendable instalarla tal y como indica su página oficial: https://git-lfs.com/. Es necesario instalar Git antes de intalar Git LFS.

- ...y, obviamente, **Unreal Engine**.
## ¿Qué es git?

### Introducción a Git

Git es un software libre (que se traduce, entre nosotros, en que es gratis) que nos ayuda a trabajar en equipo y nos mantiene un historial cronológico pudiendo navegar entre todos los cambios que se han hecho en el proyecto.

Si configuramos un proyecto con un repositorio remoto (como es nuestro caso con GitHub), la estructura en la que trabaja Git tendrá una imagen parecida a esta. Las operaciones o comandos que podemos realizar con Git son representados por las flechas.

![[07bfe4077e4790f14f67829d47845b1e1dbddd68.png]] 

Como vemos en el diagrama, tenemos 3 instancias en nuestro ordenador principales:

- **Workspace**. Que representa los cambios que se han hecho localmente en el proyecto.
- A medida que vayamos trabajando, esos cambios deberemos ir añadiendolos al **index** según si queremos incluirlo o no en un commit. (Siempre me he imaginado index como una "bolsita" donde vamos quedandonos con los cambios que queramos del workspace para ir armando nuestro commit). 
- **Local Repository**. Con la operación de `git commit` confirmamos todo lo que había en el index y lo almacenamos en el repositorio local como un commit adicional.

Cuando trabajemos en el proyecto, estarmos trabajando en una copia local del proyecto de Git y no modificaremos el servidor. Si queremos subir nuestros cambios al servidor tendremos que ejecutar `git push`. Git guarda una copia del proyecto remoto que tendremos que ir actualizando para mantener nuestro proyecto al día con los desarrollos de nuestros compañeros (con `git fetch`). 
### Conceptos básicos

Para no perdernos con la terminología, cabe primero exponer algunos de los conceptos básicos de Git y qué representan:

- **Commit**. Un commit es un conjunto de cambios que hacemos en el proyecto. Los commits los armamos y confirmamos nosotros como desarrolladores según las modificaciones que hagamos sobre los ficheros originales (esto se entenderá mejor más adelante). Un commit también se puede entender como una "instantánea" del estado de los ficheros del proyecto.

	![[Pasted image 20240911190523.png]]
	Git montará entonces un historial (visualizado como un grafo en la imagen anterior) a medida que vayamos incrementando el número de *commits*. Todos los *commits* tienen un identificador (también llamado **hash**), un título, una descripción brindada por el desarrollador, una fecha y un autor. 

- **Rama**. Las ramas son bifurcaciones en el historial de *commits*. El uso que le daremos nosotros es de línea de trabajo individual. Así se ve un historial de *commits* con una rama divergente en el último *commit*:
	
	En nuestro proyecto en específico, existirá una rama que llamaremos `master` y será donde se reflejarán las versiones importantes del proyecto. Otra rama que tendrá de nombre `develop` donde tendremos el estado actual de desarrollo del proyecto (que debería tener un estado del proyecto estable y funcional). Y luego tendremos una rama por desarrollo o tarea. **Estas ramas serán individuales y personales y los cambios que hagamos en estas ramas no afectarán al estado de otras ramas**.

- **Stage** o index. Como se comenta en el apartado de *Introducción a Git*, podemos entenderlo como una "bolsita" donde iremos metiendo nuestros cambios para armar un commit.
### Comandos básicos

Es recomendable conocer qué hace cada operación de Git. En [esta página](https://confluence.atlassian.com/bitbucketserver/basic-git-commands-776639767.html) se encuentra una lista de comando esenciales de Git. Para acceder a la documentación oficial de Git se puede acceder a través de [este enlace](https://git-scm.com/docs).
## Convenciones

Es responsabilidad de todos y cada uno seguir las convenciones definidas en esta guía para mantener un nivel de legibilidad estándar y facilitar la navegación y colaboración.

*Propuesta, pendiente de revisión con el equipo:*
El idioma el cual definiremos los elementos del proyecto debe ser **inglés**, y debemos mantenerlo en todos los ámbitos para mantener una coherencia global. 

En el único caso que usaremos el español es para el título de los *commits* para que el historial de cambios sea lo más legible posible.

Al ser un elemento que usaremos para comunicarnos entre desarrolladores, los comentarios de código serán **preferiblemente en inglés pero también se permitirá el español**.

Todo lo demás (variables, nombre de funciones, archivos, macros...) deberán estar en inglés.
### Creación de ramas

Crearemos una rama por desarrollo o tarea y siempre deberemos crearla desde la rama **develop**. 

El nombre de la rama debe seguir la siguiente convención de nombre:

`id_description`

Donde `id` será el identificador de la tarea y `description` una pequeña descripción de la tarea preferiblemente de menos de 30 carácteres en minúsculas. Los espacios serán sustituidos por "-".

Por ejemplo, tengo asignada una tarea que consiste en implementar el boost en el personaje y la tarea tiene el identificador `24`. Para trabajar en esta tarea, tendría que crearme una rama desde develop con el siguiente nombre:

`24_boost-implementation`

Cuando nuestros cambios se hayan incluido en la rama origen (que suele ser develop), debemos borrar la rama de la tarea.

Normalmente querremos tener una tarea asignada para cada incremento del proyecto que hagamos para mantener el seguimiento de las cosas que vamos haciendo. Puede darse el caso en el que esto no sea así y en algún casos tengamos que añadir algún commit que no tenga tarea correspondiente en este caso la rama tendrá la siguiente nomenclatura:

`bugfix_description`: cuando en la rama pensamos corregir algún bug.
`config_description`: cuando en la rama se van a tratar ajustes de la configuración del proyecto.
`refactor-description`: cuando hagamos algún cambio para refactorizar el código.
`optim-description`: cuando realicemos alguna tarea de optimización que no tenga tarea asignada.
``
### Creación de commits

Cuando queramos crear un commit el título también debería seguir una comvención de nombres. Esto nos facilitará el encontrar una tarea entre el historial y poder volver a estados anteriores con facilidad. El título deberá seguir la siguiente convención:

`[id] This is a title example`

Donde `id` es el identificador de la tarea y `This is a title example` será el título de la tarea de forma más descriptiva posible.

Para el ejemplo que venimos viendo. Cuando haya acabado de realizar la tarea generaré un commit que tendrá el siguiente título:

`[24] Implementación del boost`

Si vemos oportuno crear varios commits para una tarea es posible **pero es recomendable mantener las tarea en el menor número posible de commits**. Normalmente que esto ocurra es señal de que podríamos haber divido la tarea en subtareas. Si esto ocurriese no debería existir 2 commits con el mismo título. Ejemplo de 2 commits para 1 tarea:

`[24] Implementación del boost: configuración`
`[24] Implementación del boost: código y ajuste`

También deberemos rellenar una pequeña descripción de los commits. En este apartado escribiremos una pequeña descripción de los cambios que hemos introducido siendo lo más descriptivo posible.

Ejemplo de un commit con título y descripción:

```
[24] Implementación del boost: código y ajuste

Se añade la lógica necesaria al jugador para que se pueda aplicar el boost. Se han realizado cambios en el movimiento del jugador para afinar la velocidad.
```

Para los cambios sin tarea modificamos el id por el tag correspondiente en minúsculas. Por ejemplo:

```
[refactor] Cambio de orden de funciones en el Tick

Se ha cambiado el orden de las operaciones en el tick para aumentar la legibilidad del blueprint.
```
### Nomenclatura de archivos y estructura de carpetas

Seguiremos la convención que nos da Unreal para ello:

https://dev.epicgames.com/documentation/en-us/unreal-engine/recommended-asset-naming-conventions-in-unreal-engine-projects?application_version=5.3
## Caso de uso

En este apartado mostraremos un flujo completo de cómo realizar un desarrollo en el proyecto. Realmente, podrías haberte saltado toda la chapa que he escrito hasta aquí, que con leer este apartado deberías ser capaz de utilizar las herramientas que utilizaremos (aunque no sabrías cómo funcionan algunas cosas). Al lío.
### Paso 1: Instalar las herramientas

### Paso 2: Clonar el proyecto

### Paso 3: Crear una rama

### Paso 4: Trabajar en el proyecto

### Paso 5: Hacer un commit

### Paso 6: Pull Request

### Paso 7: ¡Siguiente tarea!

### *Troubleshooting* o casos especiales

Este apartado ira creciendo a medida que surjan los problemas. La intención de este punto es que expongamos casos y otros compañeros puedan consultar la solución.
#### Conflictos
#### Locking de archivos con Git LFS