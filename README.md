# ex288_3

Tenemos las templates de php-mysql ephemeral en .json y .yaml
la template usa un repo de php (este mismo repo, context_dir =quotes)
y un s2i

La app de php se conecta a la base de datos mediante parametros de la template:
$link = mysqli_connect($_ENV["DATABASE_SERVICE_NAME"],$_ENV["DATABASE_USER"],$_ENV["DATABASE_PASSWORD"],$_ENV["DATABASE_NAME"]);

oc new-app --template ${RHT_OCP4_DEV_USER}-common/php-mysql-ephemeral \
-p NAME=quotesapi \
-p APPLICATION_DOMAIN=quote-${RHT_OCP4_DEV_USER}.${RHT_OCP4_WILDCARD_DOMAIN} \
-p SOURCE_REPOSITORY_URL=https://github.com/${RHT_OCP4_GITHUB_USER}/DO288-apps \
-p CONTEXT_DIR=quotes \
-p DATABASE_SERVICE_NAME=quotesdb \
-p DATABASE_USER=user1 \
-p DATABASE_PASSWORD=mypa55 \
--name quotes


Modificar la plantilla y desplegar la aplicacion de forma que 
