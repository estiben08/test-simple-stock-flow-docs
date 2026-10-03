# ADR-010: Docker Compose y dependencias locales

**Estado:** Aceptado

**Contexto:** El repositorio infra orquesta todo, pero vendor/ y node_modules/ vacíos causan fallos en Windows al montar volúmenes.

**Decisión:** Se usarán volúmenes anónimos o nombrados en Docker para vendor y node_modules, aislando las dependencias del host local. Se debe correr un servicio efímero de composer install y npm ci.

**Consecuencias:** El entorno funciona idéntico en cualquier máquina sin ensuciar el host.
