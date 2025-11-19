# 01 - Creación de Usuarios, Grupos y Políticas

## Configuración de Identidad y Seguridad para la creación de Doguito App

Se procede con la configuración de Compartimentos de Desarrollo y Producción, Usuario de administración para la app, grupo y sus políticas. Para realizar estos pasos se debe usar el 
usuario admin de Tenant

### Creación de Compartimentos 

1. En el menú desplegable de OCI, dirigirse a Identity & Security, seleccionar Compartments
    <img width="786" height="665" alt="Captura desde 2025-11-19 10-52-16" src="https://github.com/user-attachments/assets/9eea63f2-3848-44a4-bfb1-4675e33aa736" /><b>
  
2. Seleccionar el compartimento raíz<b>
<b>
    <img width="510" height="73" alt="Captura desde 2025-11-19 10-53-24" src="https://github.com/user-attachments/assets/73fe6059-cbd8-4e87-a9f4-0a2fdf9a8822" /><b>
  
3. En la sección Child Compartments seleccionamos la opción Create Compartment
    <img width="500" height="241" alt="Captura desde 2025-11-19 10-53-40" src="https://github.com/user-attachments/assets/8f7fad00-44d2-4107-a21d-088877881f85" /><b>

4. Crear el compartimento de Desarrollo, dándole una descripción, seleccionar Create Compartment
    <img width="1781" height="853" alt="Captura desde 2025-11-19 10-55-18" src="https://github.com/user-attachments/assets/3496555e-c629-4f3a-87eb-c1078fba986d" /><b>

5. Repetir los pasos 3 y 4 para crear el compartimento de Producción
    <img width="1781" height="853" alt="Captura desde 2025-11-19 10-55-36" src="https://github.com/user-attachments/assets/d10990be-d5a5-40f3-89ac-7af8143e5353" /><b>

6. Una vez creados, aparecerán listados en Child Compartments
    <img width="1526" height="454" alt="Captura desde 2025-11-19 10-56-15" src="https://github.com/user-attachments/assets/f41209c9-57b2-43b6-abb7-469df3dd67ce" /><b>

### Creación de Usuario Admin para App

1. En el menú desplagable de OCI, dirigirse a Identity & Security, seleccionar Overview
    <img width="616" height="578" alt="Captura desde 2025-11-19 10-57-26" src="https://github.com/user-attachments/assets/4242975a-7199-4434-ae16-be741a25e9f2" /><b>

2. En la zona de Quick Links, seleccionar Users<b>
<b>
     <img width="510" height="200" alt="Captura desde 2025-11-19 10-59-03" src="https://github.com/user-attachments/assets/6b98dfc7-036d-4cbd-9324-7b1236e4d911" /><b>

3. Seleccionar Create<b>
<b>
      <img width="549" height="419" alt="Captura desde 2025-11-19 10-59-53" src="https://github.com/user-attachments/assets/8a69d21e-20a2-4c2e-8638-d95feb9d29ce" /><b>

4. Se deshabilita la opción "Use the Email address as the Username" y llenamos los datos del usuario con la siguiente información:
    |Configuración|Valor|
    |---|---|   
    |First Name | Doguito|
    |Last Name | Admin|
    |Username | doguito-admin|
    |Email | E-mail de preferencia |<b>
    
   Click en Create, llegará un correo a la cuenta indicada solicitando el alta del nuevo usuario en la plataforma OCI<b>
    <img width="1781" height="881" alt="Captura desde 2025-11-19 11-02-04" src="https://github.com/user-attachments/assets/f0eef0b5-de0f-4e8d-a09d-285db6b05c84" /><b>

5. Se muestra el nuevo usuario creado
    <img width="1450" height="442" alt="Captura desde 2025-11-19 11-02-30" src="https://github.com/user-attachments/assets/751de9f4-52cd-488a-80f1-1c72cf0c47e1" /><b>


### Creación de Grupo Admin para App

1. En la misma página de Users, en la sección de abajo, se encuentra Groups, seleccionar botón Create Groups
   <img width="1513" height="236" alt="Captura desde 2025-11-19 11-03-02" src="https://github.com/user-attachments/assets/4b1d3f6b-4f12-44c3-a9ab-1c73c6fdaf38" /><b>

