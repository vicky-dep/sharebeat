# ShareBeat

Aplicación web de radio colaborativa — Proyecto Intermodular de 2º DAW.

## Tecnologías

- Frontend: Angular 20 (previsto).
- Backend: Java 21 y Spring Boot 3.5.7.
- Base de datos: MySQL 8.4 LTS.
- Contenedores: Docker y Docker Compose.

## Requisitos previos

- Git.
- Docker Engine y Docker Compose (o Docker Desktop).
- Conexión a Internet para descargar las imágenes y dependencias.

No es necesario instalar Java, Maven ni MySQL localmente.

## Instalación y ejecución

### 1. Clonar el repositorio

Mediante SSH:

```bash
git clone git@github.com:vicky-dep/sharebeat.git
cd sharebeat
```

También se puede clonar mediante HTTPS:

```bash
git clone https://github.com/vicky-dep/sharebeat.git
cd sharebeat
```

### 2. Configurar las variables de entorno

```bash
cp .env.example .env
```

Editar `.env` y sustituir las contraseñas de ejemplo por contraseñas locales.

El archivo `.env` contiene credenciales y no debe subirse a GitHub.

La variable `DB_PORT` permite configurar el puerto de MySQL en el ordenador. Por defecto se utiliza el puerto `3307`, para evitar conflictos con otras instalaciones de MySQL.

Si ese puerto está ocupado, se puede cambiar en `.env` sin modificar `docker-compose.yml`.

### 3. Construir e iniciar los contenedores

```bash
docker compose up -d --build
```

Este comando inicia dos servicios:

- `database`: MySQL 8.4.
- `backend`: aplicación Spring Boot.

El backend espera a que MySQL supere su comprobación de disponibilidad antes de iniciarse.

### 4. Comprobar los contenedores

```bash
docker compose ps
```

Ambos servicios deben aparecer en ejecución.

### 5. Consultar los registros

```bash
docker compose logs -f
```

Para consultar únicamente el backend:

```bash
docker compose logs -f backend
```

### 6. Detener el entorno

```bash
docker compose down
```

Los datos de MySQL se conservan en un volumen Docker.

**Importante:** `docker compose down -v` elimina también el volumen y puede provocar la pérdida de los datos locales.

## Configuración

Las variables se definen en `.env.example` y se personalizan mediante `.env`.

| Variable | Descripción |
|---|---|
| `DB_ROOT_PASSWORD` | Contraseña del administrador de MySQL |
| `DB_NAME` | Nombre de la base de datos |
| `DB_USER` | Usuario de la aplicación |
| `DB_PASSWORD` | Contraseña del usuario de la aplicación |
| `DB_PORT` | Puerto local de MySQL (por defecto, 3307) |

## Puertos

| Servicio | Dirección local |
|---|---|
| Spring Boot | http://localhost:8080 |
| MySQL | 127.0.0.1:3307 (configurable mediante `DB_PORT`) |

Los puertos están publicados únicamente en localhost.

Dentro de Docker, Spring Boot se conecta a MySQL mediante el nombre del servicio `database` y el puerto interno `3306`.

Por tanto, modificar `DB_PORT` no afecta a la comunicación entre los contenedores.

## Estado del proyecto

Esta configuración corresponde al entorno inicial de desarrollo. Las funcionalidades de autenticación, salas colaborativas, reproducción musical y frontend Angular se incorporarán progresivamente.

## Equipo

- Alejandro López Jiménez
- Laura Sierra Arrabal
- María Victoria Depaoli