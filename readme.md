###Aprende Git

Este archivo explica lo basico de como usar git, subir tus archivos a Github, y usar GithubPages.

Temas:

* Que es Git
* Instalando Git
* Inicializando Git en proyectos
* Cambiando a una rama Dev
* Derivacion desde Dev (branching)
* Verificando y uniendo ramas (merging)
* Git Log
* Git Stash
* Git Pull
* Git Clone
* Enlazando a un repositorio remoto
* Subiendo archivos a Github
* Subiendo archivos a GithubPages

### Que es Git

La gente describe a git como una maquina del tiempo, algunos lo llaman un milagro, pero la realidad es que git es un *administrador de versiones*. Esto significa que git nos permite tener registro de los cambios a nuestros proyectos.

### Glosario

* ```mkdir``` generar un nuevo directorio
* ```touch``` crear un nuevo archivo en blanco
* ```cat``` desplegar el contenido de un archivo
* ```cd``` cambiar de directorio 
* ```vi``` ingresar al editor de texto vi
* ```ls``` desplegar lista de contenidos

###Instalacion
Si estas en una maquina que corre Windows, dirigete a:

#### [Git para Windows](https://git-scm.com/download/win)

Yo recomiendo descargar GitBash (viene con la instalacion) para facilitar las cosas.

Si estas en una maquina que corre Unix, asi como Linux o OSX, no te debes de preocupar, pues git ya viene instalado en tu maquina.

Si quieres actualizarlo, o en el raro caso de que no tengas git, entonces corre lo siguiente en consola:

Linux
```console
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get install git
```
OSX
```console
$ brew install git
$ brew upgrade git
```

##### Una nota en el comando ```brew```:
Brew significa Homebrew, un muy buen administrador de paquetes, especificamente para OSX, este administrador te ayudara en el futuro para instalar cosas como bases de datos, como Postgres, lenguajes de programacion, como Ruby, y administradores de version, como RVM. 

