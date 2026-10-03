# Plan Laravel — Simple Stock Flow

**Decisiones Técnicas Exclusivas para la Implementación en PHP / Laravel**

Este documento rige la forma en la que se aplicará la Arquitectura Onion de 4 capas al framework Laravel, evitando que las convenciones del framework (Active Record, Facades, inyección automática) rompan las invariantes de negocio establecidas en el spec principal.

## 1. Arquitectura Onion (4 Anillos + Bootstrap)

El código fuente del servicio (`test-simple-stock-flow-api`) se estructurará en 5 componentes principales dentro de `app/`:

1. **`Domain/` (Anillo 1):** Entidades, Value Objects e invariantes. Cero dependencias externas. No puede existir la palabra `Illuminate` aquí.
2. **`Application/` (Anillo 2):** Casos de uso y Puertos (Inbound y Outbound). Orquesta el dominio.
3. **`Infrastructure/` (Anillo 3):** Implementaciones concretas de persistencia (Eloquent), Mappers, Seguridad (JWT) y Almacenamiento.
4. **`Presentation/` (Anillo 4):** Controladores REST, Rutas (`api.php`), FormRequests (solo validación de forma, no de negocio) y Formateo de Errores (422, 400).
5. **`Bootstrap/`:** Punto de ensamblaje (Service Providers). El único lugar donde se unen las abstracciones (`Application`) con las implementaciones (`Infrastructure`).

## 2. Trampas de Laravel resueltas

### Eloquent (Active Record)
- **Regla:** Ningún modelo de Eloquent cruzará la frontera de `Infrastructure`. `Domain` operará con clases PHP puras. 
- **Mecanismo:** Se utilizarán **Mappers** en `Infrastructure/Persistence/Mapper` para convertir entre Entidades de Dominio y Modelos de Eloquent.

### Facades y Helpers Globales
- **Regla:** Prohibido el uso de Facades (`DB::`, `Log::`) o helpers (`now()`, `config()`) en `Domain` o `Application`.
- **Mecanismo:** Inyección de dependencias a través de puertos definidos en `Application/Ports/Outbound/`.

### Validaciones (FormRequests)
- **Regla:** Los FormRequests de Laravel solo se usarán para validar **forma y tipo** (400 Bad Request). Toda lógica o regla de negocio (ej. "stock no puede ser negativo") se validará en `Domain` y lanzará un 422 Unprocessable Entity mediante una excepción personalizada.

## 3. Tipos de Datos (Decimales)
- PHP no cuenta con un tipo numérico decimal nativo y el uso de `float` causaría pérdida de precisión en transacciones financieras.
- **Decisión:** Se utilizará la librería `Brick\Math\BigDecimal` en el Value Object `Money`, configurada con escala a 2 decimales y redondeo `HALF_UP`.

## 4. Control de Concurrencia
- **Mecanismo:** El modelo Eloquent de Productos incluirá una columna `version`. El Mapper validará esta versión al hacer un `UPDATE`. Si se afectan 0 filas, se lanzará una `ConcurrencyConflictException` (409 Conflict). El dominio permanecerá agnóstico a esta columna `version`.

## 5. Análisis Estático y Validación Arquitectónica
- Se usará **Deptrac** para garantizar (vía CI) que la regla de dependencias (R-01 a R-06) no se rompa (ej. `Domain` importando `Illuminate`).
- Se usará **PHPStan** (nivel máximo) junto con **Larastan** para asegurar tipado estricto.
- Se usará **PHPUnit 11** para las pruebas (sustituyendo a `pytest`).
