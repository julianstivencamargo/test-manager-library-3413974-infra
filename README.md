# test-manager-library-3413974-infra — Infraestructura Global

Orquestación con Docker Compose para el proyecto **Manager Library** (Ficha ADSO 3413974 — T-20).

## Servicios Disponibles

| Servicio | Contenedor | Puerto Host | Descripción |
|---|---|---|---|
| **Base de Datos** | `manager-library-db` | `5432` | PostgreSQL 16 Alpine con base `manager_library` y esquema `library`. |
| **API Backend** | `manager-library-api` | `8000` | Laravel 11 / PHP 8.2 con Arquitectura Hexagonal y JWT. |
| **Frontend App** | `manager-library-app` | `3000` | SPA en React para gestión de catálogo, socios, préstamos y reportes. |
| **Sitio Público** | `manager-library-page` | `8080` | Sitio estático Nginx para presentación en la feria. |

---

## Instrucciones de Inicio Rápido (Un Solo Comando)

### 1. Levantar el ecosistema completo
Desde este repositorio (`test-manager-library-3413974-infra`):
```bash
docker compose up -d
```

### 2. Ejecutar las migraciones iniciales (T-02)
La base de datos arranca limpia; ejecute las migraciones en el contenedor:
```bash
docker compose exec api php artisan migrate
```

### 3. Aprovisionar los datos de demostración (T-21)
Puebla el catálogo con 42 libros en 5 categorías, 10 socios, préstamos activos y 3 préstamos vencidos:
```bash
docker compose exec api php artisan library:demo-seed
```

---

## Acceso a las Aplicaciones

- **Frontend React:** [http://localhost:3000](http://localhost:3000)
  - Admin: `admin` / `Admin1234*`
  - Bibliotecario: `ana` / `Librarian123*`
- **Backend API:** [http://localhost:8000/api/v1](http://localhost:8000/api/v1)
  - Health check: [http://localhost:8000/health](http://localhost:8000/health)
- **Sitio Público Estático:** [http://localhost:8080](http://localhost:8080)

---

## Ejecución de Pruebas Automatizadas
Desde `test-manager-library-3413974-api`:
```bash
docker compose run --rm test
```
Resultados de la suite: **62 pruebas aprobadas, 212 aserciones**.
