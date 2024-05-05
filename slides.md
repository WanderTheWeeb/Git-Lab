---
theme: dracula
title: Git & GitHub Actios
info: |

class: text-center
highlighter: shiki
drawings:
  persist: false
transition: slide-left
mdc: true
---

# Git & GitHub Actions

Laboratorio de git

---

## Git - Configuración del entorno

 💡 Existen 3 archivos donde se puede guardar la configuración, Para ver la configuración completa se usa el comando `git config --list`
````md magic-move
```bash{hide|1-2|4-5|7-8|all}
# A nivel SO  Archivo /etc/gitconfig
git config --system

# A nivel de un usuario  ~/.config/git/config
git config --global

# A nivel de repositorio .git/config
git config --local
```
```bash
# A nivel de un usuario  ~/.config/git/config
git config --global
```

````

---

## Configuracion inicial de Git

Lo siguiente es la configuracion básica para usar git, tras realizar su instalación.

```bash{none|1-2|4-5|7-8|10-11|all}
# Agregamos nuestro nombre de usuario
git config --global [user.name] “<nombre>”

# Agregamos nuestro correo
git config --global [user.email] <correo electronico>

# En algunos casos la rama por defecto es la master
git config --global init.defaultBranch main

# Mantener las credenciales en cache
git config --global credential.helper cache
```

<v-click>  Con las protestas de BLM en 2020, se puso en discusión el lenguaje racial en tecnología. Términos como amo, esclavo, blanco o negro pueden resultar dañinos sin necesidad. Muchos decidieron renombrar la rama "maestra" de GitHub a "principal". Siguiendo esta tendencia, GitHub cambió el nombre por defecto de esta rama especial a main.</v-click>

---

## Branches

- Las ramas en Git son versiones paralelas de un repositorio que permiten trabajar en diferentes características o versiones de un proyecto de forma independiente.
  
- La rama principal de un repositorio se llama generalmente **`main`** o **`master`**, y representa la versión estable y lista para producción del proyecto.

- Las ramas secundarias se utilizan para desarrollar nuevas características, corregir errores o realizar experimentos sin afectar la rama principal.

---


```mermaid
---
title: Branch
---
gitGraph LR:
       commit id: "1"
       commit id: "2"
       branch nice_feature
       checkout nice_feature
       commit id: "3"
       checkout main
       commit id: "4"
       checkout nice_feature
       branch very_nice_feature
       checkout very_nice_feature
       commit id: "5"
       checkout main
       commit id: "6"
       checkout nice_feature
       commit id: "7"
       checkout main
       merge nice_feature id: "customID" tag: "customTag" type: REVERSE
       checkout very_nice_feature
       commit id: "8"
       checkout main
       commit id: "9"
       checkout nice_feature
       merge very_nice_feature
       checkout main
       merge nice_feature
```

---

*Comandos más usados:*

- `git branch`: Muestra una lista de todas las ramas en el repositorio y resalta la rama actual.
- `git branch <nombre>`: Crea una nueva rama con el nombre especificado.
- `git switch <nombre>`: Cambia a la rama especificada, actualizando el directorio de trabajo con los archivos de esa rama.
- `git checkout -b <nombre>`: Crea una nueva rama con el nombre especificado y cambia a ella en un solo paso.
- `git merge <rama>`: Fusiona la rama especificada en la rama actual, combinando los cambios de ambas ramas.
- `git rebase <rama>`: Reorganiza la historia de los commits para que la rama actual se aplique sobre la rama especificada, creando una historia más lineal.
- `git push origin <rama>`: Envía los cambios de la rama local al repositorio remoto en la rama especificada.
- `git branch -d <nombre>`: Elimina la rama especificada.

---

# **Los Tres Estados de Git**


💡 Los archivos en Git pueden estar en tres estados: `confirmado`, `modificado` y `preparado`.


`Confirmado (Commited)` : significa que los datos están almacenados de manera segura en tu base de datos local. 

`Modificado (modified)`  : significa que has modificado el archivo pero todavía no lo has confirmado a tu base de datos. 

`Preparado (staged)`: significa que has marcado un archivo modificado en su versión actual para que vaya en tu próxima confirmación.

*Por lo tanto, un proyecto de Git tiene tres secciones: el directorio de Git, el directorio de trabajo y el área de preparación.*

---

