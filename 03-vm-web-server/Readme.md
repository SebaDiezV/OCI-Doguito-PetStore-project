# 03 - Creación de VM's y configuración de webserver

## Configuración Instancias de Maquinas Virtuales y reglas de firewall de ingreso

Se configuran las instancias de maquina virtual dentro del compartimento Desarrollo utilizando el usuario doguito-admin, se realiza la configuración como servidor web y se abriran los puertos de firewall de ingreso, tanto en la instancia como en la red pública

### Creación de llave SSH en Cloud Shell

1. Seleccionar botón de Developer Tools que se situa al lado del ícono de anuncios, seleccinar Cloud Shell
    <img width="213" height="166" alt="Captura desde 2025-11-19 17-41-23" src="https://github.com/user-attachments/assets/826eefe0-647e-46ff-b140-bac9947f6380" />

2. En la parte inferior de la pantalla se generará una ventana con la instancia de Cloud Shell para trabajar con línea de comandos, esperar a que termine la carga de la ventana, una vez terminada, seleccionar Network en la barra de la instancia
3. y cambiar de OCI service network a Public network <b>
<b>
    <img width="506" height="344" alt="Captura desde 2025-11-19 17-41-50" src="https://github.com/user-attachments/assets/e970b813-4bca-4d15-8136-41ef6ed90f22" />

4. En la instancia de Cloud Shell, crear la carpeta de sistema .ssh, esta carpeta debe ser creada en la raiz del usuario, puedes verificar tu ubicación en la línea de comandos con el comando pwd
   
       pwd  
       mkdir .ssh
   
    <img width="388" height="76" alt="Captura desde 2025-11-19 17-44-17" src="https://github.com/user-attachments/assets/06ce8f47-26a0-42db-89ef-5c1d5fccc9be" />

5. Ingresar a la carpeta .ssh creada, una vez ahí, ejecutar el comando para crear la llave criptográfica rsa, con esto se generan un par de llaves pública/privada concon el nombre cloudshellkey y cloudshellkey.pub

       cd .ssh
       ssh-keygen -b 2048 -t rsa -f cloudshellkey
       ls

     <img width="622" height="29" alt="Captura desde 2025-11-19 18-32-22" src="https://github.com/user-attachments/assets/5cab3913-eab7-4a27-b3bd-183eb865f68e" />
     <img width="379" height="53" alt="Captura desde 2025-11-19 18-33-25" src="https://github.com/user-attachments/assets/01953313-5c6a-433a-b725-78a8e50fd9a5" />

   Estas llaves serán utilizadas más adelante para conectar a las instancias de Virtual Machine


### Creación de VM's

1. En el menú desplegable de OCI, seleccionar Compute y luego seleccionar Instances
    <img width="584" height="352" alt="Captura desde 2025-11-24 16-25-02" src="https://github.com/user-attachments/assets/c95d65e1-ee04-4650-8b37-5ef194df0881" />

2. Seleccionar Create Instance
    <img width="584" height="352" alt="Captura desde 2025-11-24 16-25-18" src="https://github.com/user-attachments/assets/0dd441a4-6d02-45dc-9298-7d48df9d25a2" />

3. Dar un nombre a la VM, seleccionar el compartimento Desarrollo y seleccionar Avaibility Domain, en este caso al estar en la región de Chile, solo hay un Avaibility Domain disponible
    <img width="990" height="719" alt="Captura desde 2025-11-24 16-36-00" src="https://github.com/user-attachments/assets/0a5b188c-700f-4c21-8750-f3a880f5673b" />

4. En la sección de Image and Shape, seleccionar Change Image
    <img width="1223" height="567" alt="Captura desde 2025-11-25 11-13-08" src="https://github.com/user-attachments/assets/e1fb657b-dbdf-44fa-867a-10cc0e614036" />

5. Mantener la selección de Oracle Linux, el compartimento debe ser Desarrollo
    <img width="1243" height="674" alt="Captura desde 2025-11-25 11-13-35" src="https://github.com/user-attachments/assets/d9ab2dfc-6f9c-4741-91a8-288cd4d59630" />

6. En Image name, seleccionar Oracle Linux 8, presionar Select image
    <img width="1403" height="725" alt="Captura desde 2025-11-25 11-13-52" src="https://github.com/user-attachments/assets/4942c944-ee10-4c43-955d-ce7f0dfadd83" />

7. En la sección Shape, seleccionar Change shape
    <img width="860" height="513" alt="Captura desde 2025-11-25 11-14-14" src="https://github.com/user-attachments/assets/4b7be417-17ee-4623-85c9-4434673d7641" />

> Nota: En el ejercicio original se utiliza un shape de instancia gratuita que no se encuentra disponible, por lo que se utiliza uno distinto

8. En Shape series seleccionar AMD, en Shape name seleccionar VM.Standard.E4.Flex, presionar Select shape, seleccionar Next
    <img width="1423" height="668" alt="Captura desde 2025-11-25 11-14-42" src="https://github.com/user-attachments/assets/ce11de55-817a-4865-8ff1-46ae4b28000b" />
    <img width="824" height="656" alt="Captura desde 2025-11-25 11-14-58" src="https://github.com/user-attachments/assets/ccd11b1c-c159-4e88-84c6-25de6f0375fa" />

9. En la sección de Security, no se realiza ningún cambio, seleccionar next
  <img width="840" height="439" alt="Captura desde 2025-11-25 11-16-06" src="https://github.com/user-attachments/assets/4da47dbb-32e4-415b-b5fd-dbf201bda182" />

10. En la sección de networking, se le da un nombre a la VNic que se asignará a la instancia, seleccionar el compartimento de Desarrollo y eligir la VCN creada con anterioridad,
también seleccionar la subnet publica

  <img width="961" height="698" alt="Captura desde 2025-11-25 11-17-52" src="https://github.com/user-attachments/assets/e2ae2cfa-f124-47a9-b813-0b13fbd89c47" />


