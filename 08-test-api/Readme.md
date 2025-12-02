# 08 Pruebas de API

## Pruebas de llamada a Doguito API

Probando al API con métodos GET, POST, PUT y DELETE con POSTMAN

### GET

1. En POSTMAN, seleccionar el método GET, ingresar la IP de la instancia en el puerto 3000/clientes, seleccionar SEND, en Body, obtendremos la información de lo que se encuentra en nuestra base de datos
    <img width="1450" height="825" alt="Captura desde 2025-11-27 17-12-02" src="https://github.com/user-attachments/assets/90f67b7b-256d-4da8-8413-081cf1937a26" />

### POST

1. Cambiar método a POST, en Headers, en Key agregar Content-Type y en Values agregar application/json
     <img width="1472" height="339" alt="Captura desde 2025-11-27 17-13-31" src="https://github.com/user-attachments/assets/f292673a-9a21-42fb-8213-5228a2d52d48" />

2. En Body - raw, agregar un par llave/valor en formato json como en el ejemplo, click SEND
    <img width="1472" height="339" alt="Captura desde 2025-11-27 17-14-16" src="https://github.com/user-attachments/assets/267e5a7a-21ee-44ee-b233-13c5b1933de8" />

3. Podemos revisar la información del objeto que se acaba de crear, como ID o fecha de creación
    <img width="564" height="268" alt="Captura desde 2025-11-27 17-14-41" src="https://github.com/user-attachments/assets/bd1fac8f-380b-444e-adcb-f72f80676527" />

4. También revisar por web de que el nuevo objeto aparece listado
    <img width="560" height="509" alt="Captura desde 2025-11-27 17-14-52" src="https://github.com/user-attachments/assets/01a38844-d52a-4dcb-86ef-b8847607c4af" />


### PUT

1. Cambiar el método a PUT y en la dirección web agregar el ID del usuario que se va a modificar, cambiar nombre y mail, click SEND
    <img width="1438" height="456" alt="Captura desde 2025-11-27 17-17-44" src="https://github.com/user-attachments/assets/0ff4c5c7-b7f5-4311-8e18-3be33cb0de33" />

2. Verificar por web que el nombre y correo de usuario cambiaron, verificar que mantiene en el mismo ID
    <img width="570" height="493" alt="Captura desde 2025-11-27 17-18-09" src="https://github.com/user-attachments/assets/e41d04d9-c86b-49cd-ac3c-f4f2df02491b" />

### DELETE

1. Cambiar el método a DELETE y en la dirección web agregar el ID de usuario que se va a eliminar, click SEND
    <img width="1436" height="397" alt="Captura desde 2025-11-27 17-18-26" src="https://github.com/user-attachments/assets/ac048eeb-7d24-446d-a498-0a2e0049dace" />

2. Verificar por web que usuario perteneciente al ID fue eliminado
    <img width="645" height="392" alt="Captura desde 2025-11-27 17-18-39" src="https://github.com/user-attachments/assets/11c56897-55ef-4598-a151-dcde9a414e73" />