1. Modificado es cuando has cambiado el archivo pero aún no lo has confirmado. 
    
    ```bash
    git init
    git clone
    ```
    
2. Preparado es cuando has marcado un archivo modificado para incluirlo en tu próxima confirmación. 
    
    ```bash
    git add
    ```
    
3. Confirmado es cuando los datos están seguros en tu base de datos local. 
    
    ```bash
    git commit
    ```
---
layout: cover
---
# Conceptos
## **Los conceptos básicos para trabajar  con git**
---

### Head

El concepto de `HEAD` es muy simple: se refiere al *commit* en el que está tu repositorio posicionado en cada momento. Por regla general `HEAD` suele coincidir con el último *`commit`* de la rama en la que estés, ya que habitualmente estás trabajando en lo último. Pero si te mueves hacia cualquier otro *`commit`* anterior entonces el `HEAD` estará más atrás.

### Main

Por regla general a *`main`* **se la considera la rama principal** y la raíz de la mayoría de las demás ramas. Lo más habitual es que en *`main`* se encuentre el "código definitivo", que luego va a producción, y es **la `rama` en la que se mezclan todas las demás tarde o temprano** para dar por finalizada una tarea e incorporarla al producto final

### Origin

**`origin`** es simplemente el nombre predeterminado que recibe el repositorio remoto principal contra el que trabajamos. Cuando clonamos un repositorio por primera vez desde **GitHub** o cualquier otro sistema remoto, el nombre que se le da a ese repositorio "maestro" es precisamente *`origin`*.

---

### Commit

Se define como un conjunto de cambios en los archivos que permite ver el historial. Cada `commit` tiene un identificador único generado con el algoritmo SHA.

### Tag

Un `tag` es una referencia a un punto específico del código, usado para volver a un punto anterior en el historial del repositorio. Si se elimina el commit o la rama principal, puede causar problemas. Se utilizan principalmente para el versionamiento.

```bash
git tag -a < nombre > -m “< descripción >”
git push --tags
```

### Ref

Nombre simbolico que apunta un `commit` especifiico, dentro una rama de un repositorio. Las referencias se encuentran el archivo `.git/refs`

### Refs

Directorio que hace referencia a todos los objetos del repositorio (Tags, branch…)

---

### Repositorio de git - Estructura

- *.git* : Corazón del sistema de control de versiones (Metadata: Historia, estiquetas, ramas, referencias , configuración global)
- *README* : Información del repositorio y su contenido, instrucciones básicas y ejemplos de uso, como contribuir al proyecto
- *LICENCE* : Establece los términos y condiciones bajo los cuales se puede usar, modificar y distribuir el software
- *.gitignore* : Todo lo que se desea excluir del control de versiones
- *.github* : Especifico para herramientas de github, como workflows
- *.docker* : Especifico para ficheros referentes a docker(Orquestaciones, ficheros de variables, repositorios de volumenes y aplicaciones)
- *src* : Código

---

### Estructura de un buen commit

El mensaje de un `commit` consiste en 3 diferentes partes separadas por una linea en blanco: el `titulo`, un `cuerpo` opcional y un `pie` opcional.

````md magic-move
```bash{none|1|3|5|all}
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```
```bash
Capitalized, short (50 chars or less) summary

More detailed explanatory text, if necessary.  Wrap it to about 72
characters or so.  In some contexts, the first line is treated as the
subject of an email and the rest of the text as the body.  The blank
line separating the summary from the body is critical (unless you omit
the body entirely); tools like rebase can get confused if you run the two together.

Write your commit message in the imperative: "Fix bug" and not "Fixed bug"
or "Fixes bug."  This convention matches up with commit messages generated
by commands like git merge and git revert.

Further paragraphs come after blank lines.

- Typically a hyphen or asterisk is used for the bullet, followed by a
  single space, with blank lines in between, but conventions vary here

If you use an issue tracker, add a reference(s) to them at the bottom,
like so:
```
````

> 💡 En caso de querer sobrescribir el commit utiliza el comando
`git commit -ammend -m <title> -m <description>`

---

### Recomendaciones para un buen commit

