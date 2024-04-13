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

## Ejercicio 2

Explicar **qué son** los xpaths y para qué se utilizan.

Dada la siguiente página web, **resolver** los apartados:
https://selectorshub.com/xpath-practice-page/

1. Dado el siguiente xpath:

   ```//div[@class = 'elementor-shortcode']//input[@type = 'checkbox']```

   Indicar:

   - El **significado** de los diferentes elementos que componen dicho xpath, e indicar de forma resumida **qué se espera** que devuelva.
   - Indicar en la página web indicada anteriormente **qué elementos devuelve** dicho xpath, y **mostrar de qué forma se ha averiguado** qué elementos son los que ha devuelto.


2. Dado el siguiente xpath para obtener los usernames de las personas de la tabla de usuarios:

    ```//table[@id='resultTable']/tbody/tr/td/a[@href]```

    Indicar qué **mala práctica** (o malas) se observa en este xpath y realizar **mejoras** para tratar de evitar dichas malas prácticas.


3. Indicar xpaths que seleccionen los elementos **User email**, **Password**, **Company** y **Mobile Number**.

4. Indicar los xpaths necesarios para realizar un **caso de prueba** que realice una **búsqueda** sobre el navegador “**Edge**” en la tabla “**System distribution details**” y que **compruebe** que los sistemas operativos son “**windows**” y “**mac**”. Indicar qué **posibles problemas** se han encontrado en la aplicación para intentar **asegurar** que las **comprobaciones** son **correctas**, si es que se ha encontrado alguno, e indicar **posibles soluciones**.

### Respuestas
1.
   - Se espera que se devuelva un input de type 'checkbox' que esté en cualquier nivel contenido dentro de un div con class 'elementor-shortcode'
   - En la web se devuelven los 10 checkbox dentro de System Distribution Details. Se ha averiguado haciendo uso del Inspector de elementos del navegador y, haciendo un CTRL+F, poniendo en el buscador el xpath indicado.
2.  
   - La primera mala práctica es estar haciendo uso de la ruta completa, además de no ser necesario ese href.
   - Se podría simplificar en este caso de la siguiente manera: ```//table[@id='resultTable']//td/a```. De esta manera solo devolvería los nombres. En el caso de que la web cambiara, habría que indicar también algún identificador propio de esos elementos. Por ejemplo haciendo uso del atributo ```rel="noopener"```. Ejemplo: ```//table[@id='resultTable']//td/a[@rel='noopener']```
3.  
   - Email: Al tratarse de un id dinámico se debe hacer uso de otros atributos, analizando el elemento se ha verificado que uno de los atributos identificativos y estáticos es el dataid. ```//input[@dataid="sh_email1"]```
   - Password: ``//input[@id="pass"]```
   - Company: Al tratarse de un elemento que se repite en 4 ocasiones, pero en 3 de ellas está en oculto, se ha realizado un xpath en el que el contenedor (div) contenga una class identificativa y además que el atributo "display" no sea "none". Acto seguido se ha buscado también que el input esté contenido y que además tenga el atributo "name" como "company". ```//div[contains(@class,"parent-inline-cont") and not(contains(@style, "display: none"))]//input[@name="company"]```
   - Mobile number: Igual que el anterior solo que hemos cambiado el name por "mobile number". ```//div[contains(@class,"parent-inline-cont") and not(contains(@style, "display: none"))]//input[@name="mobile number"]```



## Ejercicio 3

Imaginemos que el ejercicio 2 lo ha hecho otro compañero. Explicar cómo llevamos a cabo las siguientes acciones:
1. **Traer las ramas** que el resto de compañeros hayan subido al repositorio remoto (Ayuda: hay IDEs que lo hacen automáticamente, por lo que si queremos verlo de forma práctica, es mejor no abrir el IDE para que no se traiga las ramas automáticamente, y hacerlo directamente por consola).
2. **Listar** los últimos commits de la rama del ejercicio 2.
3. Traer un **commit específico** del ejercicio 2 a la **rama** del ejercicio 3

## Ejercicio 4

**Apartado 1**

