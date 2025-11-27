# 06 - Implementando una API en OCI
## Configuración de la API en las VM para el proyecto Doguito App
A continuación, configuraremos las VM's para la utilización de la API de Doguito, conectaremos nuestra base de datos Autonomous AI Database y abriremos el puerto para conexión tanto en VM como en listas de seguridad de subred

### Configuración de VM
1. En el menú desplegable de OCI, seleccionar Compute y luego seleccionar Instances
    <img width="584" height="352" alt="Captura desde 2025-11-24 16-25-02" src="https://github.com/user-attachments/assets/c95d65e1-ee04-4650-8b37-5ef194df0881" />

2. Seleccionar la primera VM creada anteriormente  
    <img width="279" height="88" alt="Captura desde 2025-11-26 15-29-48" src="https://github.com/user-attachments/assets/8f286eb0-3d4b-4d39-8ee8-6069e2ad165f" />

3. Seleccionar botón de Developer Tools que se sitúa al lado del ícono de anuncios, seleccionar Cloud Shell <b><b>
    <img width="213" height="166" alt="Captura desde 2025-11-19 17-41-23" src="https://github.com/user-attachments/assets/826eefe0-647e-46ff-b140-bac9947f6380" />

4. En Cloud Shell, conectar a instancia a través de su IP Pública utilizando el siguiente comando

        cd .ssh
        ssh opc@<ip-instancia> -i cloudshellkey
    <img width="645" height="211" alt="Captura desde 2025-11-26 15-33-45" src="https://github.com/user-attachments/assets/d11a31fb-894b-48ef-8ebe-93700a2b81e1" />

6. Instalar git en la instancia para poder clonar repositorios, si solicita, colocar "y" para que continue la instalación

        sudo dnf install git
    <img width="666" height="349" alt="Captura desde 2025-11-26 15-35-50" src="https://github.com/user-attachments/assets/2a2a6801-b4d2-4f3a-8732-431f8e4774df" />

8. Una vez instalado git, clonamos el repositorio donde se encuentra la API (se deja una copia del repositorio también en la página principal de este github), se puede verificar que carpeta fue clonada utilizando el comando ls

        git clone https://github.com/HarlandLohora/doguito-api-es
        ls
    <img width="548" height="171" alt="Captura desde 2025-11-26 15-37-41" src="https://github.com/user-attachments/assets/b7b353a6-79fb-48ce-85ad-b0f97dad458b" />

9. Instalamos el entorno de ejecución de Node.js, en el proyecto original se instala la versión 16, para este proyecto se utiliza la versión 24 que es más estable, colocar "y" para que continue la instalación

        sudo dnf install @nodejs:24
    <img width="457" height="391" alt="Captura desde 2025-11-26 15-39-10" src="https://github.com/user-attachments/assets/470b9946-7e82-4be2-b8ae-170465cfe339" />

10. Ingresar a la carpeta de la API, se puede revisar lo que contiene con el comando ls

        cd doguito-api-es
        ls
    <img width="588" height="94" alt="Captura desde 2025-11-26 15-58-44" src="https://github.com/user-attachments/assets/955330ca-b96d-4eb6-8b22-11b70fba5f2b" />

11. Instalar los paquetes de Node.js en la carpeta de API, esperar a que termine la instalación

        npm install
    <img width="375" height="93" alt="Captura desde 2025-11-26 15-59-32" src="https://github.com/user-attachments/assets/bf9d9217-7030-4f57-91c3-d7c16cbcb064" />

12. En este punto, debemos quitar los paquetes RPM y dependencias legacy que trae la imagen de Oracle Linux 8, ejecutar los siguientes comandos

        sudo dnf remove oracle-instantclient19.5-basic.x86_64
        sudo dnf remove oracle-release-el8
    <img width="661" height="168" alt="Captura desde 2025-11-26 16-11-41" src="https://github.com/user-attachments/assets/9b5259ad-98e9-408b-a2e3-2e8980a14b43" />

13. Instalar el paquete de configuración del repositorio para Oracle Instant Client, colocar "y" para que continue la instalación

        sudo dnf install oracle-instantclient-release-el8
    <img width="679" height="258" alt="Captura desde 2025-11-26 16-15-34" src="https://github.com/user-attachments/assets/58c3775a-4da0-4107-a66b-3cce3e5f625f" />

14. Instala el paquete oracle-instantclient-basic, colocar "y" para que continue la instalación

        sudo dnf install oracle-instantclient-basic
    <img width="567" height="244" alt="Captura desde 2025-11-26 16-17-02" src="https://github.com/user-attachments/assets/73b720a6-a16a-495e-9e90-3ef25f9cbec9" />

### Conectar Autonomous AI Database con API