- Especifica el tipo de commit:
- Separa el título del cuerpo del mensaje con una línea en blanco.
- Tu mensaje de commit no debería contener ningún mensaje de espacios en blanco.
- Quita signos de puntuación innecesarios.
- No termines el título con un punto.
- Usa mayúsculas al inicio del título y por cada párrafo del cuerpo del mensaje.
- Usa el modo imperativo en el título.
- Usa el cuerpo del mensaje para explicar cuáles cambios has hecho y por qué los hiciste.
- No asumas que las personas que revisará el código entiende cuál era el problema original, asegúrate de agregar la información necesaria.
- No piense que tu código se explica solo.
- Sigue la convención del mensaje de commit definida por tu equipo.

---

### Tipos

- **feat**: Una nueva característica para el usuario.
- **fix**: Arregla un bug que afecta al usuario.
- **perf**: Cambios que mejoran el rendimiento del sitio.
- **build**: Cambios en el sistema de build, tareas de despliegue o instalación.
- **ci**: Cambios en la integración continua.
- **docs**: Cambios en la documentación.
- **refactor**: Refactorización del código como cambios de nombre de variables o funciones.
- **style**: Cambios de formato, tabulaciones, espacios o puntos y coma, etc; no afectan al usuario.
- **test**: Añade tests o refactoriza uno existente.
  



---

### Regresar a otro commit

```bash{none|1-2|4-5|all}
#Desplegamos el historial de la lista de commits
git log

#Buscamos el id del commit deseado
git checkout <id-del-commit>

#Para regresar al HEAD o commit anterior(original)
git switch -
```

---

### Revertir cambios

> Mi compañero de trabajo sugirió en nuestras guías que preferimos la bandera `--force-with-lease` sobre `--force` para el comando `git push`. Esta opción permite forzar el push sin el riesgo de sobrescribir inadvertidamente el trabajo de otra persona. Actualizará las referencias remotas solo si tiene el mismo valor que la rama de seguimiento remoto que tenemos localmente. En otras palabras, solo si nadie ha actualizado la rama en el servidor. Si hay nuevos commits remotos, `--force-with-lease` fallará con un mensaje de "información obsoleta", instándonos a buscar primero. - Un Dev en StackOvewFlow


#### Git Reset

`git reset HEAD` te permite volver a un commit anterior elimina cualquier otro commit en su camino de regreso. Imagina a alguien trapeando un piso. Si alguien quiere limpiar un pasillo, no solo limpian el final. Trapean todo el piso hasta el final del pasillo. Este tipo de deshacer un error asegura que limpies todo en el camino de regreso al commit al que quieres volver. Por otro lado, esta es una opción destructiva y no guarda ningún historial de lo que eliminaste.

#### Git Revert

`git revert` crea un nuevo commit que es el opuesto al commit al que estás regresando. En lugar de eliminar todo hasta ese commit, simplemente haces una copia de este y avanzas con ese commit. No se destruyen commits en el proceso. Imagina si quisieras regresar 30 commits atrás. Si usaste `git reset`, se eliminarían todos esos 29 commits. `git revert` te permite conservar todo ese historial y crea una forma segura de avanzar.

---

## Git Stash

El comando git stash almacena temporalmente (stash) los cambios que hayas efectuado en el código en el que estás trabajando para que puedas trabajar en otra cosa y, más tarde, regresar y volver a aplicar los cambios más tarde. Guardar los cambios en stashes resulta práctico si tienes que cambiar rápidamente de contexto y ponerte con otra cosa, pero estás en medio de un cambio en el código y no lo tienes todo listo para confirmar los cambios.

- `git stash` Crea un stash
- `git stash save <descripción>` Ayuda a dar contexto
- `git stash list` Muestra los stash
- `git stash apply` Aplica los cambios del stash
- `git stash pop` Aplica los cambios del stash en la rama actual y elimina el stash de la memoria temporal

---

# Uso de un Stash

```bash{1|2-4|6|all}
$ git stash list
stash@{0}: On main: add style to our site
stash@{1}: WIP on main: 5002d47 our new homepage
stash@{2}: WIP on main: 5002d47 our new homepage

$ git stash pop stash@{2}
```

---

### Flujo de trabajo recomendado

1. Clonar el repositorio
2. Crear rama local
3. Agregar los cambios
4. Integrar la rama de integración
5. Resolver conflictos si los hay
6. Hacer el push y el pull request

<br>

### Politicas recomendadas para activar en GitHub.

1. Cambiar la rama default por Develop
2. Crear reglas en el repositorio
    1. No permitir push directos a la rama develop
3. Definir una metodología con el equipo

---

### Versionamiento

