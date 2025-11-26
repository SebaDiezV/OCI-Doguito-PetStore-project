# 03 - Creación de VM's y configuración de webserver

## Configuración Instancias de Máquinas Virtuales y reglas de firewall de ingreso

Se configuran las instancias de máquina virtual dentro del compartimento Desarrollo utilizando el usuario doguito-admin, se realiza la configuración como servidor web y se abrirán los puertos de firewall de ingreso, tanto en la instancia como en la red pública

### Creación de llave SSH en Cloud Shell

1. Seleccionar botón de Developer Tools que se sitúa al lado del ícono de anuncios, seleccionar Cloud Shell <b><b>

     <img width="213" height="166" alt="Captura desde 2025-11-19 17-41-23" src="https://github.com/user-attachments/assets/826eefe0-647e-46ff-b140-bac9947f6380" />

2. En la parte inferior de la pantalla se generará una ventana con la instancia de Cloud Shell para trabajar con línea de comandos, esperar a que termine la carga de la ventana, una vez terminada, seleccionar Network en la barra de la instancia y cambiar de OCI service network a Public network, para el resto de los ejercicios que incluyan trabajar con Cloud Shell debe estar seleccionado Public network <b><b>

    <img width="506" height="344" alt="Captura desde 2025-11-19 17-41-50" src="https://github.com/user-attachments/assets/e970b813-4bca-4d15-8136-41ef6ed90f22" />

3. En la instancia de Cloud Shell, crear la carpeta de sistema .ssh, esta carpeta debe ser creada en la raíz del usuario, puedes verificar tu ubicación en la línea de comandos con el comando pwd
   
       pwd  
       mkdir .ssh
   
    <img width="388" height="76" alt="Captura desde 2025-11-19 17-44-17" src="https://github.com/user-attachments/assets/06ce8f47-26a0-42db-89ef-5c1d5fccc9be" />

4. Ingresar a la carpeta .ssh creada, una vez ahí, ejecutar el comando para crear la llave criptográfica rsa, con esto se generan un par de llaves pública/privada con el nombre cloudshellkey y cloudshellkey.pub

       cd .ssh
       ssh-keygen -b 2048 -t rsa -f cloudshellkey
       ls

     <img width="622" height="29" alt="Captura desde 2025-11-19 18-32-22" src="https://github.com/user-attachments/assets/5cab3913-eab7-4a27-b3bd-183eb865f68e" />
     <img width="379" height="53" alt="Captura desde 2025-11-19 18-33-25" src="https://github.com/user-attachments/assets/01953313-5c6a-433a-b725-78a8e50fd9a5" />

   Minimiza la ventana de Cloud Shell, estas llaves serán utilizadas más adelante para conectar a las instancias de Virtual Machine


### Creación de VM's

1. En el menú desplegable de OCI, seleccionar Compute y luego seleccionar Instances
    <img width="584" height="352" alt="Captura desde 2025-11-24 16-25-02" src="https://github.com/user-attachments/assets/c95d65e1-ee04-4650-8b37-5ef194df0881" />

2. Seleccionar Create Instance <b>
<b>
    <img width="584" height="352" alt="Captura desde 2025-11-24 16-25-18" src="https://github.com/user-attachments/assets/0dd441a4-6d02-45dc-9298-7d48df9d25a2" />

4. Dar un nombre a la VM, seleccionar el compartimento Desarrollo y seleccionar Avaibility Domain, en este caso al estar en la región de Chile, solo hay un Avaibility Domain disponible
    <img width="990" height="719" alt="Captura desde 2025-11-24 16-36-00" src="https://github.com/user-attachments/assets/0a5b188c-700f-4c21-8750-f3a880f5673b" />

5. En la sección de Image and Shape, seleccionar Change Image
    <img width="1223" height="567" alt="Captura desde 2025-11-25 11-13-08" src="https://github.com/user-attachments/assets/e1fb657b-dbdf-44fa-867a-10cc0e614036" />

6. Mantener la selección de Oracle Linux, el compartimento debe ser Desarrollo
    <img width="1243" height="674" alt="Captura desde 2025-11-25 11-13-35" src="https://github.com/user-attachments/assets/d9ab2dfc-6f9c-4741-91a8-288cd4d59630" />

7. En Image name, seleccionar Oracle Linux 8, presionar Select image
    <img width="1403" height="725" alt="Captura desde 2025-11-25 11-13-52" src="https://github.com/user-attachments/assets/4942c944-ee10-4c43-955d-ce7f0dfadd83" />

8. En la sección Shape, seleccionar Change shape
    <img width="860" height="513" alt="Captura desde 2025-11-25 11-14-14" src="https://github.com/user-attachments/assets/4b7be417-17ee-4623-85c9-4434673d7641" />

> Nota: En el ejercicio original se utiliza un shape de instancia gratuita que no se encuentra disponible, por lo que se utiliza uno distinto

