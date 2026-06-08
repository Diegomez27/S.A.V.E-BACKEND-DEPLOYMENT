# S.A.V.E. Deployment

Configuración de despliegue automatizado para el sistema **S.A.V.E.** (Sistema de Acceso y Verificación Electrónica).

Este repositorio contiene únicamente los archivos necesarios para levantar el servidor backend y la base de datos utilizando Docker.

## Prerrequisitos

- **Docker** y **Docker Compose** instalados en el servidor o máquina local.
- Conexión a internet (para descargar las imágenes de Docker Hub).

## Instalación y Uso

### 1. Clonar este repositorio
O descargar los archivos `docker-compose.yaml` y `.env.example` en una carpeta vacía.

```bash
git clone <URL_DE_TU_NUEVO_REPO_DEPLOYMENT>
cd s.a.v.e-backend-deployment
```

### 2. Configurar Variables de Entorno

Renombra el archivo de ejemplo y configura tus contraseñas seguras.

Edita el archivo `.env` con tus credenciales:

```ini
# Configuración del Servidor
PORT=3001
NODE_ENV=production

# Base de Datos (Se creará automáticamente)
DB_HOST=savedb
DB_PORT=5434           # Puerto externo para tableplus
DB_USERNAME=postgres
DB_PASSWORD=TU_PASSWORD
DB_DATABASE=SaveDB

# Seguridad
# (mínimo 32 caracteres)
JWT_SECRET=escribe_aqui_una_clave_muy_segura_y_larga
JWT_EXPIRATION=24h
```

### 3. Iniciar el Sistema

Ejecuta el siguiente comando para descargar la imagen oficial y levantar los contenedores:

```bash
docker-compose up -d
```

El backend estará funcionando en http://localhost:3001.
El frontend estará en el http://localhost:80

## 🔄 Actualización

Para actualizar el proyecto a la última versión disponible:

```bash
# 1. Bajar la última versión de la imagen
docker-compose pull

# 2. Reiniciar los contenedores con la nueva imagen
docker-compose up -d
```

## Estructura del Despliegue

Este despliegue utiliza los siguientes servicios:

| Servicio | Imagen Docker | Descripción |
|----------|---------------|-------------|
| backend  | diegomez27/save-backend:latest | API NestJS compilada y optimizada. |
| frontend  | diegomez27/diegomez27/save-frontend:1.0.0 | App Ionic-Angular (web) compilada y optimizada. |
| db       | postgres:17.2 | Base de datos PostgreSQL. |

**bd:** Los datos de la base de datos se persisten en el volumen local `postgres_data`.

**Usuario:** admin
**Contraseña:** admin123

