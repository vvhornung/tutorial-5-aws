
# Tutorial de Despliegue Django + Docker en AWS

Este tutorial te guiará paso a paso para desplegar una aplicación Django usando Docker en una instancia EC2 de AWS, conectada a una base de datos RDS.

---

## A. Creación de Instancia EC2 en AWS
1,2. ingreso a la plataforma
   
3. Dirígete al curso `116841` con el Nickname **TEIS-2025-1**.
   
![{3B667946-F782-4CE3-9FC4-4DB70F448716}](https://github.com/user-attachments/assets/19211668-ae69-41d0-b732-67ae8ac121a7)

5. ingreso a AWS learner lab
6. Presiona **Start Lab**.
![{8C43196F-C8E6-467B-A1E9-C9023E7F7E51}](https://github.com/user-attachments/assets/942dcc84-3204-4a8a-825d-e17d8eac5613)

7. Espera que el ícono se ponga verde y haz clic en **AWS**.
![{313944EA-F39A-455D-8EFE-935ABA8B59AB}](https://github.com/user-attachments/assets/7496796b-196b-4a39-a2cf-bff675326488)

9. Busca y entra a **EC2**.
![{A4B9485B-4348-448F-AA94-AECD856271D3}](https://github.com/user-attachments/assets/2ad25286-d07a-43a9-82a0-be70a8324164)

10. Click en **Launch Instance**.
![{6727BC6D-E009-42D1-9CCE-CBCCB49BA418}](https://github.com/user-attachments/assets/c4da03f7-f61a-461c-93dc-aabc7971d04a)

11. Selecciona:
    - AMI: Amazon Linux 2023
    - ![{B9B36126-4DA4-4DAE-B0C2-6FC96E0E4A07}](https://github.com/user-attachments/assets/e25e2af7-a4e9-473b-90a8-1a78433fe276)

    - Tipo: t2.micro and Key Pair: **Proceed without a key pair**
    - ![{AA235496-F7E8-4195-A0BD-A6D3BEBD4AF7}](https://github.com/user-attachments/assets/979d7632-4e74-49be-b3ef-b6e262cd2353)
      
    - En Network Settings, active Allow HTTPS y Allow HTTP
    - ![{E459E20C-77A2-4BF2-B060-AD3FE2CAE7FD}](https://github.com/user-attachments/assets/ff8e6eea-4252-4e45-8c4e-2c06e014d2a8)

   
12. Click en **Launch Instance**.
![{59A009DE-89D3-4C2A-8CC2-7F090FC8AED9}](https://github.com/user-attachments/assets/2d58739f-4fe5-491a-a0ba-079c9963b412)

13. Ve a **Instances** y selecciona la que acabas de crear.
![{8440AC0F-C0CE-4C17-889D-E9C99C3136F4}](https://github.com/user-attachments/assets/9a4d2166-766e-464a-b0c0-ce4af6cab044)

15. Haz click en **Connect** y luego en **Connect using EC2 Instance Connect**.
![{079262AD-5C7A-4ABB-87E3-0775EA6B2203}](https://github.com/user-attachments/assets/da52c4fc-5111-44e9-8941-4016d6421830)

---

## B. Instalación de Docker y Base de Datos RDS

### En la consola EC2

paso 1:Corra el siguiente comando desde la consola de AWS (estamos en una maquina
Amazon Linux) para actualizar el sistema, instalar y activar Docker, y verificar su instalación. 

sudo dnf update -y
![{47F6997D-BEC4-4732-A2D5-9875EDEF66CA}](https://github.com/user-attachments/assets/38b2eae5-8e84-4454-869a-86a3803ea848)

sudo dnf install -y docker
![{829C16E3-A369-4D70-9120-B31DDA044871}](https://github.com/user-attachments/assets/57923511-d582-4cfb-9021-5f2b9981e91e)

sudo systemctl enable --now docker
![{FFD5CECE-E9DF-497C-A8ED-09753C7D0CE1}](https://github.com/user-attachments/assets/2bf9b3b4-cebd-4cfa-ba3b-d8b98e8f1ae4)

docker --version
![{D99EECFD-F03B-445E-BC06-D366AC9FF624}](https://github.com/user-attachments/assets/c1590b77-a178-4fb8-a1e1-61b6706282fa)


Paso 2: Vuelva al navegador, al sitio de AWS, y busque “Aurora and RDS”.

Paso 3: Busque y dé clic en la opción “Create database”.

Paso 4: Seleccione “MySQL”, verifique que tiene activa la versión “MySQL 8.0”, y seleccione “Free tier”.

Paso 5: Complete el formulario con los siguientes datos:  
- DB instance identifier: `teis20251`  
- Master username: `admin`  
- Master password: `<TuContraseñaSegura>`

Paso 6: Haga clic en el botón **Create database**.

Paso 7: Espere unos minutos a que la base de datos esté en estado “Available”.

Paso 8: Haga clic sobre la base de datos creada y copie el valor de **Endpoint**.

Paso 9: En la sección **Connectivity & security**, haga clic en el enlace del **VPC security group** (nombre como `sg-...`).

Paso 10: En la página del grupo de seguridad, haga clic en **Edit inbound rules**.

Paso 11: Agregue una nueva regla con:  
- Type: `MySQL/Aurora`  
- Port: `3306`  
- Source: `My IP` (o la IP de su instancia EC2 si prefiere más seguridad)

Paso 12: Vuelva a la terminal EC2. Instale el cliente de MySQL.  
`sudo dnf install -y mariadb105`

Paso 13: Conéctese a la base de datos usando el endpoint copiado.  
`mysql -h <ENDPOINT> -P 3306 -u admin -p`

Paso 14: Cuando lo solicite, introduzca la contraseña que configuró para el usuario admin.

Paso 15: Ya dentro de la consola de MySQL, ejecute el siguiente comando:  
`CREATE DATABASE djangodocker;`

Paso 16: Escriba `exit` para salir.

---

## C. Descargar proyecto Django y correr Docker

Paso 1: Verifique que Docker funciona correctamente con el siguiente comando.  
`sudo docker container run hello-world`

Paso 2: Instale Git en la instancia EC2.  
`sudo dnf install git -y`

Paso 3: Clone el repositorio de ejemplo desde GitHub.  
`git clone https://github.com/Nram94/djangoDocker.git`

Paso 4: Ingrese a la carpeta del proyecto.  
`cd djangoDocker`

Paso 5: Copie el archivo `.env.example` a `.env`.  
`cp .env.example .env`

Paso 6: Edite el archivo `.env` para incluir los datos de la base de datos RDS.  
`nano .env`

Paso 7: Modifique las siguientes variables:  
- `DB_HOST=<ENDPOINT_DE_RDS>`  
- `DB_DATABASE=djangodocker`  
- `DB_USERNAME=admin`  
- `DB_PASSWORD=<TuContraseñaSegura>`

Paso 8: Guarde y cierre el editor (`Ctrl + X`, luego `Y`, luego `Enter`).

Paso 9: Construya la imagen Docker.  
`sudo docker image build -t django-app .`

Paso 10: Ejecute el contenedor.  
`sudo docker container run -d --name django-docker -p 80:80 django-app`

Paso 11: Desde el navegador, visite la IP pública de su instancia EC2 con la ruta `/public/`.  
Ejemplo: `http://<IP_PÚBLICA_EC2>/public/`

---

