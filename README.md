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
   - **Email**: Al tratarse de un id dinámico se debe hacer uso de otros atributos, analizando el elemento se ha verificado que uno de los atributos identificativos y estáticos es el dataid. ```//input[@dataid="sh_email1"]```
   - **Password**: ``//input[@id="pass"]```
   - **Company**: Al tratarse de un elemento que se repite en 4 ocasiones, pero en 3 de ellas está en oculto, se ha realizado un xpath en el que el contenedor (div) contenga una class identificativa y además que el atributo "display" no sea "none". Acto seguido se ha buscado también que el input esté contenido y que además tenga el atributo "name" como "company". ```//div[contains(@class,"parent-inline-cont") and not(contains(@style, "display: none"))]//input[@name="company"]```
   - **Mobile number**: Igual que el anterior solo que hemos cambiado el name por "mobile number". ```//div[contains(@class,"parent-inline-cont") and not(contains(@style, "display: none"))]//input[@name="mobile number"]```
4.
   - Seleccionar el input: ```//*[@id="tablepress-1_filter"]/label[text()='Search:']/input```. Se ha añadido el texto del label porque no hay ningún otro identificador y para evitar que si la web añade más inputs esto falle.
   - Si el siguiente xpath devuelve algun matcheo, significa que se está incumpliendo con la condición de que la columna 2 sea windows o mac y la columna 3 sea Edge. ```//tr[not(td[@class='column-2' and text()='windows' or text()='mac']) and td[@class='column-3' and text()='Edge']]```
   - Posibles problemas que se han detectado: La tabla tiene paginado en el que solo se pueden visualizar 10 elementos por defecto. Para ello se debería utilizar un Cypress o Selenium que pueda hacer la paginación.