2. Crear grupo con la siguiente información
    |Configuración|Valor|
    |---|---|   
    |Name | admin-doguito|
    |Description | Administración Doguito|
    |Users | doguito-admin|<b>

    Click en Create<b>
    <img width="1781" height="858" alt="Captura desde 2025-11-19 11-04-25" src="https://github.com/user-attachments/assets/dee1449c-739f-4c62-ae40-6192f062b351" /><b>

### Creación de Políticas

1. En el menú desplegable de OCI, dirigirse a Identity & Security, seleccionar Policies
    <img width="590" height="593" alt="Captura desde 2025-11-19 11-05-37" src="https://github.com/user-attachments/assets/085841dc-89a0-47ca-9822-6c5d8bcb9524" /><b>

2. Seleccionar Create Policy<b>
<b>
  <img width="503" height="261" alt="Captura desde 2025-11-19 11-06-13" src="https://github.com/user-attachments/assets/8c10a7a2-9971-40f2-b7a9-3c2b16e4e5e4" /><b>

3. Crear la política con los siguientes datos:
    |Configuración|Valor|
    |---|---|   
    |Name | politica-admin-doguito|
    |Description | Politica para administración Doguito|
    |Compartment | root|<b>

    Policy Builder
    |Configuración|Valor|
    |---|---|   
    |Common policy templates | Let admin manage Compute instance configuration, instance pools, and cluster networks|

  <img width="1022" height="719" alt="Captura desde 2025-11-19 11-08-46" src="https://github.com/user-attachments/assets/12d3f534-ccb7-44d7-b83f-fd226ee2eb92" /><b>

    
5. Seleccionar Goups y seleccionar los siguientes datos:
    |Configuración|Valor|
    |---|---|   
    |Select a group| admin-doguito|
    |Location | Desarrollo|<b>

    <img width="1355" height="609" alt="Captura desde 2025-11-19 11-12-32" src="https://github.com/user-attachments/assets/8b304dd6-8e0e-4c43-9443-14959692d33f" /><b>

6. Volver a sección Policy Builder y seleccionar botón Show manual editor
    <img width="856" height="421" alt="Captura desde 2025-11-19 11-10-30" src="https://github.com/user-attachments/assets/f9f82b01-2f15-4c31-92d5-5bd05e060c99" /><b>

7. Reemplazar donde dice "Compute-management-family" por "all-resources", dándole permiso sobre todos los recursos al grupo admin doguito, presionar Create
    <img width="856" height="421" alt="Captura desde 2025-11-19 11-10-52" src="https://github.com/user-attachments/assets/21dbf29d-3346-4621-a7b5-703a7e4a90d1" />
    <img width="856" height="421" alt="Captura desde 2025-11-19 11-11-16" src="https://github.com/user-attachments/assets/24f6a9a8-1555-4d0d-b928-94450e2df0d2" /><b>

8. En la página de Policies, ingresar a la política recién creada
    <img width="1332" height="483" alt="Captura desde 2025-11-19 11-14-33" src="https://github.com/user-attachments/assets/22c98155-3a83-446b-9dbd-2340f6eb2e3b" /><b>

9. En la pestaña Statements seleccionar Edit policy statements
    <img width="1332" height="483" alt="Captura desde 2025-11-19 11-14-50" src="https://github.com/user-attachments/assets/d52ce5c4-81e4-4fb6-a157-1c3a15fab856" /><b>

10. Presionar botón Aditional rule y agregar las siguientes reglas para permitir el uso de Cloud Shell y de la red pública en Cloud Shell para los usuarios del grupo admin-doguito:

        Allow group 'Default'/'admin-doguito' to use cloud-shell in tenancy
        Allow group 'Default'/'admin-doguito' to use cloud-shell-public-network in tenancy
    
  Salvar los cambios
    <img width="1428" height="879" alt="Captura desde 2025-11-19 11-15-31" src="https://github.com/user-attachments/assets/0665570b-0118-4f8c-8698-ff48004865cf" />


**Para los siguientes pasos de este manual, se usará el usuario doguito-admin**
