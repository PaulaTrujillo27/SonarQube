# SonarQube

#  Creación de Docker Compose 

Como primera instancia, es importante crear un Docker Compose que contendrá lo siguiente:

```
version: '2'

services:
  sonarqube:
    image: sonarqube
    ports:
      - "9000:9000"
    networks:
      - sonarnet
    environment:
      - SONARQUBE_JDBC_URL=jdbc:postgresql://db:5432/sonar
      - SONARQUBE_JDBC_USERNAME=sonar
      - SONARQUBE_JDBC_PASSWORD=sonar
    volumes:
      - sonarqube_conf:/opt/sonarqube/conf
      - sonarqube_data:/opt/sonarqube/data
      - sonarqube_extensions:/opt/sonarqube/extensions
      - sonarqube_bundled-plugins:/opt/sonarqube/lib/bundled-plugins

  db:
    image: postgres
    networks:
      - sonarnet
    environment:
      - POSTGRES_USER=sonar
      - POSTGRES_PASSWORD=sonar
    volumes:
      - postgresql:/var/lib/postgresql
      - postgresql_data:/var/lib/postgresql/data

networks:
  sonarnet:
    driver: bridge

volumes:
  sonarqube_conf:
  sonarqube_data:
  sonarqube_extensions:
  sonarqube_bundled-plugins:
  postgresql:
  postgresql_data:

```

  Se realiza el comando: docker-compose up -d

  ![image](https://github.com/PaulaTrujillo27/SonarQube/assets/71205932/eb4e5ab9-b150-4825-a982-dbdd7aa075d6)

Ahora, es necesario ver la página de SonarQube que despliega el contenedor, entonces, accedemos a la url localhost:9000

![image](https://github.com/PaulaTrujillo27/SonarQube/assets/71205932/683d60c3-4d88-464e-9fac-28c6588d4d20)

Se ingresa a la plataforma de SonarQube utilizando las credenciales de inicio de sesión con el usuario "admin" y la contraseña "admin". A continuación, es necesario cambiar la contraseña predeterminada para poder seguir utilizando el sistema.

![image](https://github.com/PaulaTrujillo27/SonarQube/assets/71205932/ac071e8e-2617-4406-b341-84da3e63ec04)

Ingresamos a lo siguiente:

![image](https://github.com/PaulaTrujillo27/SonarQube/assets/71205932/49c1890c-7666-48b2-b33a-d45db50eac15)

Ahora, se crea un proyecto local, asignándole un nombre, una rama principal y una clave de proyecto, configurandolo globalmente (como predeterminado). A continuación, selecciona el método de análisis local, asigna un nombre representativo al proyecto y genera el token de autenticación para su uso con SonarScanner.

![image](https://github.com/PaulaTrujillo27/SonarQube/assets/71205932/caf8fbff-7775-4297-98c1-f9092d0960e8)

![image](https://github.com/PaulaTrujillo27/SonarQube/assets/71205932/c45222d8-5e60-4343-969a-febb5abd31af)

![image](https://github.com/PaulaTrujillo27/SonarQube/assets/71205932/d4ea3179-31f6-4e9e-82e4-44aaeea96fd3)

Luego, instalar SonarScanner en el sistema operativo

![image](https://github.com/PaulaTrujillo27/SonarQube/assets/71205932/62d083ee-7ef6-46b4-8dc4-076e7934a5a3)

Para llevar a cabo el análisis de nuestro código, es imprescindible instalar Sonar-Scanner. Dependiendo del sistema operativo en el que se encuentren el proyecto y SonarQube, hay varias formas de hacerlo. A continuación, se detallan los pasos para utilizar SonarScanner CLI a partir de un archivo .zip:

- Descomprime el archivo .zip descargado en una carpeta de tu elección.
- Modifica la configuración global para que apunte a tu instancia de SonarQube, editando el archivo ${carpeta_elegida}/conf/sonar-scanner.properties.
- Añade la ruta ${carpeta_elegida}/bin al PATH de las variables de entorno.
- Para comprobar la instalación, abre una terminal y ejecuta el comando sonar-scanner -h, o sonar-scanner.bat -h en Windows. Deberías recibir una respuesta similar a la siguiente:

![image](https://github.com/PaulaTrujillo27/SonarQube/assets/71205932/c87197ec-b399-44c9-9b0b-d9fb7327076c)

# Resultado final del análisis en SonarQube

![image](https://github.com/PaulaTrujillo27/SonarQube/assets/71205932/3b0f7a81-2b0b-4335-837b-39961c516db1)







