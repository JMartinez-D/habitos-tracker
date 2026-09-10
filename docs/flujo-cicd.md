# Flujo de Trabajo para Control de Versiones y CI/CD

## Estrategia de branching

```
main         ────●───────────●───────────●──────→  (producción, siempre desplegable)
                  \           \           \
develop      ──●───●──●───●────●──●───●────●──────→  (integración continua)
                \      \          \
feature/*    ────●──────●──────────●─────────────→  (una rama por funcionalidad)
```

- **`main`**: siempre en estado desplegable. Solo recibe merges desde `develop` vía Pull Request, después de que el pipeline completo pasa.
- **`develop`**: rama de integración. Los `feature/*` se mergean aquí primero.
- **`feature/*`**: una por funcionalidad (ej. `feature/crear-habito`, `feature/sync-offline`). Se crea desde `develop`, se mergea de vuelta a `develop` vía Pull Request.

## Convención de commits

Conventional Commits (definido en `parametros-configuracion.md`): `feat:`, `fix:`, `chore:`, `docs:`, `test:`, `refactor:`.

## Flujo de Pull Request

1. Se crea `feature/*` desde `develop`
2. Al hacer push, se abre PR hacia `develop`
3. GitHub Actions corre automáticamente: lint → unit tests → tests de integración
4. Requiere al menos 1 revisión (o autorevisión documentada, dado que es proyecto individual/pequeño equipo)
5. Merge a `develop` solo si el pipeline pasa en verde

## Pipeline de CI (Integración Continua)

Definido en [`.github/workflows/ci.yml`](../.github/workflows/ci.yml). Se dispara en cada push o PR a `main`/`develop`:

```
push / PR
   │
   ├─→ Job "api-tests"    → composer install → php artisan test
   │
   └─→ Job "app-tests"    → gradle build → testDebugUnitTest
```

Ambos jobs corren en paralelo. Si cualquiera falla, el PR queda bloqueado para merge (branch protection rule en GitHub).

## Pipeline de CD (Despliegue Continuo)

Se dispara solo en push a `main` (después de que `develop` se mergea ahí vía PR). Ver detalle completo en `estrategia-despliegue.md`:

```
merge a main
   → CI completo (tests)
   → build de artefactos (imagen Docker api / AAB app)
   → deploy a staging
   → smoke test
   → aprobación manual
   → deploy a producción
```

## Reglas de protección de rama (a configurar en GitHub)

- `main`: requiere PR, requiere que el CI pase, no permite push directo
- `develop`: requiere PR, requiere que el CI pase
