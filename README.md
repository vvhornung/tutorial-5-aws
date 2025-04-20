![{8C43196F-C8E6-467B-A1E9-C9023E7F7E51}](https://github.com/user-attachments/assets/4c515885-1761-43dd-94eb-414dc98fc736)# tutorial-5-aws
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

8. Espera que el ícono se ponga verde y haz clic en **AWS**.
9. Busca y entra a **EC2**.
10. Click en **Launch Instance**.
11. Selecciona:
    - AMI: Amazon Linux 2023
    - Tipo: t2.micro
    - Key Pair: **Proceed without a key pair**
12. En **Network Settings**:
    - Habilita **HTTP** y **HTTPS**
13. Click en **Launch Instance**.
14. Ve a **Instances** y selecciona la que acabas de crear.
15. Haz click en **Connect** y luego en **Connect using EC2 Instance Connect**.

---

## B. Instalación de Docker y Base de Datos RDS

### En la consola EC2

```bash
sudo dnf update -y
sudo dnf install -y docker
sudo systemctl enable --now docker
docker --version
