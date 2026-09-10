# Plan de Pruebas

## Alcance

| Nivel | Qué se prueba | Herramienta |
|---|---|---|
| Unit | Lógica de rachas (cálculo de streak, reinicio al saltar un día), validaciones de formularios | JUnit (app), PHPUnit (api) |
| Integración | Sync Room ↔ API, persistencia offline, endpoints de la API contra MySQL | JUnit + MockWebServer (app), PHPUnit Feature Tests (api) |
| E2E | Flujos completos de usuario (registro, crear hábito, marcar completado, ver racha) | Appium |

**Nota sobre la herramienta e2e:** se usa Appium en lugar de Selenium/Katalon directo porque el caso de estudio es una app móvil nativa (no web). Appium implementa el mismo protocolo WebDriver que Selenium, por lo que cumple el mismo enfoque de automatización e2e que piden los requerimientos, adaptado a Android.

## Entornos

| Entorno | Descripción |
|---|---|
| Local | Docker Compose (api + MySQL) + emulador Android en Android Studio |
| CI (GitHub Actions) | Contenedor efímero para la API (mismo `docker-compose`), emulador Android headless (`reactivecircus/android-emulator-runner` action) para tests instrumentados |
| Staging | Instancia de la API desplegada (ver `estrategia-despliegue.md`) usada para correr el suite de Appium contra un build de release antes de liberar |

## Ejecución del test suite

**Backend (Laravel):**
```
docker-compose exec app php artisan test
```

**App — unit tests:**
```
cd app
./gradlew testDebugUnitTest
```

**App — tests instrumentados / e2e (Appium):**
```
cd app
./gradlew connectedDebugAndroidTest
```

Estos comandos son los que se integran directamente en el pipeline de CI/CD (ver `.github/workflows/ci.yml`).

## Criterios de aceptación

- El suite de unit tests cubre al menos la lógica de cálculo de rachas (casos: día consecutivo, día saltado, mismo día repetido)
- Todos los tests unitarios y de integración pasan antes de hacer merge a `develop` o `main` (bloqueo vía GitHub Actions)
- Los casos de prueba e2e definidos en `casos-de-prueba.md` pasan contra un build de staging antes de cualquier release
- Cobertura mínima objetivo: 70% en la lógica de negocio crítica (rachas, sincronización)
