# ADR-006: Puertos en la capa Application

**Estado:** Aceptado

**Contexto:** En Onion, la comunicación desde Application hacia Infrastructure debe hacerse mediante interfaces (Dependency Inversion).

**Decisión:** Se crearán dos carpetas en Application/Ports: Inbound (para que Presentation sepa cómo hablar con Application) y Outbound (para que Application defina qué necesita de Infrastructure, como Repositorios).

**Consecuencias:** Asegura que Application no dependa de Infrastructure.
