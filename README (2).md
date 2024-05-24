# Despliegue de Infraestructura de Telemática

Este repositorio contiene configuraciones de Terraform y archivos de Docker para desplegar un servidor web en AWS.

## Prerrequisitos

Asegúrate de tener instalados en tu AWS CloudShell:
- Git
- Terraform

## Instalación y Configuración

### Paso 1: Instalar Terraform

1. Clona el repositorio `tfenv` para gestionar las versiones de Terraform:
    ```sh
    git clone https://github.com/tfutils/tfenv.git ~/.tfenv
    ```
2. Crea un directorio `bin` en tu directorio de inicio y enlaza los binarios de `tfenv` a él:
    ```sh
    mkdir ~/bin
    ln -s ~/.tfenv/bin/* ~/bin/
    ```
3. Instala la versión 1.2.5 de Terraform usando `tfenv`:
    ```sh
    tfenv install 1.2.5
    tfenv use 1.2.5
    ```
4. Verifica la instalación de Terraform:
    ```sh
    terraform --version
    ```

### Paso 2: Descargar los Scripts de Terraform

1. Clona el repositorio que contiene las configuraciones de Terraform:
    ```sh
    git clone https://github.com/daniellelooo/finaltelematica.git
    ```
2. Navega al directorio del proyecto:
    ```sh
    cd telematica
    ```

### Paso 3: Aplicar la Configuración de Terraform

1. Inicializa Terraform para descargar los plugins y módulos necesarios:
    ```sh
    terraform init
    ```
2. Aplica la configuración de Terraform para provisionar la infraestructura:
    ```sh
    terraform apply
    ```
3. Escribe `yes` para confirmar y aplicar los cambios. Copia la dirección IP pública proporcionada en la salida.

## Acceder al Servidor Web

Espera a que el servidor inicie, luego accede a tu servidor web utilizando la dirección IP pública proporcionada en un navegador web.

## Paso 4: Desplegar el Contenedor de Docker en el Servidor

1. Conéctate al servidor utilizando la dirección IP pública:
    ```sh
    ssh ec2-user@<direccion-ip-publica>
    ```
2. Navega al directorio del proyecto:
    ```sh
    cd /telematica
    ```
3. Construye la imagen de Docker:
    ```sh
    sudo docker build -t web-image:v1 .
    ```
4. Ejecuta el contenedor de Docker, mapeando el puerto 3000 en el host al puerto 80 en el contenedor:
    ```sh
    sudo docker run -d -p 3000:80 --name web-container web-image:v1
    ```

## Verificar el Despliegue

Abre tu navegador web y navega a la dirección IP pública del servidor seguida del puerto 3000 para ver tu aplicación web desplegada:

```sh
http://<direccion-ip-publica>:3000

