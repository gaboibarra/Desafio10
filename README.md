# 🏗️ Desafío 10 - Dockerizando una Aplicación NestJS con MongoDB

**📌 Descripción**

Este proyecto consiste en la creación de un entorno Dockerizado para una aplicación NestJS que utiliza MongoDB como base de datos. Se proporciona un Dockerfile y un docker-compose.yaml para facilitar la instalación y ejecución en cualquier entorno local.

**⚙️ Requisitos Previos**

Antes de instalar y ejecutar este proyecto, asegúrate de cumplir con los siguientes requisitos:

## 📌 Requisitos del Sistema

✅ Sistema Operativo: Windows 10 (versión 1903 o superior) o Windows 11

✅ Virtualización habilitada: Hyper-V y WSL 2 (Subsistema de Windows para Linux)

✅ CPU: Compatible con virtualización (Intel VT-x o AMD-V)

✅ RAM: Al menos 4 GB de memoria

## 🐳 Instalación de Docker en Windows
1️⃣ Verificar los Requisitos
Antes de instalar Docker, asegúrate de que la virtualización esté habilitada en tu equipo.

2️⃣ Descargar Docker Desktop
👉 [Docker Desktop para Windows](https://www.docker.com/products/docker-desktop/)

3️⃣ Instalar Docker Desktop
- Abre el instalador (Docker Desktop Installer.exe).
- Acepta los permisos de administrador si se solicitan. **(Opcional pero recomendado):** Marca la opción "Use WSL 2 instead of Hyper-V".
- Haz clic en "Install" y espera a que finalice la instalación.
- Reinicia tu PC si se solicita.

4️⃣ Verificar la Instalación
Abre CMD o PowerShell y ejecuta:
```bash
docker --version
```
Si la salida es algo como esto:
```bash
Docker version 24.x.x, build xxxxxxx
```
Significa que Docker está instalado correctamente. ✅

También se puede probar ejecutando un contenedor de prueba:
```bash
docker run hello-world
```
Al ver este mensaje de Bienvenida quiere decir que Docker está funcionando correctamente. 🎉

![image](https://github.com/user-attachments/assets/4538809f-e88b-48c5-b0a3-8e2cbd4d7bc7)

# 🚀 Pasos para Ejecutar la Aplicación

1️⃣ Clonar el Repositorio
```bash
git clone https://github.com/edgaregonzalez/devops-bootcamp.git
cd devops-bootcamp/Desafios/Fase3/educacionit-app
```



