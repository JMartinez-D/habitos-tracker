# Hábitos Tracker

App móvil de seguimiento de hábitos con sincronización a backend.

## Descripción

El usuario define hábitos (ej. "tomar agua", "leer 20 min"), los marca como completados cada día y ve su racha (streak) de cumplimiento. La app funciona offline-first (Room como fuente de verdad local) y sincroniza con una API cuando hay conexión.

## Estructura del repositorio

```
habitos-tracker/
├── app/          # Aplicación móvil (Android Studio / Kotlin / Jetpack Compose)
├── api/          # Backend REST (Laravel + MySQL)
├── docs/         # Documentación del proyecto (planeación, pruebas, SDD, CI/CD)
└── .github/
    └── workflows/  # Pipelines de CI/CD (GitHub Actions)
```

## Componentes

| Componente | Stack | Estado |
|---|---|---|
| App móvil | Kotlin, Jetpack Compose, Room, Retrofit, WorkManager | Por iniciar |
| API backend | Laravel, MySQL, Sanctum | Por iniciar |

## Documentación

Ver [`docs/`](./docs) para:
- `parametros-configuracion.md` — parámetros de configuración de herramientas
- `plan-de-pruebas.md` — plan de pruebas
- `casos-de-prueba.md` — casos de prueba
- `flujo-cicd.md` — flujo de control de versiones y CI/CD
- `estrategia-despliegue.md` — estrategia de despliegue
- `sdd-proposal.md` — propuesta de Spec-Driven Development (comparación Kiro vs Spec Kit)
- `sdd-implementation.md` — guía de implementación de SDD

## Cómo levantar el proyecto

### App móvil
```
cd app
# abrir en Android Studio Quail 3
```

### API
```
cd api
composer install
cp .env.example .env
php artisan migrate
php artisan serve
```