Desarrolla un **script** llamado ```ejercicio4.sh``` que haga lo siguiente: El script debe admitir un **parámetro** donde poder indicar el nombre de nuestro grupo, de cara que al ejecutarlo, mostrará el **mensaje** “Hola, NOMBRE_GRUPO“, siendo NOMBRE_GRUPO el parámetro que se le pasa.
 
Una vez mostrado el mensaje de bienvenida, el script solicitará al usuario que indique si se **quiere descargar el repositorio** de nuestro grupo, obligando a que la respuesta sea ‘**y**’ (sí) o ‘**n**’ (no). En caso de recibir una **respuesta diferente**, el script solicitará una entrada correcta.

Después, el script solicitará un **nombre de rama**, y según la respuesta anterior hará una u otra cosa:

- Si el usuario indica (‘y’), el script **clonará** el repositorio y creará la rama con el nombre dado anteriormente. Se mostrará un mensaje por pantalla indicando que se han realizado dichas acciones.

- Si se indica (‘n’) se entiende que ya lo tienes descargado, así pues el script realizará un **cambio de ruta** de la ruta actual hacia la ruta del repositorio para hacer un checkout y pull de dicha rama. Si **no existe** la rama, el script la **creará**, indicando que se ha realizado esta acción.

El script debe ser **robusto** y manejar correctamente las entradas del usuario, garantizando una interacción clara y comprensible.

**Apartado 2**

Con la imagen **ubuntu:22.04** de docker, generar un contenedor y copiar dentro el **zip** entregado en el repositorio indicado en el ejercicio 1 y el **script** bash a generar, el cual debe realizar lo siguiente:

- Instalar la versión 18 de node.
- Descomprimir el proyecto incluido en el zip.
- Descargar el fichero .env de la url https://storage.googleapis.com/quiz-2024/Q2/.env.
- Mover dicho fichero .env a la carpeta env del proyecto.
- Sustituir la variable NOMBRE_GRUPO por el nombre del grupo del quiz al que pertenezcas.
- Ejecutar el proyecto.

Mostrar que el proyecto **se está ejecutando** dentro del contenedor, y que al **acceder** desde un navegador al puerto 8080 de dicho contenedor se muestra el mensaje “El GrupoX ha resuelto el ejercicio”. Entregar tanto el **script bash** como el **Dockerfile** (si se necesita).

## Ejercicio 5

En este último ejercicio vamos a **incluir** las respuestas a los ejercicios a la **rama main** mediante **Pull Requests**. Indicar **qué es** una Pull Request, cuál es su **utilidad**, y cuáles son las **acciones** para **mergear** el código en la rama principal y que nos aseguran que los **cambios** que estamos haciendo son **correctos** y no rompen el código ya existente.

Para las Pull Request que tenemos, vamos a hacer las siguientes acciones (aplicando siempre las buenas prácticas indicadas previamente):

1. Simular que hay algún **error**, por lo que se va a indicar el error que se debe corregir y rechazar la Pull Request. Posteriormente, realizar el **cambio solicitado**, **aprobarla** y **mergearla**.
2. Realizar el flujo necesario para **mergear** correctamente el **resto** de Pull Requests sin ninguna condición autoimpuesta adicional, es decir, realizar el flujo que se desee (aprobar directamente, indicar errores que haya, etc.).

## Documentación de utilidad

Esta documentación aportada no va a resolver, ni pretende, la completitud de los ejercicios propuestos, pero sí puede ser una buena base de partida desde la que empezar a tener información para conseguirlo.

### Xpath y buenas prácticas:

https://www.blog.datahut.co/post/xpath-for-web-scraping-step-by-step-tutorial

https://exadel.com/news/how-to-choose-selectors-for-automation-to-make-your-life-a-whole-lot-easier/

### Práctica de Xpath

https://topswagcode.com/xpath/

### Git

https://www.youtube.com/watch?v=VdGzPZ31ts8

### Bash

https://www.freecodecamp.org/espanol/news/la-guia-definitiva-de-linea-de-comandos-de-linux-tutorial-completo-de-bash/ 
