# ADR-009: Aislamiento del framework Laravel

**Estado:** Aceptado

**Contexto:** Laravel fomenta el acoplamiento global (Facades, helpers).

**Decisión:** Prohibido el uso de Facades y helpers globales en Domain y Application. FormRequests solo validan forma (400), el Domain valida negocio (422).

**Consecuencias:** El núcleo del negocio podrá ser testeado sin iniciar el framework.
