# Quiz 2 - 2024 - XPath, Git y Bash

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

### Respuestas
Xpath es un lenguaje de rutas de XML. Sirve para poder realizar criterios de busqueda avanzada, siendo bastante rápida y eficaz. Se utilizan para poder seleccionar elementos dentro de un DOM y poder después interactuar con ellos mediante JS/Cypress/Selenium..., etc.
1.
   - Se espera que se devuelva un input de type 'checkbox' que esté en cualquier nivel contenido dentro de un div con class 'elementor-shortcode'
   - En la web se devuelven los 10 checkbox dentro de System Distribution Details. Se ha averiguado haciendo uso del Inspector de elementos del navegador y, haciendo un CTRL+F, poniendo en el buscador el xpath indicado.
2.
   - La primera mala práctica es estar haciendo uso de la ruta completa, además de no ser necesario ese href.
   - Se podría simplificar en este caso de la siguiente manera: ```//table[@id='resultTable']//td/a```. De esta manera solo devolvería los nombres. En el caso de que la web cambiara, habría que indicar también algún identificador propio de esos elementos. Por ejemplo haciendo uso del atributo ```rel="noopener"```. Ejemplo: ```//table[@id='resultTable']//td/a[@rel='noopener']```
3.
   - **Email**: Al tratarse de un id dinámico se debe hacer uso de otros atributos, analizando el elemento se ha verificado que uno de los atributos identificativos y estáticos es el dataid. ```//input[@dataid="sh_email1"]```
   - **Password**: ``//input[@id="pass"]```
   - **Company**: Al tratarse de un elemento que se repite en 4 ocasiones, pero en 3 de ellas está en oculto, se ha realizado un xpath en el que el contenedor (div) contenga una class identificativa y además que el atributo "display" no sea "none". Acto seguido se ha buscado también que el input esté contenido y que además tenga el atributo "name" como "company". ```//div[contains(@class,"parent-inline-cont") and not(contains(@style, "display: none"))]//input[@name="company"]```
   - **Mobile number**: Igual que el anterior solo que hemos cambiado el name por "mobile number". ```//div[contains(@class,"parent-inline-cont") and not(contains(@style, "display: none"))]//input[@name="mobile number"]```
4.
   - Seleccionar el input: ```//*[@id="tablepress-1_filter"]/label[text()='Search:']/input```. Se ha añadido el texto del label porque no hay ningún otro identificador y para evitar que si la web añade más inputs esto falle.
   - Si el siguiente xpath devuelve algun matcheo, significa que se está incumpliendo con la condición de que la columna 2 sea windows o mac y la columna 3 sea Edge. ```//tr[not(td[@class='column-2' and text()='windows' or text()='mac']) and td[@class='column-3' and text()='Edge']]```
   - Posibles problemas que se han detectado: La tabla tiene paginado en el que solo se pueden visualizar 10 elementos por defecto. Para ello se debería utilizar un Cypress o Selenium que pueda hacer la paginación.

**Haciendo cambios para que se puedan ver desde el cherry-pick en el ejercicio3**

## Ejercicio 3

Imaginemos que el ejercicio 2 lo ha hecho otro compañero. Explicar cómo llevamos a cabo las siguientes acciones:
1. **Traer las ramas** que el resto de compañeros hayan subido al repositorio remoto (Ayuda: hay IDEs que lo hacen automáticamente, por lo que si queremos verlo de forma práctica, es mejor no abrir el IDE para que no se traiga las ramas automáticamente, y hacerlo directamente por consola).
2. **Listar** los últimos commits de la rama del ejercicio 2.
3. Traer un **commit específico** del ejercicio 2 a la **rama** del ejercicio 3

1. git fetch y luego git pull origin Ejercicio2
2. git log Ejercicio2
3. git cherry-pick [commit@Ejercicio2]
