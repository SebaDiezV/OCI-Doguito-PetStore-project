# Servicio Doguito API

## Configuración de API como servicio en servidor Linux

Se procede con la configuración de Doguito API para pasarlo a un servicio dentro del servidor Linux, con lo que no será necesario levantar el servicio NPM.

### Edición archivo service

1. Dentro de la carpeta doguito-api-es se encuentra el archivo doguito-api.service, editar archivo con editor favorito, para este caso, se utiliza vi

        ls
   <img width="800" height="53" alt="Captura desde 2025-11-27 16-13-57" src="https://github.com/user-attachments/assets/248a4c24-3f88-4cb3-a98f-8792a4564615" />

       vi doguito-api.service
   
    <img width="421" height="50" alt="Captura desde 2025-11-27 16-14-36" src="https://github.com/user-attachments/assets/39c4348b-7ca4-41a9-9d17-ae22f3010f97" />

2. Presionar la tecla "i" para poder editar el archivo, se puede ver en la parte baja que se encuentra en modo INSERT
    <img width="127" height="31" alt="Captura desde 2025-11-27 16-15-13" src="https://github.com/user-attachments/assets/4b00c74e-e108-427d-9da3-4efa4915f42d" />

3. En el apartado [Service], agregar la información de DB_PASSWORD con la contraseña de la base de datos Auronomous, reemplazando los símbolos de interrogación, también reemplazar los símbolos de interrogación en CONNECT_STRING con la información de string correspondiente  
    <img width="262" height="78" alt="Captura desde 2025-11-27 16-15-50" src="https://github.com/user-attachments/assets/a26fc04c-6e9e-4a20-ba2a-fecfd4438fb1" />

4. Una vez finalizada la edición, presionar la tecla ESC, luego presionar ":wq" para guardar los cambios y salir del editor vi  
    <img width="76" height="44" alt="Captura desde 2025-11-27 16-19-41" src="https://github.com/user-attachments/assets/f9f6384a-bbff-43ef-b548-7c44beafe245" />

5. Verificar los cambios al archivo utilizando el comando cat
    <img width="642" height="316" alt="Captura desde 2025-11-27 16-20-16" src="https://github.com/user-attachments/assets/b95db6bb-2c16-4cd4-8c81-f5564ad64ff6" />

### Activar servicio doguito

1. Copiar archivo doguito-api.service hacia la carpeta /lib/systemd/system y luego ingresar a la misma carpeta

        sudo cp doguito-api.service /lib/systemd/system
     <img width="568" height="29" alt="Captura desde 2025-11-27 16-22-37" src="https://github.com/user-attachments/assets/3e210146-3d7b-4aa9-a82d-53bde22607bc" />

        cd /lib/systemd/system
     <img width="399" height="42" alt="Captura desde 2025-11-27 17-02-47" src="https://github.com/user-attachments/assets/f31efe29-8363-47cf-a90a-5288956c2a40" />  <b>

    Puedes utilizar ls para verificar que la copia fue correcta utilizando el comando ls  

3. Recargar daemon para que el sistema integre el nuevo archivo agregado

        sudo systemctl daemon-reload
     <img width="436" height="36" alt="Captura desde 2025-11-27 17-04-44" src="https://github.com/user-attachments/assets/ce1a604f-8238-4d05-87dd-7ccb58463004" />

4. Verificar el estado del servicio doguito, por defecto esta inactivo, iniciamos el servicio y verificamos el estado nuevamente

       sudo systemctl status doguito-api.service
     <img width="705" height="88" alt="Captura desde 2025-11-27 17-05-37" src="https://github.com/user-attachments/assets/0fb7d368-0cec-409a-a814-ffad5e4632fd" />

       sudo systemctl start doguito-api.service
     <img width="715" height="310" alt="Captura desde 2025-11-27 17-06-32" src="https://github.com/user-attachments/assets/9e66bf3a-3237-443a-8bb0-b5febd7ed1ed" />

     
5. Verificar el funcionamiento de la API ingresando por web a la IP de la instancia en el puerto 3000 para ver la información de la base de datos  
    <img width="711" height="383" alt="Captura desde 2025-11-27 17-07-08" src="https://github.com/user-attachments/assets/eef80f1b-dc6c-400f-8f4f-90fbed35b48b" />

6. De regreso en Cloud Shell, detener la ejecución del comando con ctrl+c, ejecutar el comando para dejar el servicio permanente mente habilitado

        sudo systemctl enable doguito-api.service
     <img width="906" height="58" alt="Captura desde 2025-11-27 17-08-55" src="https://github.com/user-attachments/assets/71c4171d-b5c9-4ea5-948d-877953d9c890" />







