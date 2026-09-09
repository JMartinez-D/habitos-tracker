# Plan de Pruebas

## Alcance

| Nivel | Qué se prueba | Herramienta |
|---|---|---|
| Unit | Lógica de rachas, validaciones de formularios | JUnit (app), PHPUnit (api) |
| Integración | Sync Room ↔ API, persistencia | JUnit + MockWebServer, PHPUnit |
| E2E | Flujos completos de usuario | Espresso / Appium (app), Playwright (panel admin si aplica) |

## Entornos

- (completar: local, staging)

## Ejecución del test suite

(completar tras configurar el pipeline — comandos exactos para correr los tests)

## Criterios de aceptación

- (completar)
