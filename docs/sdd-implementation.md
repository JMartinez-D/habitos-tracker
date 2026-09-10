# Guía de Implementación de SDD

## ¿Qué es Spec-Driven Development?

Es un enfoque donde la especificación —no el código— es la fuente de verdad del proyecto. En vez de escribir código primero y documentar después (o no documentar), se define primero **qué** debe hacer una funcionalidad (spec), luego **cómo** se va a construir (plan técnico), después se descompone en tareas concretas, y solo entonces se implementa. Cuando algo no queda claro durante la implementación, se vuelve a la spec en vez de improvisar sobre el código. Esto reduce ambigüedad para el desarrollador y para cualquier agente de IA que participe en la implementación, porque ambos trabajan contra el mismo documento de referencia.

## Instalación de Spec Kit

Spec Kit se distribuye como un CLI (`specify`) que se instala mediante `uv`, el gestor de paquetes de Python.

**1. Instalar `uv`:**

En Windows (PowerShell):
```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

**2. Instalar el CLI de Spec Kit:**
```
uv tool install specify-cli
```

**3. Inicializar Spec Kit dentro del repositorio del proyecto:**
```
specify init . --integration claude
```

Esto descarga los templates oficiales y crea la estructura de SDD (constitución del proyecto, templates de spec/plan/tareas) configurada para trabajar con Claude como agente.

## Flujo de trabajo con Spec Kit

1. **`/constitution`** — se define una sola vez al inicio: principios y estándares del proyecto (ej. "toda funcionalidad de sincronización debe ser idempotente", "las validaciones de negocio viven en la capa de dominio, no en la UI")
2. **`/specify`** — se describe la funcionalidad en lenguaje natural (ej. "el usuario puede marcar un hábito como completado una vez al día y ver su racha actual")
3. **`/plan`** — Spec Kit genera el plan técnico a partir de la spec (qué componentes tocar, qué contratos de API, qué modelos de datos)
4. **`/tasks`** — el plan se desglosa en tareas pequeñas y accionables
5. **`/analyze`** — verifica que spec, plan y tareas sean consistentes entre sí antes de implementar
6. Implementación guiada por las tareas generadas, con la spec como referencia si surge ambigüedad

## Aplicación al piloto de este proyecto

| Piloto (definido en `sdd-proposal.md`) | Qué se especifica primero |
|---|---|
| Lógica de rachas | Reglas exactas: qué cuenta como día cumplido, cómo se calcula racha actual vs. racha máxima, qué pasa al saltar un día |
| Endpoints de la API | Contrato de cada endpoint (`/habits`, `/habits/{id}/logs`, `/auth`): payloads, códigos de respuesta, validaciones |
| Sincronización offline-first | Reglas de resolución de conflictos, qué gana al reconectar (local vs. remoto), idempotencia de la sincronización |

## Beneficios esperados para este proyecto

- **Menos retrabajo en la lógica de rachas y sincronización**, que son las partes con más reglas de negocio implícitas y mayor riesgo de ambigüedad
- **Contrato claro entre app y API** antes de escribir código en ambos lados, evitando descubrir incompatibilidades a mitad de desarrollo
- **Documentación que no se desactualiza sola** — la spec vive junto al código y se referencia en cada implementación, en vez de quedar como un documento que se escribió una vez y se olvidó
- **Costo cero** y sin cambiar de herramientas de desarrollo (ver justificación completa en `sdd-proposal.md`)

## Seguimiento

| Fecha | Spec trabajada | Estado | Notas |
|---|---|---|---|
| | Constitución del proyecto | Pendiente | |
| | Lógica de rachas | Pendiente | |
| | Endpoints de la API | Pendiente | |
| | Sincronización offline-first | Pendiente | |
