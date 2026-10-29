# Guía de comandos de Git

Esta guía reúne los comandos de Git más utilizados, clasificados por categorías. Los bloques se pueden copiar y pegar directamente en la terminal.

> **Nota:** sustituye valores como `tu-nombre`, `archivo.txt`, `rama` o las URL por los datos de tu proyecto. Las salidas pueden variar según la versión de Git y el estado del repositorio.

## 1. Ayuda y versión

### Consultar la versión instalada

```bash
git --version
```

Salida de ejemplo:

```text
git version 2.43.0
```

### Abrir la ayuda de un comando

```bash
git help commit
```

También se puede consultar una ayuda breve:

```bash
git commit -h
```

## 2. Configuración inicial

### Configurar el nombre y el correo globales

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu-correo@ejemplo.com"
```

### Mostrar toda la configuración

```bash
git config --list
```

Salida de ejemplo:

```text
user.name=Tu Nombre
user.email=tu-correo@ejemplo.com
init.defaultbranch=main
```

### Consultar un valor concreto

```bash
git config user.name
```

Salida de ejemplo:

```text
Tu Nombre
```

## 3. Crear u obtener un repositorio

### Inicializar un repositorio en la carpeta actual

```bash
git init
```

Salida de ejemplo:

```text
Initialized empty Git repository in /ruta/proyecto/.git/
```

### Clonar un repositorio remoto

```bash
git clone https://github.com/usuario/proyecto.git
```

Salida de ejemplo:

```text
Cloning into 'proyecto'...
remote: Enumerating objects: 24, done.
Receiving objects: 100% (24/24), done.
```

## 4. Estado y seguimiento de archivos

### Ver el estado del repositorio

```bash
git status
```

Salida de ejemplo:

```text
On branch main
Changes not staged for commit:
  modified:   README.md

Untracked files:
  notas.txt
```

### Ver un estado resumido

```bash
git status --short
```

Salida de ejemplo:

```text
 M README.md
?? notas.txt
```

En esta salida, `M` significa modificado y `??` indica que Git todavía no sigue el archivo.

### Añadir un archivo al área de preparación

```bash
git add archivo.txt
```

### Añadir todos los cambios

```bash
git add .
```

### Dejar de seguir un archivo sin borrarlo del disco

```bash
git rm --cached archivo.txt
```

Salida de ejemplo:

```text
rm 'archivo.txt'
```

### Eliminar un archivo y preparar su eliminación

```bash
git rm archivo.txt
```

### Mover o renombrar un archivo

```bash
git mv nombre-anterior.txt nombre-nuevo.txt
```

## 5. Confirmar cambios (commits)

### Crear un commit

```bash
git commit -m "Añade la página de contacto"
```

Salida de ejemplo:

```text
[main a1b2c3d] Añade la página de contacto
 1 file changed, 18 insertions(+)
 create mode 100644 contacto.html
```

### Añadir y confirmar archivos ya seguidos

```bash
git commit -am "Corrige errores de estilo"
```

> `-a` no incluye archivos nuevos que Git todavía no esté siguiendo.

### Modificar el último commit

```bash
git commit --amend -m "Mensaje corregido"
```

> Este comando reemplaza el último commit. Evítalo si ya lo compartiste con otras personas, salvo que el equipo haya acordado reescribir el historial.

## 6. Consultar el historial

### Mostrar el historial completo

```bash
git log
```

Salida de ejemplo:

```text
commit a1b2c3d4e5f678901234567890abcdef12345678
Author: Tu Nombre <tu-correo@ejemplo.com>
Date:   Thu Oct 29 12:30:00 2026 +0000

    Añade la página de contacto
```

### Mostrar un historial compacto

```bash
git log --oneline
```

Salida de ejemplo:

```text
a1b2c3d Añade la página de contacto
7e8f9a0 Crea la estructura inicial
```

### Mostrar ramas y fusiones gráficamente

```bash
git log --oneline --graph --decorate --all
```

Salida de ejemplo:

```text
*   f7a8b9c (HEAD -> main) Merge branch 'contacto'
|\
| * c4d5e6f (contacto) Añade formulario
* | a1b2c3d Actualiza portada
|/
* 7e8f9a0 Commit inicial
```

### Ver quién modificó cada línea

```bash
git blame archivo.txt
```

## 7. Comparar cambios

### Ver cambios aún no preparados

```bash
git diff
```

Salida de ejemplo:

```diff
diff --git a/hola.txt b/hola.txt
index ce01362..94954ab 100644
--- a/hola.txt
+++ b/hola.txt
@@ -1 +1,2 @@
 hola
+bienvenido
```

### Ver cambios preparados para el próximo commit

```bash
git diff --staged
```

### Comparar dos ramas

```bash
git diff main..desarrollo
```

## 8. Ramas

### Listar las ramas locales

```bash
git branch
```

Salida de ejemplo:

```text
  desarrollo
