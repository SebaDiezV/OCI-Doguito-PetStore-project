# 02 - Configuración de Redes

## Configuración de VCN y subredes para la creación de Doguito App

Se realiza la configuración de VCN y subredes publica y privada dentro de compartimento de Desarrollo con el usuario **doguito-admin**

## Configuración de VCN

1. En el menú desplegable, seleccionar Networking y luego Virtual Cloud Networks
    <img width="635" height="500" alt="Captura desde 2025-11-20 12-51-13" src="https://github.com/user-attachments/assets/ba3a8a1c-e344-4ab8-89ac-094628447488" /> <b>

2. Seleccionar el menú desplegable Actions y seleccionar Start VCN Wizard
    <img width="649" height="366" alt="Captura desde 2025-11-20 12-52-17" src="https://github.com/user-attachments/assets/7fc7117a-3a66-4eee-81bb-fe38ce8f6a9c" /> <b>

3. Seleccionar Create VCN with Internet Connectivity, esto creará una VCN con una subred pública que puede ser alcanzada desde internet, también crea una subred privada
que se conecta a internet a través de un NAT Gateway y también privadamente conecta con los servicios de Oracle Services Network
    <img width="1421" height="844" alt="Captura desde 2025-11-20 12-53-35" src="https://github.com/user-attachments/assets/631198e3-f799-40c0-b7f2-fb35ab4a6653" /> <b>

4. Agregar nombre para la VCN y seleccionar el compartimento Desarrollo
    <img width="897" height="441" alt="Captura desde 2025-11-25 15-59-26" src="https://github.com/user-attachments/assets/c9c783a3-c6fe-4163-bc74-561b046d728b" /> <b>

5. Para este ejercicio, dejaremos por defecto los valores de CIDR de la VCN y las subredes pública y privada, seleccionar Next
    <img width="1764" height="877" alt="Captura desde 2025-11-20 12-55-48" src="https://github.com/user-attachments/assets/787e78f6-a133-4085-8feb-bf9b6d4d34f9" /> <b>

6. Seleccionar Create
    <img width="1764" height="877" alt="Captura desde 2025-11-20 12-57-32" src="https://github.com/user-attachments/assets/209359f9-3e7f-430e-ac86-1fe500865986" /> <b>

7. Una vez terminada la configuración, seleccionar View VCN
    <img width="1764" height="877" alt="Captura desde 2025-11-20 12-58-29" src="https://github.com/user-attachments/assets/fae4a417-6a59-48bf-9ed0-6de95dd34aa7" />
    <img width="1764" height="877" alt="Captura desde 2025-11-20 12-59-11" src="https://github.com/user-attachments/assets/bb77722f-3969-4f17-ae45-376fd79e8331" /> <b>

Con esto concluye la configuración básica de la red para Doguito Petshop, otros cambios, como apertura de puertos, se verán en otras partes del para evitar confusiones.

