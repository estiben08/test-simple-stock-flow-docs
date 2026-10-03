# ADR-008: Deptrac para control arquitectónico

**Estado:** Aceptado

**Contexto:** Es muy fácil que un desarrollador viole las capas de Onion (ej. importando Eloquent en Domain).

**Decisión:** Se configurará Qossmic Deptrac en CI para romper el build si Domain depende de Application, Infrastructure o Presentation, o si Application depende de Infrastructure.

**Consecuencias:** Cero tolerancia a violaciones arquitectónicas.