1. En el menú desplegable de OCI, dirigirse a Oracle AI Database, luego seleccionar Autonomous AI Database
    <img width="729" height="490" alt="Captura desde 2025-11-26 15-00-24" src="https://github.com/user-attachments/assets/721db46c-fffc-4053-953d-3c8528c1d523" />

2. Ingresar a la base de datos creada con anterioridad  
    <img width="498" height="319" alt="Captura desde 2025-11-26 16-25-45" src="https://github.com/user-attachments/assets/bb6c35ac-354d-4db4-960f-fc9060d3477b" />

3. Seleccionar Database connection
    <img width="1206" height="132" alt="Captura desde 2025-11-26 16-25-59" src="https://github.com/user-attachments/assets/38c5ebbb-3c00-41b9-9883-c9c801958e6d" />

4. Crear un password para la Wallet y presionar botón Download, con esto descargaremos un archivo ZIP a nuestro computador local
    <img width="1394" height="506" alt="Captura desde 2025-11-26 16-27-12" src="https://github.com/user-attachments/assets/e1bbe2ca-b49d-48f4-a949-5f30c4fb3616" />

5. En la ventana de Cloud Shell, usar el comando exit para cerrar la conexión a la VM y regresar a la instancia de Cloud Shell, debes quedar en la raíz de Cloud Shell, por lo que si te encuentras en la carpeta .ssh utilizar el comando cd ..

        exit
        cd .. 
  
    <img width="381" height="113" alt="Captura desde 2025-11-26 16-28-51" src="https://github.com/user-attachments/assets/d45ddd47-54bc-4414-9f99-448cf82c357f" />

7. En la ventana de Cloud Shell, seleccionar el ícono de engranaje y seleccionar Upload  
    <img width="238" height="272" alt="Captura desde 2025-11-26 16-29-05" src="https://github.com/user-attachments/assets/69a7f481-2b25-4174-bebb-1d4c791547dd" />

8. Arrastrar o seleccionar el archivo ZIP descargado anteriormente, luego selecciona Upload, esto deja el archivo ZIP en la raíz de la instancia Cloud Shell  
    <img width="614" height="244" alt="Captura desde 2025-11-26 16-29-42" src="https://github.com/user-attachments/assets/24e18e32-95dd-4064-a20c-ef770cbea272" />
    <img width="637" height="184" alt="Captura desde 2025-11-26 16-29-59" src="https://github.com/user-attachments/assets/7319a3eb-3fb4-4d13-bd35-2b835eba1c8e" />

9. Copiar el archivo ZIP de la instancia de Cloud Shell hacia la VM donde se está configurando la API con el siguiente comando

        scp -i .ssh/cloudshellkey <nombre-archivo>.zip opc@<ip-instancia>:/home/opc/
     <img width="861" height="56" alt="Captura desde 2025-11-26 17-23-30" src="https://github.com/user-attachments/assets/8e18c219-fa4c-487b-b364-a306bcbcb603" />

10. Volver a conectar a la VM donde se esta configurando la API
    <img width="615" height="87" alt="Captura desde 2025-11-26 17-25-14" src="https://github.com/user-attachments/assets/5e927a32-6d8e-4476-9a86-729270dff415" />

11. Dentro de la VM, copiar el archivo ZIP a la ruta /usr/lib/oracle/21/client64/lib/network/admin/

        sudo <nombre_archivo>.zip /usr/lib/oracle/21/client64/lib/network/admin/
      <img width="685" height="44" alt="Captura desde 2025-11-26 17-28-42" src="https://github.com/user-attachments/assets/bdefeca7-d8cf-405e-9613-4c36b6711aef" />

12. ingresar a la carpeta donde copió archivo ZIP, luego revisar que la copia del archivo se encuentre correctamente en la ruta

        cd /usr/lib/oracle/21/client64/lib/network/admin/
        ls
      <img width="588" height="73" alt="Captura desde 2025-11-26 17-29-38" src="https://github.com/user-attachments/assets/b4d2662d-af2a-46a2-aa2b-9780deafa4d9" />

13. Descomprimir archivo ZIP en la ruta donde fue copiado

        sudo unzip -B Wallet_DOGUITODB.zip
      <img width="428" height="186" alt="Captura desde 2025-11-26 17-30-33" src="https://github.com/user-attachments/assets/3ef78803-925c-454c-b70e-79dcf3afb868" />

14. Regresar a la ruta raíz de la VM para ingresar a la carpeta de la API

        cd
        cd doguito-api-es
      <img width="280" height="72" alt="Captura desde 2025-11-26 17-31-02" src="https://github.com/user-attachments/assets/2cdd72f9-abbc-4118-af37-251961f7cfc2" />

