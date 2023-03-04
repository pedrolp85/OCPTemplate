# ex288_3

Tenemos las templates de php-mysql ephemeral en .json
la template usa un repo de php (este mismo repo, https://github.com/pedrolp85/ex288_3.git context_dir =quotes)
y un s2i 

La app de php se conecta a la base de datos mediante parametros de la template:
$link = mysqli_connect($_ENV["DATABASE_SERVICE_NAME"],$_ENV["DATABASE_USER"],$_ENV["DATABASE_PASSWORD"],$_ENV["DATABASE_NAME"]);

En index.php imprime por pantalla un saludo, usando la variable de entorno GREETING


oc new-app --template templating/php-mysql-ephemeral -p NAME=quotesapi -p APPLICATION_DOMAIN=quote-${RHT_OCP4_DEV_USER}.${RHT_OCP4_WILDCARD_DOMAIN} -p SOURCE_REPOSITORY_URL=https://github.com/pedrolp85/ex288_3 -p CONTEXT_DIR=quotes -p DATABASE_SERVICE_NAME=quotesdb -p DATABASE_USER=user1 -p DATABASE_PASSWORD=mypa55 --name quotes


Modificar y crear la plantilla y desplegar la aplicacion de forma que: 

- La plantilla existe en el projecto <templating> y con el nombre ex288-php-mysql
- Todos los objetos creados por la plantilla se pueden borrar con el comando oc delete all -l template=php-mysql
- Usa versiones disponibles de php y mysql
- La template tiene un custom parameter GREETING
     - Si no le paso greeting al oc new-app, toma el valor por defecto "Engineers"
     - Si se lo paso lo usa para el saludo

- el siguiente comando falla: oc new-app ex288-php-mysql -> el paremetro APPLICATION_DOMAIN debe ser obligatorio
- el siguiente comando tiene exito: oc new-app --template templating/php-mysql-ephemeral -p NAME=quotesapi -p APPLICATION_DOMAIN=quote-${RHT_OCP4_DEV_USER}.${RHT_OCP4_WILDCARD_DOMAIN} -p DATABASE_SERVICE_NAME=quotesdb -p DATABASE_USER=user1 -p DATABASE_PASSWORD=mypa55 --name quotes y saca por pantalla el saludo por defecto "engineers"

- El siguiente comando es correcto y el saludo por pantalla es para los programadores: oc new-app --template templating/php-mysql-ephemeral -p NAME=quotesapi -p APPLICATION_DOMAIN=quote-${RHT_OCP4_DEV_USER}.${RHT_OCP4_WILDCARD_DOMAIN} -p DATABASE_SERVICE_NAME=quotesdb -p DATABASE_USER=user1 -p DATABASE_PASSWORD=mypa55 -p GREETING=developers --name quotes

Nota: tener en cuenta que el git y el context dir NO se van a pasar explcitamente al pasar la plantilla
