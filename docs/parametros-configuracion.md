# Parámetros de Configuración de Herramientas

## App móvil

| Parámetro | Valor |
|---|---|
| IDE | Android Studio Quail (3) |
| Lenguaje | Kotlin |
| UI | Jetpack Compose |
| Min SDK | 24 (Android 7.0) — cubre prácticamente todos los dispositivos activos |
| Target SDK | 36 (Android 16) — requerido por Google Play para apps nuevas desde agosto 2026 |
| Persistencia local | Room |
| Networking | Retrofit |
| Sincronización en background | WorkManager |

## Backend / API

| Parámetro | Valor |
|---|---|
| Framework | Laravel 13.x (requiere PHP 8.3+) |
| Base de datos | MySQL 8.4 |
| Autenticación | Laravel Sanctum |
| Entorno local | Docker (docker-compose con servicios `app`, `mysql`) |

**Justificación de Docker:** reproducibilidad entre máquinas (evita el "en mi máquina sí funciona"), y el mismo contenedor puede usarse en el pipeline de CI/CD sin reconfigurar nada — alinea con la estrategia de infraestructura como código del proyecto.

## Control de versiones

| Parámetro | Valor |
|---|---|
| Estrategia de branching | `main` (estable) / `develop` (integración) / `feature/*` (por funcionalidad) |
| Convención de commits | Conventional Commits (`feat:`, `fix:`, `chore:`, `docs:`, `test:`, `refactor:`) |
| Plataforma CI/CD | GitHub Actions |

## Plan de instalación e implementación

1. **App móvil:**
   - Clonar el repo, abrir la carpeta `app/` en Android Studio Quail 3
   - Dejar que Gradle sincronice dependencias (Room, Retrofit, WorkManager se agregan en `build.gradle.kts`)
   - Configurar la URL base de la API en un archivo de configuración local (no versionado)

2. **Backend / API:**
   - Clonar el repo, entrar a `api/`
   - Copiar `.env.example` a `.env` y ajustar credenciales de MySQL
   - Levantar con `docker-compose up -d`
   - Correr migraciones: `docker-compose exec app php artisan migrate`

3. **Primera ejecución local:**
   - Verificar que la API responde en `http://localhost:8000`
   - Apuntar la app móvil (en el emulador, `http://10.0.2.2:8000`) a esa URL
   - Probar el flujo de registro/login como primera prueba de humo end-to-end
