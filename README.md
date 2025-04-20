
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

```bash
sudo dnf update -y
sudo dnf install -y docker
sudo systemctl enable --now docker
docker --version