8. En Shape series seleccionar AMD, en Shape name seleccionar VM.Standard.E4.Flex, presionar Select shape, seleccionar Next
    <img width="1423" height="668" alt="Captura desde 2025-11-25 11-14-42" src="https://github.com/user-attachments/assets/ce11de55-817a-4865-8ff1-46ae4b28000b" />
    <img width="824" height="656" alt="Captura desde 2025-11-25 11-14-58" src="https://github.com/user-attachments/assets/ccd11b1c-c159-4e88-84c6-25de6f0375fa" />

9. En la sección de Security, no se realiza ningún cambio, seleccionar next
    <img width="840" height="439" alt="Captura desde 2025-11-25 11-16-06" src="https://github.com/user-attachments/assets/4da47dbb-32e4-415b-b5fd-dbf201bda182" />

10. En la sección de networking, se le da un nombre a la VNIC que se asignará a la instancia, seleccionar el compartimento de Desarrollo y elegir la VCN creada con anterioridad,
también seleccionar la subnet publica

    <img width="961" height="698" alt="Captura desde 2025-11-25 11-17-52" src="https://github.com/user-attachments/assets/e2ae2cfa-f124-47a9-b813-0b13fbd89c47" />

11. La configuraciones de dirección pública y privada de IPv4 se dejan por defecto para este ejercicio
    <img width="1341" height="696" alt="Captura desde 2025-11-25 11-18-43" src="https://github.com/user-attachments/assets/bbc91922-a972-4bd0-a041-586d87db94d4" />

12. En la sección Add SSH keys, se selecciona Paste public key, se habilita un espacio para pegar la llave publica SSH
    <img width="1341" height="696" alt="Captura desde 2025-11-25 11-29-37" src="https://github.com/user-attachments/assets/b7d487d4-3ed3-4582-95fc-38447e67be72" />
    
    Sin salir de la página de configuración, vuelve a abrir la ventana de Cloud Shell, estando en la carpeta .ssh utilizada en el primer paso, ejecutar el comando       cat para visibilizar la llave publica

        cat cloudshellkey.pub
    <img width="510" height="56" alt="Captura desde 2025-11-25 11-30-01" src="https://github.com/user-attachments/assets/5dceab5d-5fa6-49e7-97ca-080f5e031ce0" />
    
    Copiar y pegar toda la salida del comando en el espacio para pegar la llave publica SSH, cuidado con los espacios en blanco, click Next<b>
    <b>
    <img width="938" height="419" alt="Captura desde 2025-11-25 11-30-27" src="https://github.com/user-attachments/assets/0720fd10-2a0e-486c-beaf-5f8d5ea21027" />
    
13. En la sección Boot volume, deshabilitar la opción Use in-transit encryption, no es necesaria para este ejercicio, click en Next
    <img width="1013" height="418" alt="Captura desde 2025-11-25 11-35-14" src="https://github.com/user-attachments/assets/b50200d6-52e6-48b9-b616-b30b368f50c4" />

14. Click en Create para crear la primera VM
    <img width="1788" height="793" alt="Captura desde 2025-11-25 11-35-34" src="https://github.com/user-attachments/assets/0196d36e-541c-4e59-a34c-525e324c9b23" />

15. Repetir los pasos de esta sección para crear una segunda VM, manteniendo el estándar de los nombres para esta nueva instancia
    <img width="1062" height="553" alt="Captura desde 2025-11-25 11-38-24" src="https://github.com/user-attachments/assets/63f49a2e-0d5a-48e0-8f46-83ca0c34812a" />
    <img width="1044" height="303" alt="Captura desde 2025-11-25 11-39-37" src="https://github.com/user-attachments/assets/ef4e67eb-57c9-4e03-a300-191760612f4a" />

### Configuración de VM's como Web Server

1. En el menú desplegable de OCI, seleccionar Compute y luego seleccionar Instances
    <img width="584" height="352" alt="Captura desde 2025-11-24 16-25-02" src="https://github.com/user-attachments/assets/c95d65e1-ee04-4650-8b37-5ef194df0881" />

2. Seleccionar la primera instancia creada, en la sección Instance access, se puede visibilizar la ip publica de la VM, abrir la instancia Cloud Shell como se especifica en la primera parte de este documento, ingresar a la carpeta .ssh y ejecutar el siguiente comando para conectar remotamente a la instancia

        ssh opc@<ip-instancia> -i cloudshellkey
Al ingresar la primera vez te solicita confirmar el acceso , escribir yes
    <img width="1107" height="434" alt="Captura desde 2025-11-25 11-47-34" src="https://github.com/user-attachments/assets/bbe29946-366c-4ea1-8c2b-49a01d3e4b3e" />

3. una vez conectado a la instancia, ejecutar el siguiente comando para instalar el servidor HTTP Apache

        sudo yum -y install httpd
   <b>
 <img width="324" height="29" alt="Captura desde 2025-11-25 12-03-20" src="https://github.com/user-attachments/assets/afe7d3b0-e263-41a9-9110-e1548355ab1a" /><b>  
