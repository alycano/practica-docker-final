# Laboratorio: Contenerización de Aplicación End-to-End - TesloShop

Este repositorio contiene la solución completa para la contenerización de una plataforma de e-commerce utilizando una arquitectura de microservicios. Se ha implementado el despliegue de una base de datos relacional, una API REST y una aplicación cliente, todos orquestados mediante Docker Compose.

## 1. Arquitectura del Proyecto

La aplicación se basa en tres capas fundamentales que operan de forma aislada pero interconectada:

* **Frontend (Angular 19):** Interfaz de usuario servida mediante un servidor web Nginx optimizado.
* **Backend (NestJS):** API lógica que gestiona las reglas de negocio y la comunicación con la base de datos.
* **Database (PostgreSQL 14.3):** Motor de base de datos relacional para la persistencia de la información.

## 2. Proceso de Implementación

El desarrollo se llevó a cabo siguiendo estos pasos clave:

1.  **Clonación y Configuración:** Se obtuvo el código fuente y se configuraron las variables de entorno (`.env`) para definir credenciales de base de datos y puertos de publicación.
2.  **Optimización de Imágenes:** Se implementaron **Multi-stage builds** en los Dockerfiles para asegurar que las imágenes de producción sean ligeras, conteniendo únicamente los archivos transpilados de JavaScript y las dependencias necesarias.
3.  **Persistencia de Datos:** Se definieron volúmenes de Docker para evitar la pérdida de información en la base de datos tras el reinicio de los contenedores.
4.  **Mapeo de Archivos Estáticos:** Se configuró un volumen de tipo *bind mount* para permitir que el backend acceda a las imágenes físicas de los productos desde el sistema de archivos del host.

## 3. Guía de Ejecución Rápida

Siga este orden para poner en marcha la solución:

### A. Preparación
Asegúrese de que el motor de Docker (Docker Desktop) esté iniciado y operativo en su sistema.

### B. Despliegue de Servicios
Desde la terminal en la raíz del proyecto, ejecute:
```bash
docker compose up --build -d
C. Población de Datos (Seed)
Para cargar el catálogo de productos y usuarios de prueba, acceda a:
http://localhost:3000/api/seed

D. Acceso a los Servicios
Tienda Web: http://localhost:8080

Documentación Swagger (API): http://localhost:3000/api

4. Tecnologías y Prácticas Aplicadas
Docker Compose: Orquestación de contenedores y redes virtuales.

Nginx Proxy: Configurado para servir el frontend y gestionar las rutas.

Healthchecks: Implementados en la base de datos para garantizar que el backend solo intente conectarse cuando el servicio esté listo.

Aislamiento: Cada servicio corre en su propia red interna, exponiendo solo los puertos necesarios al exterior.

Autor: Aly Santiago Cano
Proyecto: Análisis y Desarrollo de Software - SENA


