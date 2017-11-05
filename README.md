## Configuracion Base de datos en Heroku



1. Cree (si no la tiene aún) una cuenta en el proveedor PAAS Heroku ([www.heroku.com](www.heroku.com)).
2. Acceda a su cuenta en Heroku y cree una nueva aplicación:

	![](img/HerokuCreateApp.png)
	![](img/HerokuCreateApp2.png)
	![](img/HerokuCreateApp3.png)

3. Después de crear su cuenta en Heroku y la respectiva aplicación,Agregue un Add-ons,para esto dirijase a la pestaña "Resources" y en la parte inferior encontrara una pestaña de busqueda,escriba "Heroku Postgres"

	![](img/HerokuCreateApp4.png)
	
	Seleccione la opcion "Heroku Postgres" , a continuacion saldra un recuadro donde se elegira el plan a usar,por default esta seleccionado el plan gratuito:
	
	![](img/HerokuCreateApp5.png)

4. Una vez creada la base de datos saldra un mensaje de informacion diciendo que la base de datos fue agregada con exito a la aplicacion anteriormente creada.
	
	![](img/HerokuCreateApp6.png)

5. Seleccione la opción que muestra la base de datos anteriormente creada

	![](img/HerokuCreateApp6B.png) 

	Una vez cargada la base de datos,se mostrara la informacion basica de la base de datos

	![](img/HerokuCreateApp7.png)

	
	
6.	Revise la informacion de conexion de la base de datos anteriormente creada

	Vaya a la pestaña "Settings"
	
	![](img/HerokuCreateApp8.png)
	
	Luego presione el boton "View Credentials"
	
	![](img/HerokuCreateApp8B.png)

7.	Se encontrara la siguiente informacion:

	Host: Server donde esta alojada la base de datos
	DataBase: Nombre de la base de datos 
	User: Usuario que se usara para entrar en la base de datos
	Port: Puerto por default 
	Password: contraseña del usuario para entrar en la base de datos
	
	![](img/HerokuCreateApp9.png)


8.	Conectandose a la base de datos
	
	(1)Para conectarse a la base de datos es preferible utilizar un cliente,en este caso usaremos el cliente SQuirreL.
	(2)Dirijase a la pagina oficial de SQuirreL [http://www.squirrelsql.org/](http://www.squirrelsql.org/) y descargue el instalador
	
	![](img/SQuirreLinstaller1.png)
	![](img/SQuirreLinstaller2.png)
	
	(3)Una vez descargado el instalador dirijase a la ruta donde se encuentra el archivo y abra la consola y proceda a instalar el archivo con el siguiente comando:
	java -jar squirrel-sql-<version>-install.jar
	(4)En caso de que el instalador genere errores por que no tiene permisos de escritura en la ruta por default,seleccione otra tipo "Documentos"
	![](img/SQuirreLinstaller3.png)
	(5)Seleccione instalar todos los plugins
	![](img/SQuirreLinstaller4.png)
	(6)Seleccione crear un acceso directo a escritorio
	![](img/SQuirreLinstaller5.png)
	(7)Una vez instalado se procedera a descargar el ultimo plugin de Postgres,para esto dirijase al siguiente link y descargue la version acorde a su version de java.
	[https://jdbc.postgresql.org/download.html](https://jdbc.postgresql.org/download.html)
	(8)Una vez descargado el plugin copielo y peguelo en la carpeta "plugins"  donde se instalo SQuirreL
	![](img/SQuirreLinstaller6.png)
	(9)Proceda a ejecutar el programa y dirijase a la pestaña "Drivers" y localize el driver "Postgres"
	![](img/SQuirreLinstaller7.png)
	(10)Dele click derecho y luego seleccione la opcion de "modificar"
	![](img/SQuirreLinstaller8.png)
	(11)Se abrira un recuadro con la configuracion del plugin,deje la casilla Class Name como se observa en la siguiente imagen.
	![](img/SQuirreLinstaller9.png)
	(12)Ahora en la pestaña "Extra Class Path" agregue el plugin de Postgres anteriormente descargado y en la casilla Class Name dejela como muestra la imagen
	![](img/SQuirreLinstaller10.png)
	(13)Guarde la configuracion y podra observar que el driver Postgres ya sale con un "chulito" de color azul.
	(14)Ahora dirijase a la pestaña Alias y agrege uno nuevo y llene los campos acorde a lo siguiente:
	Name: Nombre de la conexion "puede ser cualquiera"
	Driver: Seleccione el driver a usar en este caso "PostgreSQL"
	URL: La URL de la base de datos, para esto usaremos los datos del paso 7:
		jdbc:postgresql://[Host del paso 7]:[Puerto del paso 7]/[Base de datos del paso 7]
		Su URL debe quedar como el siguiente ejemplo: 
		jdbc:postgresql://ec2-50-19-110-195.compute-1.amazonaws.com:5432/d6gl59md04gnl0
		Debido a que la version gratuita de heroku no tiene configurado las credenciales SSL,es necesario informarle al SQuirreL (si no hacemos esto generara error al intentar conectarnos),para esto agregamos la siguente informacion a la URL:
		?ssl=true&sslfactory=org.postgresql.ssl.NonValidatingFactory
		Por lo que la URL en definitiva quedaria de la siguiente manera:
		jdbc:postgresql://ec2-50-19-110-195.compute-1.amazonaws.com:5432/d6gl59md04gnl0?ssl=true&sslfactory=org.postgresql.ssl.NonValidatingFactory
	User: user del paso 7
	Password: contraseña del paso 7
	![](img/SQuirreLinstaller11.png)
	(15)Una vez configurado presione el boton "Test",si fue correcta la conexion proceda a darle "ok",si no revise los parametros nuevamente.
	![](img/SQuirreLinstaller12.png)
	(16)Parece arriba del alias anteriormente creado y dele doble click para conectarse a la base de datos.
	![](img/SQuirreLinstaller13.png)
	![](img/SQuirreLinstaller14.png)