<b>
 <img width="491" height="214" alt="Captura desde 2025-11-25 12-00-56" src="https://github.com/user-attachments/assets/e89494d4-1664-4d22-ad5a-70b46cddda67" />

4. A continuación ejecutar el siguiente comando para abrir el puerto 80 del firewall de la instancia para recibir tráfico TCP y luego reiniciar el firewall para que ejecute el cambio

       sudo firewall-cmd --permanent --add-port=80/tcp
       sudo firewall-cmd --reload 
    <img width="478" height="63" alt="Captura desde 2025-11-25 12-05-15" src="https://github.com/user-attachments/assets/bd0001d3-900b-45d0-b046-d7805535eba5" />  <b>  
    <img width="478" height="63" alt="Captura desde 2025-11-25 12-06-07" src="https://github.com/user-attachments/assets/139e73c2-0b45-4a8e-9d14-1361e1dde878" />

5. Ejecutar el siguiente comando para iniciar el servidor HTTP Apache

        sudo systemctl start httpd

     <img width="478" height="63" alt="Captura desde 2025-11-25 12-06-57" src="https://github.com/user-attachments/assets/5080a62c-cf2b-426f-9cf8-f2081f1274e1" />

6. Cambiar a usuario root con el siguiente comando

        sudo su
     <img width="320" height="54" alt="Captura desde 2025-11-25 12-08-11" src="https://github.com/user-attachments/assets/8142dcb1-4022-45c1-a55c-978bf3c6812c" />


7. Cambiar el texto contenido del archivo index.html con un mensaje personalizado con el siguiente comando

         echo "<h1>Doguito Petshop Server 1</h1>" >> /var/www/html/index.html
   
     <img width="643" height="94" alt="Captura desde 2025-11-25 12-11-00" src="https://github.com/user-attachments/assets/0260bc63-167f-42df-ad89-3a55afa9e2ea" />  
<b>
        Salir del usuario root usando el comando exit

8. Minimizar la instancia Cloud Shell para volver a la página de información de la VM, dirigirse a la pestaña Networking
    <img width="555" height="253" alt="Captura desde 2025-11-25 12-11-33" src="https://github.com/user-attachments/assets/2b414807-8a1e-4621-a3ad-8403aa9f06fa" />

9. En la sección Primary VNIC, en subnet, seleccionar Public subnet-VCN1
    <img width="702" height="564" alt="Captura desde 2025-11-25 12-15-14" src="https://github.com/user-attachments/assets/8e70e08c-4e48-42f0-93ff-9f7b0e4f2109" />

10. En Public subnet-VCN1, seleccionar la pestaña Security y seleccionar Default Security List for VCN1
    <img width="702" height="564" alt="Captura desde 2025-11-25 12-15-43" src="https://github.com/user-attachments/assets/a9f04953-ef23-4072-89af-bc0fff15750a" />

11.  En Default Security List for VCN1 seleccionar Security rules, en la sección Ingress Rules seleccionar Add ingress rules<b>  
<b>
     <img width="1502" height="709" alt="Captura desde 2025-11-25 12-16-03" src="https://github.com/user-attachments/assets/746b956c-f78e-4586-b6f7-4a94905fef6c" />  <b>
     <img width="395" height="263" alt="Captura desde 2025-11-25 12-17-13" src="https://github.com/user-attachments/assets/4ce1ac8c-35c1-47af-9885-3f9d3a071064" />

12.  Ingresar la siguiente información para crear una nueva regla de ingreso, click en Add ingress rule  
    
   |Configuración|Valor|
   |---|---|   
   |Source type | CIDR|
   |Source CIDR | 0.0.0.0/0|
   |Destination port range | 80|<b>
<b>
  <img width="1765" height="789" alt="Captura desde 2025-11-25 12-18-10" src="https://github.com/user-attachments/assets/dd2f491f-10f4-4e29-9cb8-badc4b3f8b34" />


13. Regresar a la página principal de la VM, copiar la dirección IP publica de la instancia y pegarla en un navegador web, debe aparecer el texto cambiado en index.html<b>    
    <img width="596" height="189" alt="Captura desde 2025-11-25 12-19-16" src="https://github.com/user-attachments/assets/c214d8f2-6c5e-4a30-9f2a-1840bf75f226" />

14. Realizar los pasos 1 al 7 para configurar la segunda VM, colocando el texto como Doguito Petshop Server 2 en el archivo index.hatml de esa instancia<b>  
    <img width="650" height="29" alt="Captura desde 2025-11-25 12-33-00" src="https://github.com/user-attachments/assets/8e1a2730-ac90-4655-8273-4b8faa94050c" />

15. Realizar el paso 13 en la segunda VM, los pasos del 8 al 12 se omiten ya que la segunda instancia se encuentra en la misma VCN1 que la primera<b>  
    <img width="533" height="143" alt="Captura desde 2025-11-25 12-33-16" src="https://github.com/user-attachments/assets/aee558fe-80dd-4e9b-9599-dded944560d0" />

    
