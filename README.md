# tutorial-5-aws
# Tutorial de Despliegue Django + Docker en AWS

Este tutorial te guiará paso a paso para desplegar una aplicación Django usando Docker en una instancia EC2 de AWS, conectada a una base de datos RDS.

---

## A. Creación de Instancia EC2 en AWS
1. y 2. ingreso a la plataforma
   
3. Dirígete al curso `116841` con el Nickname **TEIS-2025-1**.
![{8AFF31D6-6961-4BD5-90E2-E63891849EB6}](https://github.com/user-attachments/assets/8decbf23-c3e6-4c65-9e9d-cbec78ba89e3)

7. Presiona **Start Lab**.
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
