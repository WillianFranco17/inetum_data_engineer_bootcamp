# Aprendizajes Git — Willian Franco

## ¿Qué es Git y para qué sirve?

Git es una herramienta que permite guardar, gestionar y controlar los cambios en el codigo o archivos de un proyecto.

## Comandos que aprendí

git init # Inicializa un repositorio
git add. # Agrega archivos
git clone <ruta del repositorio> # Clona un repositorio para subir cambios
git checkout -b <Nombre de la rama> # Crea una rama
git pull origin <Nombre de la rama> # Descarga y actualiza los cambios del repositorio remoto
git commit -m "<Comentario sobre el cambio>" # Guarda cambios
git branch <Nombre de la rama> # Crea una rama
git flow init # Inicializa GitFlow en el repositorio
git flow <rama> start <nombre> # Crea una rama con el respectivo el nombre, dependiendo de la rama que se crea sale desde main o develop, en el caso de ser feature y release sale desde la rama develop, para hotfix esta se genera desde la rama main
git flow <rama> finish <nombre o version> # Fusiona la rama creada con la rama de la cual fue creada eliminandola despues de dicha fusion, feature se fusiona con develop, release y hotfix se fusiona con la rama main y develop y crea un tag. 

## ¿Qué es una rama y por qué se usa?

Es una linea de trabajo independiente dentro de un mismo repositorio; se utiliza para no afectar el proyecto principal que ya esta funcionando, tambien sirve para poder trabajr de manera paralela al resto del equipo que esten realizando cambios al proyecto en curso, en el caso de usar gitflow permite organizar el trabajo dependiendo de la rama en la cual se este trabajando, facilita realizar pruebas con las cambios agregados antes de subirlos a la rama principal. 

## Dudas o dificultades

En principio es aprenderse de memoria los comandos y el saber en que momento usarlo, tambien identificar las ramas en la cual trabajar y mas cuando se hace uso de gitflow.

## Comandos que investigue

### 1. git stash

**¿Que hace?**
Guarda de forma temporal los cambios que todavia no se quieren confirmar con un 'commit'

**¿Cuando usarlo?**
Cuando se esta trabajando en una rama, pero necesito cambiarme de manera rapida a otra rama sin perder mis cambios.

**Ejemplo concreto**
git status
git stash
git status
git stash pop

**Que hice y que paso**
Modifique un archivo de prueba, luego ejecute git stash y Git guardo mis cambios temporalmente, al ejecutar git status el area de trabajo quedo limpia y luego use git stash pop y los cambios regresaron al archivo.

### 2. git diff

**¿Que hace?** 
Muestra las difrencias entre el estado actual de los archivos y la ultima version guardada.

**¿Cuando usarlo?**
Antes de hacer commit, para revisar exactamente que cambios realice.

**Ejemplo concreto**
git diff

**Que hice y que paso**
Modifique el archivo aprendizaje_Willian_Franco.md agregando esta seccion, luego ejecute git diff y Git me mostro las lineas nuevas agregadas y los cambios realizados antes de confirmarlos.

### 3. git log --oneline --graph

**¿Que hace?**
Muestra el historial de commits de forma resumida y visual usando una linea por commit y una grafica de ramas.

**¿Cuando usarlo?**
Cuando quiero revisar el historial del proyecto de manera clara y ver como se han unido las ramas.

**Ejemplo concreto**
git log --oneline --graph

**Que hice y que paso**
Ejecute el comando en mi rama y Git mostro una lista resumida de commits, cada uno aparecio con su identificacion corta y su mensaje.

### 4. git revert <commit>

**¿Que hace?**
Deshace los cambios de un commit creando un nuevo commit, sin borrar el historial anterior.

**¿Cuando usarlo?**
Cuando se hace un commit y quiero revertirlo de forma segura, especialmente si ese commit ya fue compartido con otras personas

**Ejemplo concreto**
git log --oneline
git revert 5339d8a

**Que hice y que paso**
Primero ejecute git log --oneline para identificar el commit que queria deshacer, luego ejecute git revert usando la identificacion del commit, Git creo un nuevo commit que revierte los cambios del commit seleccionado, manteniendo el historial del proyecto.

## Deshacer cambios de forma segura

### A. Descartar cambios que aun no estan en staging

**Comando**
git restore <nombre del arcibo>

**¿Que hace?**
Descarta los cambios locales de un archivo que todavia no ha sido agregado al staging con git add.

**¿Cuando usarlo?**
Cuando modifique un archico por error y quiero volverlo al ultimo estado confirmado en Git

**Que hice**
git status 
git diff
git restore aprendizaje_Willian_Franco.md
git status

**Que sucedio**
Primero modifique una linea del archivo, al ejecutar git status Git mostro el archivo como modificado, luego use git restore y los cambios se descartaron, despues git status mostro que el archivo ua no tenia cambios pendientes.

### B. Deshacer el ultimo commit pero conservar los cambios

**Comando**
git reset --soft HEAD~1

**¿Que hace?**
Deshace el ultimo commit, pero conserva los cambios en el area de staging.

**¿Cuando usarlo?**
Cuando hice un commit antes de tiempo o quiero rehacerlo con mas cambios.

**Que hice**
echo "Cambio temporal de prueba" >> aprendizaje_Willian_Franco.md
git add .
git commit -m "commit temporal"
git reset --soft HEAD~1
git status

**Que paso**
Git elimino el ultimo commit del historial, pero no borro los cambios, al ejecutar git status los cambios quedaron en staging, listos para hacer un nuevo commit

### C. Corregir el mensaje del ultimo commit antes de hacer push

**Comando**
git commit --amend -m "mensaje corregido"

**¿Que hace?**
Modifica el ultimo commit, en este caso cambia su mensaje.

**¿Cuando usarlo?**
Cuando se escribe mal el mensaje  del ultimo commit y todavia no lo he subido con git push.

**Que hice**
git add .
git commit -m "mensaje erroneo"
git commit --amend -m "docs: documentar estrategias para deshacer cambios"
git log --oneline

**Que paso**
Git reemplazo el ultimo commit por uno nuevo con el mensaje corregido, al revisar con git log --oneline, aparecio el nuevo mensaje corregido en el ultimo commit.