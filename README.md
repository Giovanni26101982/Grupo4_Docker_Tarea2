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

Esta implementación representa un entorno completo de WordPress containerizado, diseñado bajo principios de DevOps e infraestructura como código.

Desplegar una instancia de WordPress 100% funcional y aislada que incluya:

- Servicio de aplicación: WordPress
- Base de datos: MariaDB para persistencia de datos
- Gestión de configuraciones: Variables de entorno centralizadas
- Persistencia: Volúmenes para datos críticos

Componentes Implementados
1. Orquestación con Docker Compose
   Coordinación automática de múltiples servicios interconectados, gestionando su ciclo de vida de manera unificada.
   
2. Aislamiento con Contenedores
   
   - WordPress: Servicio web independiente
   - MariaDB: Motor de base de datos aislado
   - Comunicación controlada: Red virtual dedicada

3. Persistencia con Volúmenes Docker
   - db_data:    # Base de datos (contenido, usuarios, configuraciones)
   - wp_data:    # Archivos WordPress (themes, plugins, uploads)

4. Seguridad con Variables de Entorno
   
   Implementación mediante archivo .env que permite:
   
   - Separación de configuración y código
   - Seguridad de credenciales sensibles
   - Portabilidad entre diferentes entornos
   - Versionado seguro (excluido de repositorios)

---

## 🚀 Características
- wordpress:6.5.2-php8.2-apache

---  

## 📂 Estructura
```bash
├── .env
├── docker-compose.yml
└── README.md

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

- Ejecutar:

```bash
docker compose up -d
```

<img width="1012" height="308" alt="04" src="https://github.com/user-attachments/assets/e0cc6d15-8b03-4ac2-99c6-da70443f5182" />

-	Descarga las imágenes si no existen

<img width="1182" height="712" alt="05" src="https://github.com/user-attachments/assets/1683cf28-75b3-4143-8d40-59cc885e8ce3" />

-	Crea red virtual para comunicación entre servicios

-	Crea volúmenes persistentes

-	Inicia contenedor de BD con configuración

-	Inicia WordPress que espera a que BD esté lista

-	WordPress se conecta automáticamente a la BD

-	Configuración automática

-	WordPress detecta que es primera instalación

-	Crea tablas en la base de datos

-	Muestra pantalla de instalación inicial


---

5. **PASO 5: Una vez levantados los servicios se muestra la siguiente ventana a través del comando:**

```bash
docker compose ps
```

<img width="1587" height="832" alt="06" src="https://github.com/user-attachments/assets/05b8a7ed-c09e-4b90-a9dc-4ca49694c35c" />

---


6. **PASO 6: Verificamos que hayan tomado los valores correctos del archivo .env a través del siguiente comando:**

```bash
docker compose config
```

<img width="1093" height="807" alt="07" src="https://github.com/user-attachments/assets/49a35919-e7fe-423e-b56a-3e3f724a1f8c" />

---

7. **PASO 7: Finalmente verificamos la pantalla de instalación**

<img width="999" height="630" alt="08" src="https://github.com/user-attachments/assets/0ad00844-8b52-47e0-936e-21b726640929" />

---


## ✅ Conclusiones - Recomendaciones

Implementación con versión de imagen de wordpress sin inconvenientes.

a)	Implementación:
   - Despliegue: Todos los servicios se inicializaron correctamente
   -	Arquitectura containerizada funcional: WordPress + MariaDB operando en contenedores aislados
   -	Comunicación inter-servicios efectiva: Conexión WordPress → BD establecida sin errores

b)	Ventajas
   -	Entorno 100% replicable
   -	Control exacto de versiones de software
   -	Servicios independientes pero conectados

c)	Configuración Optima
   -	Contraseñas y configuraciones aisladas en variables de entorno
   -	Servicios optimizados para su función específica
   -	Fácil actualización de versiones mediante cambio de tags

d)	Métricas
   -	Contenedores operativos: 2/2 servicios running
   -	WordPress accesible vía puerto 80
   -	Volúmenes creados y montados correctamente
   -	Comunicación interna servicio db → wordpress
   -	Servicios responden sin errores
e)	Buenas prácticas implementadas
   -	Uso de versiones específicas  Evita breaking changes
   -	Variables de entorno  Separación configuración/código
   -	Volúmenes nombrados  Persistencia garantizada

---
