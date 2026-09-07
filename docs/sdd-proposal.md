# Propuesta de Spec-Driven Development (SDD)

## Contexto

Este proyecto arranca desde cero, sin código previo. Esto lo hace un punto de partida ideal para adoptar Spec-Driven Development desde el día uno, en lugar de aplicarlo por ingeniería inversa sobre un sistema existente.

## Diagnóstico del estado actual

- Código existente: ninguno
- Especificaciones existentes: ninguna
- Herramientas de desarrollo asistido por IA disponibles: Kiro, GitHub Spec Kit

## Comparación: Kiro vs Spec Kit

| Criterio | Kiro | Spec Kit |
|---|---|---|
| Origen | (completar) | GitHub (github.com/github/spec-kit) |
| Enfoque | (completar) | Specs → plan → tasks → implementación |
| Integración con el flujo de trabajo actual | (completar) | (completar) |
| Curva de aprendizaje | (completar) | (completar) |
| Adecuación a este proyecto | (completar) | (completar) |

## Herramienta elegida y justificación

(completar tras investigar ambas opciones)

## Alcance piloto de SDD

Se aplicará SDD formal, usando Spec Kit, a:
1. La lógica de rachas (streaks) de hábitos
2. Los endpoints principales de la API (`/habits`, `/habits/{id}/logs`, `/auth`)
3. El flujo de sincronización offline-first
