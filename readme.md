###Aprende Git

This mini readme has the basics of how to use git, upload to Github and how to use GithubPages.
Esta es una pequeña guía que te enseñará:

* Cómo instalar Git.
* Cómo usar Git.
* Buenas prácticas.
* Subir a Github.

Temas:

* Instalar Git
* Git en proyectos.
* Branching
* Usar una Branch de Dev
* Verificar y unir Branches
* Git Log
* Git Stash
* Git Pull
* Git Clone
* Unir tu repositorio con uno remoto.
* Subir a Github
* Subir a Github Pages

###Instalación
Si estás en una máquina con Windows, deberías entrar a: 

* [Git para Windows](https://git-scm.com/download/win)

Es preferible que descarguen GitBash (viene en la instalación) para que haya disposición de un emulador tipo *NIX y hacer todo más sencillo.

Si ya estás en una máquina *NIX, como un distro de LINUX U OS X, entonces no hay nada de qué preocuparse, Git ya viene con tu máquina.

En caso de que quieras actualizarlo, o suceda el raro caso de que no esté instalado, entonces corre en tu terminal:

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

###Empezando con Git

Bien, ya tienes tu máquina con git, lo primero que vamos a hacer es asegurarnos de que esté ahí:

```console
git --version
```
Excelente, este tutorial es pequeño, pero cubriremos al rededor de 90% de lo que hay que saber.

Primero, hagamos nuestra carpeta. Puede ser el lugar que desees de tu computadora, yo tengo una que se llama ```Playground``` donde hagos mis expermientos.

*No hay que temerle a la consola, sino la consola a nosotros* - Proverbio chino.

```console
$ cd Docmuents/Playground/Projects
```
Una vez dentro de donde quieras hacer tu proyecto, vamos a crear la carpeta donde meteremos todos nuestros archivos:

```console
$ mkdir git_tutorial && cd git_tutorial
```

Perfecto, ahora vamos a empezar a usar git:

```console
$ git init
```

Tu terminal debería regresarme un mensaje como este:

```console
Initialized empty Git repository in /Documents/Playground/Proyectos/git_tutorial/.git/
```

Y deberías ver algo así:

![Init](https://raw.githubusercontent.com/oelizondo/learn-git/master/git_init.png)

Excelente, ahora vamos a crear un archivo de texto sencillo con el clasiquísimo *Hello world*

```console
$ touch hello.txt && vi hello.txt
```

No te asustes por el útlimo commando, solo le dijimos a nuestra terminal que entrara al editor de texto *vim* para aregregar algo de texto. Si no te gusta Vim, siempre puedes usar el editor de texto que prefieras

Si sigues en Vim, presiona *i* para entrar en modo *insert* para escribir.

![Init](https://raw.githubusercontent.com/oelizondo/learn-git/master/hello_txt.png)

After that we can exit vi pressing *esc* and *:wq*, press enter and you should be back in your terminal.
We can check our text file typing:

Después de eso, podemos salir de Vim tecleando *esc* y *:wq*, presiona enter y deberías estar en tu terminal de nuevo. El commando *:wq* significa *write and quit*. Eso le dice a Vim que grabe lo que escribiste y se salga. Ahora, para checar que sí hicimos cambios:

```console
$ cat hello.txt
```

Ahora es hora de nuestro primer commit. Los commits son básicamente una foto de nuestro proyecto en un determinado tiempo. Tómalo como un *ctrl + save* en cualquier programa. Siempre puedes regresarte a un commit en específico, pero veremos eso después, primero, vamos a revisar el *status* del proyecto para ver cuáles archivos está trackeando Git.

```console
$ git status
```

Deberías ver:

![Init](https://raw.githubusercontent.com/oelizondo/learn-git/master/git_status.png)


Esto significa que *hello.txt* no ha sido agregado al proyecto en sí. Hagamos eso con un commando sencillo:

```console
$ git add -A
```
Después de eso, todos nusestros archivos se agregar al proyecto, hagamos el commit:

```console
$ git commit -m "Adds text file to project"
```
La bandera *-m* es para agregarle un mensaje a tu commit, es útil para saber qué paso en ese momento. Los mensajes en git son obligatorios, y no te dejará avanzar si no le agregas uno,

###Branching
Muy bien, tenemos nuestro proyecto, hicimos nuestro primer commit, y ahora es hora de ver una de las funciones más importantes de Git. Branching. Branching te permite tener differentes versiones de tu proyecto dentro del mismo proyecto bajo un nonmbre diferente a master. Esto nos permite trabajar en un lugar aislado de la aplicación y lejos de master, y así no contaminar la versión final del proyecto. 

Esto es útil para trabajar en equipo. Imáginate que cada miembro del equipo tiene su propia branch donde escribe su código y corre y sus pruebas, y hasta que esté completamente validada va a poder mezclarse con master.


####La rama Dev

Antes de hacer cualquier cosa, debemos crear la rama de Dev. Dev nos permite romper, refactorizar, agregar y borrar todo el código que necesitemos antes de mandarlo a producción. Después de que todo el código en Dev haya sido verificado, se puede mandar a master y posteriormente a producción


```console
$ git checkout -b dev
```

![Init](https://raw.githubusercontent.com/oelizondo/learn-git/master/git_checkout.png)

Ahora tenemos una copia de nuestro proyecto en una rama diferente, así no contaminamos la rama master. Es hora de modificarla, y para esto entraremos rápidamente en una buena práctica: tener una rama separada para cada cosa que hagamos. Por ejemplo

* Componentes 
* Pruebas
* Fixes
* Bugs
* Features 

Ahorita mismo  mismo estamos en Dev, así que crearemos una rama nueva para trabajar en un sitio de internet. La llamaramos ```feature/website``` y le pondremos un archivo de HTML.

```console
$ git checkout -b feature/website
```

Then we create our HTML file:

```console
$ touch index.html
```

The content is in this link:

* [Simple Website structure](https://gist.githubusercontent.com/oelizondo/d5b95e661878135feeb6/raw/dc2893cb0066dd3c8cf127bf5cbf10e6f8a1bbef/index.html)

Puedes crear el contenido con cualquier editor de texto.

###Verificando y mezclando ramas

Excelente, ahora es tiempo de hacer un commit nuevo:


```console
$ git add -A
$ git commit -m "Adds website to project"
```
Perfecto, y ahora debemos agregar nuestra rama con el archivo HTML al proyecto principal. Mezclar es exactamente eso, agarramos una rama y la mezclamos con otra. Se ve algo así:

```console
$ git checkout dev
```

If we do

```console
$ ls
```

Con ese commando podemos ver los archivos en el directorio, y nos damos cuenta de que *index.html* no está ahi. No te alarmes, esto es porque *index.html* está en una rama separada, y la vamos a traer para acá:

```console
$ git merge feature/website
```

![Init](https://raw.githubusercontent.com/oelizondo/learn-git/master/git_merge.png)

Ahora si volvemos a hacer *ls* podemos ver nuestro *index.hmtl*, bastante cool, ¿verdad?

**Buena Práctica**
Es bueno primero verificar que las ramas que vayamos a mezclar, en este caso *feature/website* funcione. Tal vez esto no es muy obvio ahorita, pero en una aplicación de Rails por ejemplo, tenemos que asegurarnos que todas las pruebas pasen antes de traerla a Dev, y más imporantemente, master.

###Git log

Parece que llevamos mucho, pero vamos a ver con detalle exactamente qué. ¿Cómo hacemos esto?
Git es bastante bueno que tiene un tracking de todo lo ue hacemos en el proyecto, como un diario de actividades, hagamos:
Seems like we did a lot, but let's go back to see what we actually did. Wait, how do we do that?

```console
$ git log
```

![Init](https://raw.githubusercontent.com/oelizondo/learn-git/master/git_log.png)


Podemos ver:

* El ID del commit.
* El autor del commit.
* Cuándo se hizo el commit.
* El mensaje justificándolo (Ya ves porqué son imporantes).

Esto es muy importante, porque así podemos saber *quién* hizo *qué*, *cuándo* y *por qué*. ¿Te acuerdas cuando dije que podías regresar a cualquier commit que quieras para checar algo, agregar, quitar o modificar código? Se hace así:

```console
git checkout <commit_id>
```
Esto nos va a regresar en el tiempo (la verdad no) a ese punto en específico en nuestro proyecto donde podemos modificar lo que neceistemos.

###Git stash

Esta es una función más específica de git, pero digamos que estás en la rama *feature/website* y un miembro del equipo de pide que hagas una modificación en Dev. Se vale, pero no haz acabado de trabajar en tu rama, y si intentas cambiarte a Dev vas a recibir un error diciendo que tienes que hacer un commit primero. Para eso funciona *git stash*. Esta función te deja *poner en pause* o *congelar* lo que estamos haciendo y cambiarnos a otras ramas. Se hace así:

```console
$ git add -A
$ git stash
$ git checout <otra_rama>
```
Esto manda todo a una lista donde se quedará esperando hasta que regresamos a la rama del cual la usamos. Como es una lista, lo natural sería hacer:

```console
$ git stash pop
```

Para regresar a trabajar.

###Github y Github Pages

Muy bien, probablemente te estés preguntando cómo puedes subir tu trabajo a github y tener miles de estrellitas. Okay, te diré el secreto. Si estás leyendo esto entonces ya estás en github, así que haz una cuenta si no tienes una y pícale al botón verde que dice *New Repository*, pónle un nombre, un descripción rápida ¡y Crear!

Alright, you're probably wondering by now how to upload your repository to Github and have many stars. Alright, I'll tell you, if you're reading this then you're already here in github, so go ahead and click the big green button that says **+ New repository**. Name it, add a description and click the create button.

The next screen is kinda scary, but no fear, we only need the middle option **…or push an existing repository from the command line**

Before we can push anything though, we need to merge with *master*, remember? Go ahead and commit everything you have in *dev*, and merge to *master* (No tutorial this time, your turn!).

Now we just copy pase:

```console
$ git remote add origin git@github.com:oelizondo/git_tutorial.git
$ git push -u origin master
```
If it's your first time using git, then you'll be prompted to add your email and username. This is fine, it's for git and github to know who you are, so go ahead and follow *those* instructions.

And there we go, you just published your first project on Github!

Great, now we want to publish our website. Wait, what!? But I have to pay for that! Don't worry, Github gives us free hosting of our websites. You can check the whole documentation here: [Github Pages](https://pages.github.com/). 

For now, let's go ahead and checkout a new branch called *gh-pages*

```console
$ git checkout -b gh-pages
```
Now we just push

```console
$ git push -u origin gh-pages
```

And we're done! Our website should be published in just a minute.

![Init](https://raw.githubusercontent.com/oelizondo/learn-git/master/hello_world.png)


###Good Practices and Naming Conventions

Some good practices:

* Always create a dev / mvp / staging branch from master so you can work without worries.
* Name your branches short and sweet, prefix them with the purpose of that branch *feauture/user_aunthentication*, *test/users_spec*.
* After making sure your branch is working, merge it to dev and then delete that branch. This avoids having unused left-over data.
* Remember to commit useful messages. Don't make a "lol" commit message. What if another developer has to join your team and must read through your code base?

Feel free to add any other good practices you feel necessary! How? like this:

###Contributing

1. Fork project!
2. Make changes!
3. Pull request!

###Todo
* Translate to Spanish.


###Author

####Oscar Elizondo
* http://twitter.com/oehinojosa
* http://github.com/oelizondo


###Where to now?

These are just the basics of git, I would recommend checking out [Gitflow](https://github.com/nvie/gitflow) to see where these conventions and practices come from. [TryGit](https://try.github.io/levels/1/challenges/1) is acclaimed by the community, why don't you give it a try?

If something is not clear enough here, feel free to send a message or create an issue.