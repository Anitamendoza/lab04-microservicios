# lab04-microservicios
Microservicios
# Contenedores Microservicios
######  Paso 1: Crear la aplicación Express y ejecutarla en el puerto 5000
Asegúrate de haber creado la aplicación Express siguiendo los pasos mencionados anteriormente y que esté configurada para ejecutarse en el puerto 5000.

###### Paso 2: Crear un repositorio público en GitHub

Crea un repositorio público en GitHub. Asegúrate de que el repositorio sea público, ya que si es privado, podría haber problemas de acceso desde AWS.

###### Paso 3: Subir tu aplicación a tu repositorio

Sube tu proyecto Express a tu repositorio de GitHub utilizando los comandos de Git, como git clone, git status, git commit -m y git push.

###### Paso 4: Crear una instancia en AWS

- Inicia sesión en tu cuenta de AWS.

- Ve al panel de control de EC2.

- Haz clic en "Launch Instance" para crear una nueva instancia.

- Selecciona una imagen de Ubuntu (por ejemplo, "server-lab04") y sigue los pasos para configurar la instancia según tus necesidades. Asegúrate de configurar las reglas de seguridad para permitir el tráfico en el puerto 9000.

- Lanza la instancia y guarda la clave privada (.pem) que se te proporcionará, ya que la necesitarás para acceder a la instancia.

###### Paso 5: Acceder a la instancia y configurar Docker y Node 
- Conéctate a la instancia de AWS mediante SSH con tu clave privada en Git Bash:
`$ ssh -i tu-clave.pem ubuntu@tu-direccion-ip-de-aws `
- Instala docker y node 
- Verifica que Docker esté funcionando correctamente:- 
`$ docker --version`
`$ id -nG`
- Verifica que Node esté instalado:
`$ docker search node `

###### Paso 6: Crear un archivo Dockerfile
- En tu instancia de AWS con Ubuntu, crea una carpeta llamada "proyectos" y dentro de ella, crea una carpeta específica, por ejemplo, "lab04".
`$ mkdir proyectos`
`$ cd proyectos`
`$ mkdir lab04`
`$ cd lab04`
- Crea un archivo Dockerfile dentro de la carpeta "lab04" y edítalo con un editor de texto como nano.
`$ nano Dockerfile`
- Dentro del Dockerfile, agrega las siguientes instrucciones:
###### # Utiliza La Imagen Base De Node.Js
`$ FROM node`
###### # Establece el mantenedor
`$ LABEL maintainer ana.mendoza@tecsup.edu.pe`
###### # Clona el repositorio de GitHub
`$ RUN git clone -q https://github.com/Anitamendoza/lab04-microservicios.git`
###### # Establece el directorio de trabajo
`$ WORKDIR lab04-microservicios`
###### # Instala las dependencias
`$ RUN npm install > /dev/null`
###### # Expone el puerto 5000
`$ EXPOSE 5000`
###### # Comando para iniciar la aplicación
`$ CMD ["npm", "start"]`

Guarda el archivo Dockerfile y sal del editor de texto (en nano, puedes hacerlo con Ctrl + O, luego Enter, y luego Ctrl + X).
- Verifica si el archivo Dokcerfile este cofigurado correctamente:
`$ cat Dockerfile `
###### Paso 7: Crear y ejecutar la imagen Docker en tu instancia de AWS
- Construye la imagen Docker ejecutando el siguiente comando dentro de la carpeta "lab04" donde se encuentra el Dockerfile:
`$ docker build .`
- Cambia el nombre de la imagen si es necesario:
`$ docker tag [ID_DE_LA_IMAGEN] lab04-microservicios`
Verifica que la imagen se haya creado correctamente:
`$ docker images`
- Ejecuta un contenedor basado en la imagen que acabas de crear:
`$ docker run -d -p 9000:5000 lab04-microservicios`

######  Paso 8: Acceder a la aplicación desde un navegador
Puedes acceder a la aplicación desde un navegador utilizando la dirección IP de tu instancia de AWS y el puerto 9000:

`$ http://[tu-direccion-ip-de-aws]:9000/`
`$ http://[tu-direccion-ip-de-aws]:9000/clientes`
`$ http://[tu-direccion-ip-de-aws]:9000/productos`
Asegúrate de reemplazar [tu-direccion-ip-de-aws] con la dirección IP real de tu instancia de AWS.
