# 04 - Creación de Load Balancer

## Creación y configuración del Balanceador de Carga para los servidores web de Doguito APP

En este paso se creará el balanceador de carga como un frontend que tendrá en su backend los servidores web creados con anterioridad, con esto ambos servidores quedan disponibles con solo una IP pública

### Creación de Load Balancer

1. En el menú desplegable de OCI, seleccionar Networking, luego Load balancers
    <img width="634" height="429" alt="Captura desde 2025-11-25 12-38-41" src="https://github.com/user-attachments/assets/4c80703c-0451-42b3-8d10-6875ff26a5f1" />

2. En Overview, seleccionar el botón Create load balancer
    <img width="1775" height="378" alt="Captura desde 2025-11-25 12-40-30" src="https://github.com/user-attachments/assets/3aee6656-1af0-4915-90ed-d77cf0a3b9d4" />

3. Se asigna un nombre para el Load Balancer, se selecciona el tipo de visibilidad como Public para recibir tráfico entrante desde internet y para asignar una dirección IP pública se selecciona Ephemeral IP Address
    <img width="1042" height="473" alt="Captura desde 2025-11-25 12-42-04" src="https://github.com/user-attachments/assets/d4bd0fd0-7610-42f1-8223-8d2010e5f4a3" />

4. En Bandwidth, se deja el shape por defecto para el Load Balancer
    <img width="1042" height="473" alt="Captura desde 2025-11-25 12-43-09" src="https://github.com/user-attachments/assets/abc83a8f-97a6-4c03-8e01-b2ef2c9417fc" />

5. Se especifica la VCN y la Public subnet creadas con anterioridad, verificar que todo está siendo seleccionado en el compartimento Desarrollo, click en Next
    <img width="1065" height="422" alt="Captura desde 2025-11-25 12-43-38" src="https://github.com/user-attachments/assets/4039f26d-144b-4003-ae9a-b4324f9d0963" />

6. Al escoger los backend, se debe escoger que política de balanceo de carga se va a utilizar para el Load Balancer, en este caso se utiliza Weighted round robin, presionar botón Add backends
    <img width="1064" height="468" alt="Captura desde 2025-11-25 12-45-35" src="https://github.com/user-attachments/assets/e51e6ab4-9ee1-4faa-93ec-99536c449739" />

7. Seleccionar las dos instancias creadas en los pasos anteriores, presionar botón Add selected backends
    <img width="1193" height="841" alt="Captura desde 2025-11-25 12-46-03" src="https://github.com/user-attachments/assets/502b78af-35bd-4160-8639-89b450662f8c" />
    <img width="1063" height="681" alt="Captura desde 2025-11-25 12-46-15" src="https://github.com/user-attachments/assets/012787fb-e181-4276-aeb4-c393ef50c5b5" />

8. En Specify health check policy, dejamos los valores que entrega por defecto, presionar next
    <img width="1056" height="537" alt="Captura desde 2025-11-25 12-47-14" src="https://github.com/user-attachments/assets/8f78a56c-6f59-416f-a732-a6da3593ca51" />

9. En Configure listener, dar un nombre al listener y en Specify the type of traffic your listener handles seleccionar HTTP, presionar next
    <img width="1074" height="515" alt="Captura desde 2025-11-25 12-48-03" src="https://github.com/user-attachments/assets/a8634af2-5e4c-4715-92ca-22b3ad28c720" />

10. En Manage logging, dejar los valores por defecto para este ejercicio, presionar botón Submit para crear el Load Balancer
    <img width="1296" height="815" alt="Captura desde 2025-11-25 12-56-46" src="https://github.com/user-attachments/assets/5efb71fb-1f32-458f-96d3-6e31020cea1a" />

11. Una vez que el estado del nuevo Load Balancer se Active, ingresar al Load Balancer
    <img width="568" height="153" alt="Captura desde 2025-11-25 12-58-08" src="https://github.com/user-attachments/assets/5b792ead-0ca9-4cf7-a11c-4cccf82be36c" />

12. Puedes ver que el Load Balancer Health no presenta problemas  
    <img width="487" height="551" alt="Captura desde 2025-11-25 12-58-23" src="https://github.com/user-attachments/assets/e91bbd72-3e8a-44e9-9d1c-50c32ade1268" />

13. En la sección Load balancer information, se encuentra la IP pública del Load Balancer, copiar la IP
    <img width="716" height="601" alt="Captura desde 2025-11-25 13-00-17" src="https://github.com/user-attachments/assets/b6dde821-09bd-4057-bb22-13077fcb6b6f" />

14. Pegar la IP copiada en un navegador y refrescar varias veces, se puede observar como el Load balancer cambia de servidor web utilizando su IP pública<b>  
    <img width="566" height="147" alt="Captura desde 2025-11-25 13-00-35" src="https://github.com/user-attachments/assets/9280b6c0-8b93-4ae1-a928-401df0f7db3a" />  
    <img width="566" height="147" alt="Captura desde 2025-11-25 13-00-43" src="https://github.com/user-attachments/assets/46ebbd4f-0191-4de4-86d1-ce1e7edcf697" />

