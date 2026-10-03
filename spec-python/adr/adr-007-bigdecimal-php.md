# ADR-007: Uso de BigDecimal para Dinero

**Estado:** Aceptado

**Contexto:** Los flotantes en PHP causan errores de precisión en cálculos monetarios.

**Decisión:** Se usará brick/math (BigDecimal) para manejar todo campo monetario. Escala 2, redondeo HALF_UP.

**Consecuencias:** Obliga a mapear a string/int en la DB y a string en el JSON de salida.
