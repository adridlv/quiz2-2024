# Quiz 2 - 2024 - XPath, Git y Bash

## Ejercicio 1

Crear un repositorio **privado** en Github, con nombre "**Quiz-2024-GrupoX**" (siendo la X el nº del grupo), **dar acceso** a los **miembros** del equipo y a "**quimikuaxh**" (el usuario de jgavilan), establecer la **rama** main como la principal y subir a dicha rama el contenido de la rama “quiz2-2024" del repositorio https://github.com/Emergya/ed-qa. Tener en cuenta que para resolver **cada uno de los siguientes ejercicios** se deberá hacer en una **rama distinta**, y las **respuestas** se deben indicar en el **readme** del proyecto, junto con el enunciado.

Explicar **qué es** el fichero **gitignore**, y crear uno teniendo en cuenta que es un repositorio apto para almacenar código nodejs. Explicar qué se ha incluido en él y por qué.

### Respuesta:
Teniendo en cuenta que es un gitignore para un proyecto de node, se ha utilizado como base un gitignore de PS.
Se destacan los siguientes:
- node_modules: Por la instalación de las librerías de npm
- package-lock.json: Por la instalación de las librerías de npm
- dist: Por la transpilación de TS a JS
- env: Para no subir credenciales ni variables de entorno.
- .idea y .vscode: Para no subir configuración generada por los IDEs.
- .DS_store y Thumbs.db: Para no subir ficheros generados por Mac
- El resto de ficheros son, o bien propios de emergya, o bien se han incluido como buenas prácticas
