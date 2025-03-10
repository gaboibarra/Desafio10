# 🏗️ Desafío 10 - Dockerizando una Aplicación NestJS con MongoDB

## **📌 Descripción**

Este proyecto consiste en la creación de un entorno Dockerizado para una aplicación NestJS que utiliza MongoDB como base de datos. Se proporciona un Dockerfile y un docker-compose.yaml para facilitar la instalación y ejecución en cualquier entorno local.

## **⚙️ Requisitos Previos**

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

![image](https://github.com/user-attachments/assets/e1fd2283-3c68-47ac-b259-1a95bd2be889)

# 🚀 Pasos para Ejecutar la Aplicación

1️⃣ Clonar el Repositorio
```bash
git clone https://github.com/edgaregonzalez/devops-bootcamp.git
cd devops-bootcamp/Desafios/Fase3/educacionit-app
```
2️⃣ Validar los Archivos en el Proyecto

```bash
dir  # (Windows)
```
![image](https://github.com/user-attachments/assets/ec3a8af7-ccce-47c6-ae1c-32d5ee0a0074)

3️⃣ Construir y Levantar los Contenedores
```bash
docker-compose up --build -d
```
![image](https://github.com/user-attachments/assets/78de46ad-358c-4963-957c-7b8b7c8d2a40)

4️⃣ Verificar que los Contenedores Están Corriendo
```bash
docker ps
```
![image](https://github.com/user-attachments/assets/37990c04-9fa6-4a2f-bf8d-c38bd6cde0ab)

5️⃣ Acceder a la Aplicación

Abrir el navegador y accede a: 👉 http://localhost:3000

Si todo funciona bien, deberías ver la API en funcionamiento. 🚀

![image](https://github.com/user-attachments/assets/a3550e4d-3138-40af-965d-aad1ba6186a5)

# 🛠️ Probar MongoDB (Opcional, pero Recomendado)

1️⃣ Conectarse a MongoDB dentro del Contenedor
Ejecutar el siguiente comando:

```bash
docker exec -it mongo mongosh -u root -p rootpassword --authenticationDatabase admin
```
Si la conexión es exitosa, se vera un mensaje como este: 

![image](https://github.com/user-attachments/assets/f51b9955-e52a-4829-a798-b7317791e2e0)

2️⃣ Verificar que MongoDB Está Corriendo
Dentro de mongosh, ejecuta:

```bash
show dbs
```
![image](https://github.com/user-attachments/assets/9940d628-fc97-4429-9562-5fc457200fe5)

**Dado que MongoDB no muestra bases de datos vacías hay que asegurarse de que la aplicación realmente está insertando datos.**
3️⃣ Insertar un Documento de Prueba
Si la base de datos aún no tiene datos, agregarlos manualmente:
```bash
use educacionit
db.usuarios.insertOne({ name: "Gabriel Ibarra", email: "gabar@example.com" })
```
![image](https://github.com/user-attachments/assets/7f2817ed-7d21-4b7e-aedc-d2e1f2b997ff)

Verificar que el documento fue insertado:

```bash
db.usuarios.find().pretty()
```
![image](https://github.com/user-attachments/assets/bb2c869f-fb20-40f0-9e47-1ee910635bfc)

## 🛠️ **Solución de Problemas**

Si se experimenta problemas al ejecutar la aplicación, revisar la siguiente tabla con soluciones comunes:

| 🚨 Problema | 🔍 Posible Causa | 🛠️ Solución |
|------------|-----------------|-------------|
| `docker ps` no muestra contenedores | Docker no está corriendo | Abrir **Docker Desktop** y verificar que esté activo |
| No se puede acceder a `http://localhost:3000` | El contenedor `nestjs_app` no está corriendo | Ejecutar `docker-compose up --build -d` nuevamente |
| `docker logs nestjs_app` muestra errores de módulos faltantes | No se instalaron las dependencias correctamente | Ejecutar `docker exec -it nestjs_app sh` y luego `npm install` dentro del contenedor |
| **MongoDB no está disponible** (`Connection refused`) | MongoDB no inició correctamente | Verificar los logs con `docker logs mongo_db` y asegurarse de que el contenedor esté corriendo con `docker ps` |
| **NestJS no puede conectarse a MongoDB** (`ECONNREFUSED`) | La URI de conexión es incorrecta o MongoDB no está listo | Asegurarse de que `MONGO_URI=mongodb://mongo:27017/educacionit` está correctamente configurada en `docker-compose.yaml` |
| **Error `Cannot find module '@nestjs/core'`** | NestJS no tiene las dependencias instaladas | Acceder al contenedor y ejecutar `npm install` y luego `npm run build` |
| **El contenedor de NestJS se queda en `Restarting`** | Error en la ejecución del servidor | Ejecutar `docker logs nestjs_app` para obtener más información |

Si el problema persiste, revisar los logs de la aplicación con:

```sh
docker logs nestjs_app
```
Y los logs de MongoDB con:
```sh
docker logs mongo_db
```
Luego, intentar reiniciar los servicios:
```sh
docker-compose down
docker-compose up --build -d
```
## 🏆 Conclusión
Este proyecto permite ejecutar una aplicación NestJS con MongoDB de manera rápida y eficiente usando Docker. Gracias a docker-compose, todos los desarrolladores pueden replicar fácilmente el entorno sin problemas de configuración. 🚀

## 📄 Créditos
Desarrollado como parte del Desafío 10 del bootcamp de DevOps. 🎓

## 🛠 **Tecnologías Utilizadas**

Este proyecto utiliza las siguientes tecnologías:

### 📦 **Backend**
- **[NestJS](https://nestjs.com/)** - Framework progresivo de Node.js para construir aplicaciones eficientes y escalables.
- **[TypeScript](https://www.typescriptlang.org/)** - Lenguaje tipado que mejora la robustez del código en JavaScript.

### 🗄️ **Base de Datos**
- **[MongoDB](https://www.mongodb.com/)** - Base de datos NoSQL orientada a documentos.
- **[Mongoose](https://mongoosejs.com/)** - ODM (Object Data Modeling) para manejar MongoDB en NestJS.

### 🐳 **Contenedores y Orquestación**
- **[Docker](https://www.docker.com/)** - Plataforma para contenedores que permite la portabilidad del proyecto.
- **[Docker Compose](https://docs.docker.com/compose/)** - Orquestador para levantar múltiples servicios en un solo comando.

### 🔧 **Herramientas de Desarrollo**
- **[Node.js](https://nodejs.org/)** - Entorno de ejecución de JavaScript en el servidor.
- **[NPM](https://www.npmjs.com/)** - Administrador de paquetes para JavaScript.
- **[Git](https://git-scm.com/)** - Sistema de control de versiones.
- **[Visual Studio Code](https://code.visualstudio.com/)** - Editor de código recomendado para trabajar con este proyecto.

---
