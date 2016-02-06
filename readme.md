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

Alright, we have our project rolling, it's time to introduce Branches. Branches allows you create a clone of your project under a different name that's not master, and let's you keep working with a different version of the project without contaminating the master branch. This is useful when we work with other people. Imagine a team of two persons, each branching out from master to his or her own branch and work from there to avoid conflicts with each other.

####The dev branch

Before anything else, we need to create a dev branch. the Dev branch allows us to break, refactor, add, delete as much code as we need before sending it to production. After all the code has been verified in Dev, we can merge it with master and push it.

```console
$ git checkout -b dev
```

![Init](https://raw.githubusercontent.com/oelizondo/learn-git/master/git_checkout.png)


Now we have a copy of our project in another branch. It's  time to modify it! It's good practice to have a separate branch for a feature, component, test or functionality. Right now we're in Dev, so we're going to create a new branch called *feature/website* and have a simple html file there.

```console
$ git checkout -b feature/website
```

Then we create our HTML file:

```console
$ touch index.html
```

The content is in this link:

* [Simple Website structure](https://gist.githubusercontent.com/oelizondo/d5b95e661878135feeb6/raw/dc2893cb0066dd3c8cf127bf5cbf10e6f8a1bbef/index.html)

Just copy and paste it with any text editor.

###Verifying and merging branches

Great! Now it's time to make our new commit. Same as before:

```console
$ git add -A
$ git commit -m "Adds website to project"
```

Awesome, now it's time to *merge* our branches. Merging just means we take one branch and combine it with another one. We're going to merge it into Dev right now, here's how it would look like:

```console
$ git checkout dev
```

If we do

```console
$ ls
```

We'll see that the *index.html* file is no there! Not to worry, this is because our *index.html* is in another branch, and we're going to bring it over here.

```console
$ git merge feature/website
```

![Init](https://raw.githubusercontent.com/oelizondo/learn-git/master/git_merge.png)


Now, repeating the *ls* command will show us our *index.html* file. Pretty cool, huh?

**Good practice**
It's good practice to first verify that the external branch (in this case feature/website) works correctly. Maybe right now it's not obvious, but in a Rails application for example, we should make sure all our tests are passing before merging an important feature into dev, and more importantly, master.

###Git log

Seems like we did a lot, but let's go back to see what we actually did. Wait, how do we do that?

Git is awesome enough that it keeps track of everything we do, kind of like a log (not a wooden one). If we type

```console
$ git log
```

![Init](https://raw.githubusercontent.com/oelizondo/learn-git/master/git_log.png)


we can see:

* The commit Id
* The author of the commit
* When was the commit made
* The message that comes with the commit

This is very useful and we can keep track of *who* does *what* and *when*. Remember when I told you we can hop to different commits in case somebody commited some buggy code? We totally can:

```console
git checkout <commit_id>
```

This will send us back in time to that specific point of our project and allow us to fix that buggy code nobody likes.

###Git stash

This is a more specific feature of git, but let's say you're in *feature/website* and some coworker asks you to do something in *dev*. That's fair, but you're not finished working in your branch, and to change back to *dev* you'd have to make a silly commit with work that's not done. This is where *git stash* comes in. Git stash let's you add your modified files but instead of commiting them we just

```console
$ git add -A
$ git stash
```

This sends everything into a queue list, and *pause* your branch, allowing you to switch over to dev and continue working. When coming back to *feature/website* then you should just

```console
$ git stash pop
```

To resume your work.

###Github and Github Pages

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