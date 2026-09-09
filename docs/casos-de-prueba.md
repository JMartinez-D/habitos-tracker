# Casos de Prueba

| ID | Descripción | Pasos | Resultado esperado |
|---|---|---|---|
| CP-01 | Crear hábito con nombre vacío | 1. Abrir "nuevo hábito" 2. Dejar nombre vacío 3. Guardar | Muestra error de validación, no se crea el hábito |
| CP-02 | Marcar hábito completado dos veces el mismo día | 1. Marcar hábito como hecho 2. Intentar marcarlo de nuevo | No duplica el registro ni la racha |
| CP-03 | Uso sin conexión | 1. Desactivar red 2. Crear/editar hábito 3. Reactivar red | Cambios se guardan localmente y sincronizan al reconectar |
| CP-04 | Cálculo de racha tras un día saltado | 1. Completar hábito 2 días seguidos 3. Saltar un día 4. Completar de nuevo | Racha se reinicia en 1, racha máxima se conserva |
| CP-05 | Login con credenciales inválidas | 1. Ingresar usuario/contraseña incorrectos | Muestra error, no autentica |
| CP-06 | Eliminar hábito | 1. Eliminar un hábito existente | Hábito y sus logs asociados desaparecen de la app y (tras sync) del backend |

*(agregar más casos conforme se defina el alcance final del MVP)*
