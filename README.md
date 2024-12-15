
# Desafío LATAM - Módulo 5
Configuración de GitHub Actions para despliegues en EC2.




## Descripción del proyecto
El proyecto implementa un pipeline con Github Actions para:
- Crear una instancia EC2 en AWS y servir un archivo HTML.
- Generar una AMI personalizada a partir de esta instancia.
- Lanzar una nueva instancia EC2 a partir de la AMI creada.
- Limpiar todos los recursos creados (claves SSG, instancias, etc.)




## Paso a paso


##### 1. Configuración de Credenciales AWS
    Se configuran las credenciales de AWS utilizando Github Secrets para permitir que Github interactúe con AWS de forma segura.
    
##### 2. Checkout del código
    Se utiliza actions/checkout para descargar el código de fuente del repositorio.

##### 3. Generar clave SSH (temporal)
    Se crea una clave SSH temporal con ssh-keygen y se importa a AWS.

##### 4. Creación de instancia EC2
    Se lanza una instancia EC2 con una AMI Base (Amazon Linux 2 AMI), usando la clave generada y el grupo de seguridad preconfigurado en AWS.

##### 5. Deploy archivo HTML
    Luego de esperar a que la instancia esté disponible, se configura para servir un archivo HTML estático (index.html).

##### 6. Creación de una AMI personalizada
    Se crea una AMI a partir de la instancia que se acaba de configurar.

##### 7. Lanzamiento de nueva instancia desde AMI
    Luego de esperar que la AMI esté disponible, se lanza una nueva instancia utilizando la ami personalizada.

##### 8. Limpieza de recursos
    Se terminan las instancias de EC2 y se eliminan las claves SSH, además de la AMI creada.


## Ejecución

#### 1. Configurar credenciales de AWS en los secrets del repositorio:

  - *AWS_ACCESS_KEY_ID*
  - *AWS_SECRET_ACCESS_KEY*

#### 2. Crea un grupo de seguridad en AWS que permita el tráfico SSH y HTTP.
&nbsp;&nbsp;&nbsp;&nbsp; Reemplaza el valor de la variable *SECURITY_GROUP_ID* por la id de tu grupo de seguridad en el pipeline.

#### 3. Recuperar ID del subnet.
&nbsp;&nbsp;&nbsp;&nbsp; Reemplaza el valor de la variable *SUBNET_ID* por el id de tu subnet (VPC Default).

#### 4. Realizar push a la rama main.

&nbsp;&nbsp;&nbsp;&nbsp; Realiza un push a la rama *main*  para inicializar el workflow.

## Documentación

[AWS Cli](https://docs.aws.amazon.com/cli/latest/reference/ec2/run-instances.html)