| Característica    | SemVer                                                                                                | CalVer                                                                                        | shaVersion            |
|-------------------|-------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|-----------------------|
| Significado       | Versión basada en significado semántico. Mayor.Minor.Patch. Ej: 1.2.3                                | Versión basada en calendario. Año.Mes.Día. Ej: 2022.01.15                                    | Versión basada en el hash SHA-1 de la confirmación más reciente. |
| Cambios           | Mayor: Rompe compatibilidad hacia atrás. Minor: Agrega funcionalidad de manera retrocompatible. Patch: Corrige errores de manera retrocompatible. | Los cambios importantes suelen requerir cambios en la versión principal o en la secundaria. Las correcciones de errores y las mejoras menores pueden reflejarse en la versión de parche. | No tiene una estructura fija de versiones, ya que depende del hash SHA-1 de la confirmación más reciente. |
| Ejemplo           | 2.0.16                                                                                                | 2022.01.15                                                                                   | c2d69e2               |

---
layout: cover
---
# Metodologías con Git

---

# Git Flow

Algunos puntos clave que debes saber sobre Gitflow son los siguientes:

- Este flujo de trabajo es ideal para los flujos de trabajo de software basados en publicaciones.
- Gitflow ofrece un canal específico para las correcciones de producción.
<center>
<img src="https://wac-cdn.atlassian.com/dam/jcr:34c86360-8dea-4be4-92f7-6597d4d5bfae/02%20Feature%20branches.svg?cdnVersion=1605" alt="Git flow Diagram" width="600">
</center>

---

### El flujo general de Gitflow es el siguiente:

1. Se crea una rama `develop` a partir de `main`.

2. Se crea una rama `release` a partir de la rama `develop`.

3. Se crean ramas `feature` a partir de la rama `develop`.

4. Cuando se termina una rama `feature`, se fusiona en la rama `develop`.

5. Cuando la rama `release` está lista, se fusiona en las ramas `develop` y `main`.

6. Si se detecta un problema en `main`, se crea una rama `hotfix` a partir de `main`.

7. Una vez terminada la rama `hotfix`, esta se fusiona tanto en `develop` como en `main`.
---

# Trunk-Based

Rama Principal (Trunk): En `TBD`, todos los cambios se integran directamente en la rama principal (trunk). No se utilizan ramas de características (feature branches) de larga duración.
Integración Continua: Los equipos practican la integración continua, lo que significa que cada cambio se integra en la rama principal tan pronto como esté listo, lo que ayuda a detectar y corregir problemas de integración de manera rápida.


---

### Diagrama Trunk-Based 
1. **Rama Principal (Trunk):** En `TBD`, todos los cambios se integran directamente en la rama principal (trunk). No se utilizan ramas de características (feature branches) de larga duración.
2. **Integración Continua:** Los equipos practican la integración continua, lo que significa que cada cambio se integra en la rama principal tan pronto como esté listo, lo que ayuda a detectar y corregir problemas de integración de manera rápida.
<br>
<br>
<center>
<img src="https://file.notion.so/f/f/ec6edb8c-306e-4309-b6d8-6efb77ada7aa/89e9449a-d1e5-437f-9f04-af01c8d00163/Untitled.png?id=5b6b6669-66c5-4098-86e3-47fcf581029d&table=block&spaceId=ec6edb8c-306e-4309-b6d8-6efb77ada7aa&expirationTimestamp=1715040000000&signature=6gri53rbyhUEPpQDLYFMUx1B0Jt1qZjyc-oiw61dYq8&downloadName=Untitled.png" alt="Trunk-Based Diagram" width="60%"> 
</center>
---

### Git Flow vs Trunk-Based

| Aspecto | Gitflow | Trunk-Based Development |
| --- | --- | --- |
| Modelo de ramificación | Complejo, con varias ramas para características, desarrollo, lanzamiento y corrección de errores. | Simple, con una única rama principal (trunk). |
| Versiones estables | Se enfoca en tener una rama principal estable y ramas de lanzamiento para preparar versiones específicas. | Centrado en la entrega continua, integrando y desplegando cambios en la rama principal de forma regular y frecuente. |
| Desarrollo paralelo | Permite a varios desarrolladores trabajar en características independientes de forma simultánea, cada una en su propia rama de características. | Al centrarse en la rama principal, los desarrolladores trabajan en colaboración, integrando cambios directamente en la rama principal. |
---

