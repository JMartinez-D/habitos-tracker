# Estrategia de Despliegue

## App móvil

- Build de APK/AAB como artefacto del pipeline de CI/CD
- (completar: distribución — Firebase App Distribution, directo, etc.)

## API backend

- (completar: proveedor — Railway / Render / VPS)
- Variables de entorno gestionadas vía (completar)
- Migraciones automáticas en despliegue: (sí/no, completar)

## Pipeline de despliegue (CD)

```
main branch → tests pasan → build → deploy a staging → (aprobación manual) → deploy a producción
```

## Monitoreo post-despliegue

- (completar — se detalla más a fondo en Actividad 3: Proceso de liberación y monitoreo)