15. A continuación definir las variables de entorno para la conexión de la API a la base de datos, La información de CONNECT_STRING se encuentra en la misma página donde se descarga el archivo ZIP de la base de datos, iniciar npm, con esto la API queda escuchando en puerto 3000 por lo configuración es correcta, usar combinación de teclas crtl + c para detener npm

        export DB_USER=ADMIN
        export DB_PASSWORD=<contraseña de ADMIN generada con la creación de Autonomous AI Database>
        export CONNECT_STRING=dbdoguito_high
        npm start
      <img width="509" height="215" alt="Captura desde 2025-11-26 17-35-09" src="https://github.com/user-attachments/assets/93aeb8c5-9a2c-4a05-95df-6f1dafe55e7f" />


### Habilitar puerto 3000 para conexión a API

1. Abrir el puerto 3000 en firewall de VM para que pueda recibir tráfico tcp, luego reiniciar firewall para que utilice la nueva configuración, iniciar npm

        sudo firewall-cmd --permanent --add-port=3000/tcp
        sudo firewall-cmd --reload
        npm start
    <img width="568" height="72" alt="Captura desde 2025-11-26 17-40-22" src="https://github.com/user-attachments/assets/72023ec4-86e2-4da5-996c-f3b04de09f74" />
3.  Minimizar la instancia Cloud Shell para volver a la página de información de la VM, dirigirse a la pestaña Networking
    <img width="555" height="253" alt="Captura desde 2025-11-25 12-11-33" src="https://github.com/user-attachments/assets/2b414807-8a1e-4621-a3ad-8403aa9f06fa" />

4. En la sección Primary VNIC, en subnet, seleccionar Public subnet-VCN1
    <img width="702" height="564" alt="Captura desde 2025-11-25 12-15-14" src="https://github.com/user-attachments/assets/8e70e08c-4e48-42f0-93ff-9f7b0e4f2109" />

5. En Public subnet-VCN1, seleccionar la pestaña Security y seleccionar Default Security List for VCN1
    <img width="702" height="564" alt="Captura desde 2025-11-25 12-15-43" src="https://github.com/user-attachments/assets/a9f04953-ef23-4072-89af-bc0fff15750a" />

6.  En Default Security List for VCN1 seleccionar Security rules, en la sección Ingress Rules seleccionar Add ingress rules<b>  
    <img width="1502" height="709" alt="Captura desde 2025-11-25 12-16-03" src="https://github.com/user-attachments/assets/746b956c-f78e-4586-b6f7-4a94905fef6c" />  <b>
    <img width="395" height="263" alt="Captura desde 2025-11-25 12-17-13" src="https://github.com/user-attachments/assets/4ce1ac8c-35c1-47af-9885-3f9d3a071064" />  
     
7.  Ingresar la siguiente información para crear una nueva regla de ingreso, click en Add ingress rule  
    
     |Configuración|Valor|
     |---|---|   
     |Source type | CIDR|
     |Source CIDR | 0.0.0.0/0|
     |Destination port range | 3000|<b>
    <img width="1778" height="729" alt="Captura desde 2025-11-26 17-42-06" src="https://github.com/user-attachments/assets/656ad26c-5880-439f-b0b2-2a79d8b8fa39" />

  8. En el navegador web, ingresar la dirección IP publica de la VM agregando al final :3000, aparece la página de bienvenida de la API

         http://<ip-instancia>:3000
       <img width="748" height="273" alt="Captura desde 2025-11-26 17-42-26" src="https://github.com/user-attachments/assets/ed7cbe23-1368-472c-99ad-99f945b8e505" />

9. agregar a la dirección /clientes, aparece el registro que esta creado en la base de datos

        http://<ip-instancia>:3000/clientes
     <img width="756" height="281" alt="Captura desde 2025-11-26 17-42-51" src="https://github.com/user-attachments/assets/b200a375-0f18-4415-bd89-c834b81f2fa5" />

11. para verificar el correcto funcionamiento, puedes regresar a crear un nuevo registro en la base Autonomous AI Database (desde el punto 6 en la creación de la base de datos) y volver a refrescar el navegador para ver el nuevo registro a través de la web
      <img width="893" height="930" alt="Captura desde 2025-11-26 17-45-16" src="https://github.com/user-attachments/assets/6793530c-b054-4e13-be25-77ce99f75e58" />
      <img width="1480" height="503" alt="Captura desde 2025-11-26 17-45-27" src="https://github.com/user-attachments/assets/8f654a02-8f95-4158-bcd5-d153edd324ab" />
      <img width="538" height="377" alt="Captura desde 2025-11-26 17-45-42" src="https://github.com/user-attachments/assets/b0d9956e-37de-4545-b478-20de2166c686" />

Repetir los pasos en la segunda instancia, con excepción de la descarga de la Wallet de Autonomous AI Database
