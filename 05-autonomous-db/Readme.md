# 05 - Configuración de Autonomous AI Database
## Configuración de Base de Datos de clientes para Doguito App
Se procede con la creación y configuración de la base de datos de clientes en formato JSON en Autonomous AI Database de Oracle
### Configuración de Autonomous AI Database

1. En el menú desplegable de OCI, dirigirse a Oracle AI Database, luego seleccionar Autonomous AI Database
    <img width="729" height="490" alt="Captura desde 2025-11-26 15-00-24" src="https://github.com/user-attachments/assets/721db46c-fffc-4053-953d-3c8528c1d523" />

2. Presionar botón Create Autonoumous AI Database
    <img width="725" height="504" alt="Captura desde 2025-11-26 15-00-49" src="https://github.com/user-attachments/assets/d8b4ce95-d85e-4ed7-b595-72cc9e4ef7f6" />

3. Dar un Display name y Database name a la base de datos que está creando, se sugiere utilizar el mismo nombre, asegurar que se está creando la base de datos en el compartimento de Desarrollo y seleccionar Workload type como JSON
    <img width="1389" height="717" alt="Captura desde 2025-11-26 15-02-02" src="https://github.com/user-attachments/assets/fa76f290-62b9-46bb-80fb-3afbcc7bb8e6" />

4. Según pasos originales, se debía utilizar en Database configuration la opción Always free, esta opción no se encuentra disponible, se desactiva opción de Compute autoscalling y el resto de las opciones queda por defecto (si en el futuro, se encuentra disponible, utilizar opción Always free)
    <img width="1387" height="687" alt="Captura desde 2025-11-26 15-06-56" src="https://github.com/user-attachments/assets/473a7c87-54b3-4cf5-8b74-da6904c2fa8d" />    

5. En la sección Administrator credentials creation, se debe otorgar una clave segura al usuario ADMIN de Autonomous AI Database, **esta clave debe quedar registrada ya que será utilizada en pasos posteriores**. En la sección Network access, seleccionar opción Secure acces from everywhere, click en Create para crear la base de datos
    <img width="1779" height="725" alt="Captura desde 2025-11-26 15-08-05" src="https://github.com/user-attachments/assets/8e5c7806-524d-41bc-aa8d-80041ba1e665" />

6. Una vez se encuentre disponible la Autonoumus AI Database, abrir el menú desplegable Database actions y seleccionar la opción View all database actions
    <img width="1141" height="369" alt="Captura desde 2025-11-26 15-10-53" src="https://github.com/user-attachments/assets/ac4aac97-7aa2-4890-8990-5ae593e62f21" />

7. En la pantalla de inicio de Database actions, seleccionar la pestaña Desarrollo y seleccionar JSON
    <img width="1276" height="847" alt="Captura desde 2025-11-26 15-12-06" src="https://github.com/user-attachments/assets/a1bc2b9d-2c27-4565-aa8d-6eb51ccbd7ac" />

8. En la sección Gestionar los Datos de JSON, seleccionar Crear recopilación
    <img width="948" height="504" alt="Captura desde 2025-11-26 15-12-25" src="https://github.com/user-attachments/assets/40f4639f-037b-48dd-be75-1efc4f853b2e" />

9. En Nombre de recopilación, colocar por nombre **clientes** y quitar check de Compatible con Mongo DB, presionar botón Crear
    <img width="551" height="222" alt="Captura desde 2025-11-26 15-13-09" src="https://github.com/user-attachments/assets/960040a9-2c3e-4bc8-9053-a6cf9c967572" />
    <img width="551" height="945" alt="Captura desde 2025-11-26 15-13-16" src="https://github.com/user-attachments/assets/0ac957bd-0b33-447e-add2-86214c2f7531" />

10. En la recopilación clientes creada, seleccionar botón Nuevo documento de JSON
    <img width="414" height="255" alt="Captura desde 2025-11-26 15-13-56" src="https://github.com/user-attachments/assets/c0410b39-3e43-4f73-9503-bae84d460e28" />

11. Crear un nuevo documento de JSON como en el ejemplo, presionar botón Crear
    <img width="905" height="934" alt="Captura desde 2025-11-26 15-15-02" src="https://github.com/user-attachments/assets/8755d512-b47a-49b5-b2f1-c3ba0f490dcb" />

12. Revisar que nuevo documento de JSON fue creado correctamente
    <img width="669" height="562" alt="Captura desde 2025-11-26 15-15-15" src="https://github.com/user-attachments/assets/96d734f0-7779-4bcf-8690-57ca643fcfba" />

