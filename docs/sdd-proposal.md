# Propuesta de Spec-Driven Development (SDD)

## Contexto

Este proyecto arranca desde cero, sin código previo. Esto lo hace un punto de partida ideal para adoptar Spec-Driven Development desde el día uno, en lugar de aplicarlo por ingeniería inversa sobre un sistema existente.

## Diagnóstico del estado actual

| Aspecto | Estado |
|---|---|
| Código existente | Ninguno |
| Especificaciones existentes | Ninguna |
| Repositorio | Configurado (estructura `app/`, `api/`, `docs/`, CI base) |
| Proceso de desarrollo formal | No definido antes de este documento |
| Herramientas de IA para SDD evaluadas | Kiro (AWS), GitHub Spec Kit |

**Qué falta para SDD formal:** una fuente única de verdad ("constitución" del proyecto), specs por funcionalidad antes de implementar, un flujo repetible de spec → plan → tareas → código, y un mecanismo para mantener las specs vivas conforme el proyecto evoluciona.

## Comparación: Kiro vs Spec Kit

| Criterio | Kiro (AWS) | GitHub Spec Kit |
|---|---|---|
| Naturaleza | IDE completo (fork de VS Code / Code OSS) | CLI + templates que se integran a tu IDE/agente actual |
| Motor de IA | Claude vía Amazon Bedrock (integrado, no intercambiable) | Agnóstico — funciona con GitHub Copilot, Claude Code, Gemini CLI, Cursor, etc. |
| Costo | Freemium con créditos: gratis (50 créditos/mes), Pro $20/mes (1,000 créditos); una funcionalidad completa con specs consume 15–25 créditos | Gratuito y open source |
| Dependencia de infraestructura | Ventaja real solo si ya usas AWS/Bedrock | Ninguna — funciona con cualquier stack |
| Flujo de trabajo | Requiere, diseño, tareas generados dentro del IDE; ejecución de agentes en paralelo; hooks y "steering files" | Comandos explícitos: `/specify` → `/plan` → `/tasks` → `/analyze` → implementación |
| Curva de aprendizaje | Alta — implica adoptar un IDE nuevo completo | Baja — se instala con un CLI (`uv`) sobre las herramientas que ya usas |
| Madurez | Producto v1.x, GA desde 2026, ecosistema de hooks/steering aún creciendo | Herramienta con comunidad activa, alcanzó la versión 1.0 en 2026 |
| Adecuación a este proyecto | Baja: no hay infraestructura AWS en el proyecto, y el modelo de créditos no es viable para un proyecto académico sin presupuesto | Alta: se integra directo al flujo de GitHub + Claude que ya se está usando, sin costo ni cambio de herramientas |

## Herramienta elegida y justificación

Se elige **GitHub Spec Kit**. Las razones:

1. **Costo cero** — es un requisito práctico para un proyecto académico sin presupuesto asignado a herramientas de IA.
2. **No exige cambiar de IDE ni de agente** — el flujo de trabajo actual (Android Studio, terminal, Claude, GitHub) se mantiene intacto; Spec Kit solo agrega estructura (templates y comandos) encima.
3. **Encaja con el repositorio ya configurado** — al ser un toolkit basado en archivos y CLI, se integra de forma natural a la estructura `docs/` y al flujo de Git ya definido en `flujo-cicd.md`.
4. **Kiro no aporta ventaja real aquí** — su punto fuerte (integración profunda con AWS/Bedrock) no aplica porque el despliegue de este proyecto usa Railway y Docker, no AWS.

## Alcance piloto de SDD

Se aplicará SDD formal, usando Spec Kit, a tres frentes concretos:

1. **La lógica de rachas (streaks) de hábitos** — reglas de negocio no triviales (qué cuenta como "racha activa", cómo se reinicia, cómo se calcula la racha máxima), ideal para especificar antes de codificar.
2. **Los endpoints principales de la API** (`/habits`, `/habits/{id}/logs`, `/auth`) — contrato claro entre app y backend, útil para que ambos lados se desarrollen contra la misma spec.
3. **El flujo de sincronización offline-first** — es la parte de mayor riesgo de ambigüedad del proyecto (qué pasa con conflictos, qué se prioriza al reconectar), y donde una spec explícita previene retrabajo.

El detalle de instalación y ejecución de este piloto se documenta en `sdd-implementation.md`.