Puedes descargarlo en el siguiente enlace: [HOMBREW](http://brew.sh/).

###Inicializando Git

Excelente, tienes git instalado en tu maquina, ahora hay que utilizarlo.

Este sera un mini-tutorial sobre como usar git, asi que haremos un repositorio (un espacio donde guardas y manejas tu trabajo).

Para empezar, hagamos una carpeta (Yo usare mi propia direccion personal, asi que ustedes deberan de usar la suya):

```console
$ cd Docmuents/Playground/Projects
```

Una vez que estes adentro del directorio donde haras tu trabajo, crearemos una carpeta para guardar el contenido de este tutorial.

```console
$ mkdir git_tutorial && cd git_tutorial
```

Excelente! Ahora vamos a inicializar git en nuestro espacio de trabajo, utilizando:

```console
$ git init
```
Deberias de ver un mensaje como este:

```console
Initialized empty Git repository in /Documents/Playground/Proyectos/git_tutorial/.git/
```

Deberias de ver algo como esto:

![Init](https://raw.githubusercontent.com/oelizondo/learn-git/master/git_init.png)

Perfecto, ahora hay que crear un simple archivo de texto con el clasico "Hello World"

```console
$ touch hello.txt && vi hello.txt
```

No temas al ultimo comando, solo le instruimos a nuestra terminal (tradicionalmente llamada "command line") que ingresara al editor *vi* para agregar algo de texto a nuestro nuevo archivo.
No olvides presionar *i* para entrar a modo de *insert* y comenzar a teclear, escribiendo en el archivo.

![Init](https://raw.githubusercontent.com/oelizondo/learn-git/master/hello_txt.png)

Despues de eso, podemos salir de vi presionando *esc* y *:wq* (wq significa *write* y *quit*, o escribir y salir), presiona *enter* y deberias de estar de regreso en la terminal.
Podemos revisar nuestro archivo de texto al teclear:

```console
$ cat hello.txt
```

```cat``` muestra los contenidos del archivo que indicaste.

Ahora es tiempo para nuestro primer *commit*. Un *commit* es basicamente una fotografia de tu proyecto, donde el estado del proyecto se guarda. Siempre puedes regresarte a un commit especifico, pero veremos eso luego. Primero, hay que revisar el estado de nuestro proyecto para ver que archivos faltan ser agregados.

```console
$ git status
```

Deberias de ver:

![Init](https://raw.githubusercontent.com/oelizondo/learn-git/master/git_status.png)


Esto significa que *hello.txt* no ha sido agregado al proyecto de git aun, asi que hagamos eso con un comando para agregar a todos los archivos en nuestro proyecto:

```console
$ git add -A
```

Puedes agregar archivos individuales tambien:

```console
$ git add hello.txt
```

Despues de eso, podemos avanzar. Hay que hacer un commit a nuestro archivo de texto:

```console
$ git commit -m "Adds text file to project"
```

El comando *-m* es para adjuntar un mensaje al commit, haciendo mas facil ver que paso en ese punto guardado.

###Produciendo ramas (branching)

Bien, tenemos nuestro proyecto en camino, y es hora de introducir el concepto de ramas, o *branches*. Las ramas te permiten generar un clon de tu proyecto bajo un nombre distinto al proyecto principal (un clon que no se llama *master*), y te permiten seguir trabajando con una version distinta del proyecto sin contaminar la rama *master*. Esto es util cuando trabajamos con mas gente. Imagina a un equipo de dos personas, cada quien generando ramas a partir del archivo *master* y trabajando ahi para evitar conflictos entre si.

####La rama dev

Antes de cualquier otra cosa, tenemos que crear una rama dev. La rama dev nos permite separarnos, editar, agregar, y borrar cuanto codigo necesitemos antes de enviarlo a produccion o como *producto final*, que casi siempre es *master*. Ya que todo el codigo ha sido revisado y verificado en la rama dev, podemos unirla con master y hacer un *push*, empujando la rama dev hacia master para aceptar el trabajo hecho en dev como parte del producto final.

```console
$ git checkout -b dev
```

![Init](https://raw.githubusercontent.com/oelizondo/learn-git/master/git_checkout.png)


Ahora tenemos una copia de nuestro proyecto en otra rama. Es hora de modificarla! Es buena practica tener una rama diferente para una funcion, componente, prueba o caracteristica. En este momento, estamos en la rama dev, asi que crearemos una rama nueva llamada *caracteristica/sitioweb*, y tendremos un simple archivo html ahi.

```console
$ git checkout -b feature/website
```

Luego creamos nuestro archivo html:

```console
$ touch index.html
```

El contenido del html viene en el siguiente enlace:

* [Estructura de Sitio Web Simple](https://gist.githubusercontent.com/oelizondo/d5b95e661878135feeb6/raw/dc2893cb0066dd3c8cf127bf5cbf10e6f8a1bbef/index.html)

Solo copia y pega el contenido a tu html con cualquier editor de texto.

###Verificando y uniendo ramas (merging)

Excelente! Ahora es hora de hacer nuestro nuevo commit. Al igual que antes:

```console
$ git add -A
$ git commit -m "Agrega el sitio web al proyecto"
```

Bien, ahora es tiempo de hacer *merge* (unir) a nuestras ramas. Esto solo quiere decir que agarraremos una reme y la combinaremos con otra rama. Vamos a unirla a dev ahora, asi es como se ve:

```console
$ git checkout dev
```

Si hacemos lo siguiente:

```console
$ ls
```

Veremos que el archivo *index.html* no esta ahi! No hay que preocuparnos, esto es porque nuestro *index.html* esta en otra rama, y la vamos a traer aqui.

```console
$ git merge feature/website
```

![Init](https://raw.githubusercontent.com/oelizondo/learn-git/master/git_merge.png)

Repitiendo el comando *ls* nos mostrara que nuestro *index.html* esta aqui, indicando que unimos las ramas exitosamente. Grandioso, no?

**Buena practica**

Es buena practica verificar que la rama externa (en este caso fue caracteristica/sitioweb) funciona correctamente. Quiza no es muy claro u obvio ahorita, pero en una aplicacion de Rails, por ejemplo, deberiamos de tener seguro que nuestras pruebas son exitosas antes de unir una funcion importante a la rama dev, y, mas importante, a master.

###Git log

Parece que hemos hecho mucho, pero hay que regresarnos a ver que hemos hecho en realidad. Pero espera, como hacemos eso?

Git es suficientemente maravilloso como para notar todo lo que hemos hecho, como un registro. Si tecleamos:

```console
$ git log
```

![Init](https://raw.githubusercontent.com/oelizondo/learn-git/master/git_log.png)


podemos ver:

* La identificacion del commit
* El autor del commit
* Cuando fue hecho el commit
* El mensaje que viene con el commit

Esto es muy util y podemos guardar registro de *quien* hace *que* y *cuando*. Recuerdas cuando mencione que podemos ver los diferentes commits en caso de que alguien subio codigo disfuncional? Claro que podemos:

```console
git checkout <commit_id>
```

Esto nos regresara en el tiempo a ese punto especifico en nuestro proyecto y nos dejara arreglar ese codigo malo que a nadie le gusta.

###Git stash

Esta es una funcion mas especifica de git, pero digamos que estas en *caracteristica/sitioweb* y un amigo te pide que hagas algo en la rama *dev*. Es valido, pero aun no has terminado de trabajar en tu rama *caracteristica/sitioweb*, y para cambiar a *dev* tendrias que hacer un commit con trabajo que no esta terminado. Aqui es donde *git stash* sirve. Git stash te permite poner tu codigo en un estado de pausa, y puedes moverte y trabajar sin afectar a los archivos que mantuviste en pausa. Para esto, hacemos:

```console
$ git stash
```

Esto hace pausa a tu rama, permitiendote cambiarte a dev y continuar trabajo ahi. Para volver a *caracteristica/sitioweb*, entonces haces lo siguiente:

```console
$ git stash pop
```

para continuar tu trabajo.

###Github y Github Pages

Bien, probablemente estas preguntandote sobre como le haras para subir tu repositorio a Github y ganar muchas estrellas. Te lo dire, si estas leyendo esto entonces ya estas aqui en github, asi que ve y presiona el gran boton verde en tu perfil que dice **+ New repository**. Dale un nombre (lo que tu quieras), agregale una descripcion, y presiona el boton para crearlo.

La siguiente pantalla da un poco de miedo, pero no lo tengas, solo necesitamos la opcion de en medio: **or push an existing repository from the command line**

Antes de que podamos hacerle push a lo que sea, tenemos que unirlo con *master*, recuerdas? Haz commit a todo lo que tengas en *dev*, y unelo a *master* (no hay tutorial aqui, es tu turno!).

Ahora damos en la consola (metiendo tus datos):

```console
$ git remote add github git@github.com:<tu_nombre_de_usuario>/<tu_repositorio>.git
$ git push -u github master
```



Si es tu primera vez usando git, te pediran tu cuenta de github (el correo con el que te inscribiste) y tu contraseña. Esto esta bien, es para que git y github sepa quien eres, asi que sigue esas instrucciones.

Y ahi lo tienes, acabas de publicar tu primer proyecto en Github!

Bien, ahora queremos publicar nuestro sitio. Espera, que!? Pero debo de pagar por eso! No te preocupes, Github nos proporciona ese servicio de forma gratuita. Puedes checar toda la documentacion aqui (ingles): [Github Pages](https://pages.github.com/). 

Por ahora, hagamos una nueva rama llamada *gh-pages*

```console
$ git checkout -b gh-pages
```
Ahora solo hacemos *push*

```console
$ git push -u github gh-pages
```

And we're done! Our website should be published in just a minute.
Y terminamos! Nuestro sitio deberia de estar publicado en un momento. Puedes buscarlo como: <nombre_de_usuario>.github.io/<nombre_de_repositorio>

![Init](https://raw.githubusercontent.com/oelizondo/learn-git/master/hello_world.png)

###Buenas Practicas y Estatutos Para Nombrar

Algunas buenas practicas:

* Siempre crea una rama dev / mvp / staging desde master para que puedas trabajar sin preocupaciones.
* Nombra a tus ramas de manera corta y astuta, dandoles prefijos que indiquen sus propositos.
* Despues de asegurar que tu rama es funcional, unela a dev y luego elimina esa rama. Esto evita tener codigo no utilizado y de sobra.
* Siempre recuerda poner mensajes utiles con tus commits. No hagas un mensaje de commit que diga "XD". Que si otro desarrollador tiene que unirse a tu equipo y debe de leer por tu codigo?

Sientete bienvenido a agregar cualquier buena practica que haga falta! Como? Asi:

###Contribuyendo

1. Clona el proyecto.
3. Crea una nueva rama para tus cambios.
4. Haz ```git push -u github <tu_rama>```
5. Crea un *pull request* hacia ```spanish```.


###Autor

####Oscar Elizondo
* http://twitter.com/oehinojosa
* http://github.com/oelizondo


###Y ahora?

Esto es solo lo basico de git. Yo recomendaria ver [Gitflow](https://github.com/nvie/gitflow) para ver de donde vienen estas practicas y convenciones. [TryGit](https://try.github.io/levels/1/challenges/1) es aclamado por la comunidad. Por que no le das un intento?


Si algo no es suficientemente claro, por favor deje un mensaje para poderlo corregir!
