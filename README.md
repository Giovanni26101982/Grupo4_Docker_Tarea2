# 📌 Grupo 4
## 📌 TAREA 02: Despliegue de infraestructura con docker compose.


---

## 🚀 Integrantes
| Nro. | Nombre | Link |
|------|---------|---------|
| 1 | Giovanni Xavier Baño Jaya | https://github.com/Giovanni26101982/Grupo4_Docker_Tarea2  |
| 2 | Portero Salas Onofre Lolislao | https://github.com/oportero/Grupo4_Docker_Tarea2  |
| 3 | Jara Pauta Cesar Paúl | https://github.com/PaulJara84/Grupo4_Docker_Tarea2  |
| 4 | Maldonado Flores Oscar Alexander | https://github.com/Oscar112248/Grupo4_Docker_Tarea2 |
| 5 | Balarezo Leon Ricardo Martin | https://github.com/TinchoXD/Grupo4_Docker_Tarea2  |

---

## 📖 Introducción

En la presente tarea se documenta el desarrollo y entrega del laboratorio grupal fastapi-app, cuyo objetivo es construir, publicar y evaluar la seguridad de una imagen Dockerfile multistage, y automatizar el análisis de vulnerabilidades mediante GitHub Actions con Docker Scout.

El trabajo contempla: 

- Con base en el laboratorio de fastapi-app, deberan subir la imagen que le corresponde a su grupo y las aplicaciones a su repositorio de github 
- Construir la imagen, subir a docker hub y realizar el análisis de vulnerabilidades con docker scout mediante un flujo de github actions
- Realizar el reporte de lo ejecutado en el archivo Readme.md del repositorio. Dentro del reporte debe constar la captura de pantalla que muestre la subida de la imagen en su repositorio de Docker hub y los resultados del análisis de vulnerabilidades con docker scout.
- Este trabajo se lo realizó de manera grupal y se encuentra publicado eb el repositorio git.

---

## 🚀 Características
- wordpress:6.5.2-php8.2-apache



---  

## 📂 Estructura
```bash
├── app/
|   └── main.py 
├── .gitignore
├── Dockerfile
├── dockerhub-scout.yml
├── README.md
└── requerimientos.txt

```
--- 

## 🛠 Desarrollo - Procedimiento

---
Para la presente práctica utilizamos versión de imagen wordpress: wordpress:6.5.2-php8.2-apache
--- 

1. **PASO 1: Creamos un archivo .env para colocar las credenciales de conexión tanto de base como del wordpress a través del comando:**

```bash
nano .env
```
<img width="424" height="440" alt="01" src="https://github.com/user-attachments/assets/837b518c-ab81-4b42-8333-1b34bb8164ce" />

Las ventajas de utilizar este archivo son:
-	No se tienen contraseñas expuestas en el docker-compose
-	Se puede cambiar fácilmente las contraseñas
-	Se pueden compartir sin exponer datos sensibles
-	Se pueden tener varios archivo .env para diferentes ambientes de trabajo

---

2. **PASO 2: Creamos un archivo docker-compose.yml, con el comando:**

```bash
nano docker-compose.yml
```
Realizar lo siguiente:

Servicio db
-	Crea un contenedor Maria db 10.6.4
-	Configura usuario y base de datos de manera aurompatica
-	Los datos se guardan en un volumen persistente db_data
Servicio Wordpress
-	Crea contenedor con wordpress
-	Se conecta automáticamente a la base de datos
-	Los archivos de wordpress persisten
-	Se expone wordpress en http://localhost:80

Volúmenes:
- db_data # volumen para datos de BD
- wp_data # volumen para archivos WP

<img width="698" height="641" alt="02" src="https://github.com/user-attachments/assets/8d056743-0238-4ae0-8ae4-be363b61eaea" />

---

3. **PASO 3: Verificamos los archivo a través de:**

```bash
tree –a
```
<img width="801" height="128" alt="03" src="https://github.com/user-attachments/assets/802bc5c7-1233-416f-b7d4-fd724f39c1b7" />

---

4. **PASO 4: Flujo de ejecución:**

Ejecutar:

```bash
docker-compose up -d
```

<img width="1012" height="308" alt="04" src="https://github.com/user-attachments/assets/e0cc6d15-8b03-4ac2-99c6-da70443f5182" />

---


## ✅ Conclusiones - Recomendaciones

1. El despliegue de la aplicación `FastAPI con Docker` se realizó exitosamente mediante la construcción de una imagen multistage, permitiendo una implementación más ligera y optimizada.
   
3. El análisis con Docker Scout evidenció que, aunque la aplicación funciona correctamente, existen vulnerabilidades conocidas en librerías del sistema base y dependencias de Python.

4. Para mitigar riesgos de seguridad se recomienda:
   - Actualizar la librería starlette a la versión 0.47.2 o superior, corrigiendo fallas de recursos sin límite.
   - Mantener actualizado el sistema base y explorar imágenes oficiales más recientes o variantes “slim” para reducir la superficie de ataque.
   - Establecer un flujo de integración continua (CI/CD) que incluya escaneo automático de vulnerabilidades en cada build de imagen.
  
1. **Cumplimiento de los entregables y trazabilidad**  
   Se construyó la imagen asociada al grupo, se publicó en Docker Hub y se registraron evidencias del proceso y del análisis de vulnerabilidades en el README.md.

1. **Impacto de la estrategia de construcción (single vs multistage)**  
   El uso de `multistage` (cuando aplicó) permitió `reducir tamaño de imagen` y `disminuir la superficie de ataque`, mejorando tiempos de pull y despliegue. En escenarios simples, single puede ser suficiente, pero para producción la strategia multietapa mostró claras ventajas de seguridad y eficiencia.

1. **Integración de seguridad en el ciclo de vida (Docker Scout + CI)**  
   La automatización con `GitHub Actions` y `Docker Scout` aportó `visibilidad continua`. Esta práctica refuerza la cultura `DevSecOps` al detectar riesgos antes del despliegue.

1. **Trabajo individual con enfoque profesional**  
   La organización para la ejecución del trabajo grupal, junto con la publicación en Docker Hub y auditoría automatizada, favoreció la `responsabilidad técnica` y la `calidad del entregable`, alineando el resultado con expectativas de acuerdo a lo solicitado.

1. La actividad no solo cumplió los requerimientos, sino que consolidó un `pipeline reproducible y seguro` para empaquetar aplicaciones con Docker, `publicarlas` y `evaluar su postura de seguridad` de forma integral, dejando como valor final un repositorio verificable y un informe con evidencias claras del proceso.

3. Finalmente, la práctica demuestra la importancia de no solo asegurar la funcionalidad del contenedor, sino también su seguridad y mantenimiento continuo en entornos de producción.

---