### Git Flow vs Trunk-Based

| Aspecto | Gitflow | Trunk-Based Development |
| --- | --- | --- |
| Despliegues continuos | Menos orientado hacia despliegues continuos, ya que se enfoca en versiones estables y ramas de lanzamiento. | Orientado hacia despliegues continuos, integrando y desplegando cambios en la rama principal regularmente. |
| Complejidad | Mayor complejidad debido al modelo de ramificación y la gestión de múltiples tipos de ramas. | Menor complejidad debido al flujo de trabajo simple y la única rama principal. |
| Adecuado para | Proyectos que requieren un mayor control sobre las versiones y un desarrollo estructurado. | Proyectos donde la entrega continua y la simplicidad en el flujo de trabajo son prioritarios. |

---
layout: cover
---
# Practica 01
---

# Laboratorio de Git - Primera practica

Organiza equipos de 4 o 5 integrantes. Cada equipo deberá tener un líder designado para realizar la integración de los cambios.

Sigue estos pasos para configurar el entorno de trabajo:

1. EL lider del equipo hara un fork del repositorio principal en GitHub.
   
2. El lider configura dos remotos en su proyecto: uno para el repositorio principal y otro para el repositorio del equipo. 
    ```bash
    git remote add upstream https://github.com/WanderTheWeeb/Practica-01
    git remote add origin <url-del-repositorio-equipo>
    ```    
3. Cada integrante del equipo debe clonar el repositorio a su computadora local usando el siguiente comando: `git clone <url-repositorio-equipo>`

4. Crea una nueva rama para trabajar en tu tarea específica:
---
   
1. Realiza los cambios necesarios en los archivos de la página.
   
2. Una vez que hayas completado tus cambios, añade los archivos modificados al área de staging y haz un commit:
```bash
git add .
git commit -m "Mensaje descriptivo de los cambios realizados"
```

1. Sincroniza tu rama con el repositorio principal:
` git pull origin main `

1. Sube tus cambios a tu repositorio de equipo: `git push origin main`
2. Primero, asegúrate de estar en la rama principal: `git checkout main` o `git switch main`
3.   Luego, obtén los últimos cambios del repositorio principal: `git pull origin main `
4.    Finalmente, fusiona la rama del equipo con la rama principal y sube los cambios:
```bash
git merge origin/nombre-de-la-rama
git push upstream main
```
---
layout: two-cols
---

<template v-slot:default>

### Flujo de trabajo recomendado

1. Clonar el repositorio
2. Crear rama local
3. Agregar los cambios
4. Integrar la rama de integración
5. Resolver conflictos si los hay
6. Hacer el push y el pull request

<br>

### Politicas recomendadas para activar en GitHub.

1. Cambiar la rama default por Develop
2. Crear reglas en el repositorio
    1. No permitir push directos a la rama develop
3. Definir una metodología con el equipo

</template>
<template v-slot:right>
<br>
<br>
<br>
<br>
<img src="/public/Flujo.jpeg" width="600">

</template>
---

### Recomendaciones para un buen commit

- Especifica el tipo de commit:
- Separa el título del cuerpo del mensaje con una línea en blanco.
- Tu mensaje de commit no debería contener ningún mensaje de espacios en blanco.
- Quita signos de puntuación innecesarios.
- No termines el título con un punto.
- Usa mayúsculas al inicio del título y por cada párrafo del cuerpo del mensaje.
- Usa el modo imperativo en el título.
- Usa el cuerpo del mensaje para explicar cuáles cambios has hecho y por qué los hiciste.
- No asumas que las personas que revisará el código entiende cuál era el problema original, asegúrate de agregar la información necesaria.
- No piense que tu código se explica solo.
- Sigue la convención del mensaje de commit definida por tu equipo.

---

### Tipos

- **feat**: Una nueva característica para el usuario.
- **fix**: Arregla un bug que afecta al usuario.
- **perf**: Cambios que mejoran el rendimiento del sitio.
- **build**: Cambios en el sistema de build, tareas de despliegue o instalación.
- **ci**: Cambios en la integración continua.
- **docs**: Cambios en la documentación.
- **refactor**: Refactorización del código como cambios de nombre de variables o funciones.
- **style**: Cambios de formato, tabulaciones, espacios o puntos y coma, etc; no afectan al usuario.
- **test**: Añade tests o refactoriza uno existente.  
