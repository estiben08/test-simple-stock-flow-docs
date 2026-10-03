# ADR-005: Transición de Hexagonal a Onion

**Estado:** Aceptado

**Contexto:** La especificación original (Python/.NET) plantea una Arquitectura Hexagonal. Sin embargo, para la implementación final se nos requiere usar Arquitectura Onion.

**Decisión:** Se estructurará el código en 4 capas estrictas (Domain, Application, Infrastructure, Presentation) según la teoría clásica de Onion, descartando la terminología de puertos y adaptadores de la capa exterior (Hexagonal), pero manteniendo los puertos Inbound/Outbound dentro de la capa Application para la inyección de dependencias.

**Consecuencias:** Habrá que hacer un mapeo mental. Lo que en Hexagonal era el 'Core', aquí será Domain + Application. Lo que eran 'Adaptadores', aquí serán Infrastructure y Presentation.