* main
```

El asterisco identifica la rama actual.

### Crear una rama

```bash
git branch nueva-funcionalidad
```

### Cambiar de rama

```bash
git switch nueva-funcionalidad
```

Salida de ejemplo:

```text
Switched to branch 'nueva-funcionalidad'
```

### Crear una rama y cambiar a ella

```bash
git switch -c nueva-funcionalidad
```

### Renombrar la rama actual

```bash
git branch -m nuevo-nombre
```

### Eliminar una rama ya fusionada

```bash
git branch -d nueva-funcionalidad
```

Salida de ejemplo:

```text
Deleted branch nueva-funcionalidad (was a1b2c3d).
```

> `git branch -D rama` fuerza la eliminación aunque haya cambios sin fusionar y puede provocar pérdida de trabajo.

## 9. Fusionar ramas y resolver conflictos

### Fusionar otra rama en la rama actual

```bash
git merge nueva-funcionalidad
```

Salida de ejemplo sin conflictos:

```text
Updating a1b2c3d..c4d5e6f
Fast-forward
 contacto.txt | 5 +++++
 1 file changed, 5 insertions(+)
```

Salida de ejemplo con conflicto:

```text
Auto-merging contacto.txt
CONFLICT (content): Merge conflict in contacto.txt
Automatic merge failed; fix conflicts and then commit the result.
```

Después de editar el archivo y resolver las marcas de conflicto:

```bash
git add contacto.txt
git commit
```

### Cancelar una fusión con conflictos

```bash
git merge --abort
```

## 10. Repositorios remotos

### Listar los remotos

```bash
git remote -v
```

Salida de ejemplo:

```text
origin  https://github.com/usuario/proyecto.git (fetch)
origin  https://github.com/usuario/proyecto.git (push)
```

### Añadir un remoto

```bash
git remote add origin https://github.com/usuario/proyecto.git
```

### Descargar referencias sin integrar cambios

```bash
git fetch origin
```

Salida de ejemplo:

```text
From https://github.com/usuario/proyecto
 * [new branch]      desarrollo -> origin/desarrollo
```

### Descargar e integrar los cambios remotos

```bash
git pull origin main
```

### Publicar una rama por primera vez

```bash
git push -u origin main
```

Salida de ejemplo:

```text
Enumerating objects: 5, done.
Writing objects: 100% (3/3), done.
To https://github.com/usuario/proyecto.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```

### Publicar commits posteriores

```bash
git push
```

## 11. Guardar cambios temporalmente (stash)

### Guardar cambios sin crear un commit

```bash
git stash push -m "Trabajo en progreso"
```

Salida de ejemplo:

```text
Saved working directory and index state On main: Trabajo en progreso
```

### Listar cambios guardados

```bash
git stash list
```

Salida de ejemplo:

```text
stash@{0}: On main: Trabajo en progreso
```

### Recuperar el último stash y eliminarlo de la lista

```bash
git stash pop
```

### Aplicar un stash sin eliminarlo

```bash
git stash apply stash@{0}
```

## 12. Deshacer cambios

### Descartar cambios no preparados de un archivo

```bash
git restore archivo.txt
```

> Se perderán las modificaciones locales no guardadas de ese archivo.

### Sacar un archivo del área de preparación

```bash
git restore --staged archivo.txt
```

### Revertir un commit con un nuevo commit

```bash
git revert a1b2c3d
```

Salida de ejemplo:

```text
[main d4e5f6a] Revert "Añade la página de contacto"
 1 file changed, 18 deletions(-)
```

Esta opción es apropiada para commits que ya se han compartido, porque conserva el historial.

### Mover la rama al commit anterior conservando los cambios preparados

```bash
git reset --soft HEAD~1
```

### Mover la rama al commit anterior conservando los cambios sin preparar

```bash
git reset HEAD~1
```

> **Precaución:** `git reset --hard HEAD~1` también descarta los cambios de los archivos. Puede ocasionar pérdida de trabajo.

## 13. Etiquetas (tags)

### Listar etiquetas

```bash
git tag
```

### Crear una etiqueta anotada

```bash
git tag -a v1.0.0 -m "Versión 1.0.0"
```

### Mostrar una etiqueta

```bash
git show v1.0.0
```

### Publicar una etiqueta

```bash
git push origin v1.0.0
```

### Publicar todas las etiquetas

```bash
git push origin --tags
```

## 14. Buscar y recuperar información

### Buscar texto en los archivos controlados por Git

```bash
git grep "texto a buscar"
```

Salida de ejemplo:

```text
README.md:Este es el texto a buscar.
```

### Mostrar un commit concreto

```bash
git show a1b2c3d
```

### Ver los movimientos recientes de `HEAD`

```bash
git reflog
```

Salida de ejemplo:

```text
a1b2c3d HEAD@{0}: commit: Añade la página de contacto
7e8f9a0 HEAD@{1}: checkout: moving from desarrollo to main
```

`reflog` puede ayudar a localizar commits que ya no aparecen en el historial normal.

## 15. Flujo de trabajo básico

Un ciclo habitual de trabajo es:

```bash
git status
git switch -c mi-cambio
git add .
git commit -m "Describe el cambio"
git push -u origin mi-cambio
```

Para incorporar la rama después de revisarla:

```bash
git switch main
git pull
git merge mi-cambio
git push
```

## 16. Referencia rápida

| Objetivo | Comando |
|---|---|
| Ver el estado | `git status` |
| Añadir cambios | `git add .` |
| Crear un commit | `git commit -m "Mensaje"` |
| Ver el historial | `git log --oneline --graph --all` |
| Crear y abrir una rama | `git switch -c nombre-rama` |
| Fusionar una rama | `git merge nombre-rama` |
| Descargar cambios | `git pull` |
| Publicar cambios | `git push` |
| Guardar cambios temporalmente | `git stash` |
| Restaurar un archivo | `git restore archivo.txt` |

