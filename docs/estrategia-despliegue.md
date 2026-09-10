# Estrategia de Despliegue

## App móvil

- El pipeline de CI/CD genera un **AAB/APK firmado** como artefacto en cada push a `main` (job de "release build" en GitHub Actions)
- Distribución mediante **Firebase App Distribution**: permite instalar builds de prueba en dispositivos reales sin pasar por Google Play, ideal para el alcance de este proyecto y para que el profesor/equipo pueda probar cada versión
- Publicación a Google Play queda fuera del alcance del curso, pero se documenta como paso futuro

## API backend

- **Proveedor:** Railway — soporta despliegue directo desde un `Dockerfile`/`docker-compose`, incluye MySQL como addon administrado, y tiene un flujo simple de conectar el repo de GitHub para despliegue automático en cada push a `main`
- **Variables de entorno:** gestionadas como *GitHub Actions Secrets* (para el pipeline) y como *Railway Environment Variables* (para producción) — nunca se versionan en el repo (ver `.gitignore`)
- **Migraciones automáticas:** sí — se ejecutan como parte del paso de despliegue (`php artisan migrate --force`) después de que el contenedor nuevo pasa su *health check*, para minimizar downtime

## Pipeline de despliegue (CD)

```
push a main
   → tests pasan (unit + integración + e2e)
   → build de imagen Docker (api) / AAB firmado (app)
   → deploy a staging (Railway staging environment)
   → smoke test contra staging
   → aprobación manual (protección de rama / environment de GitHub)
   → deploy a producción (Railway production environment)
   → migración de base de datos
```

## Monitoreo post-despliegue

- Logs de la API centralizados en Railway (salida estándar del contenedor)
- Health check endpoint (`/api/health`) verificado tras cada despliegue
- Métricas de crashes de la app vía Firebase Crashlytics
- El detalle operativo de monitoreo (alertas, dashboards, rollback) se desarrolla a fondo en la Actividad 3 ("Proceso de liberación y monitoreo")
