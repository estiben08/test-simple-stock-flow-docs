# GUIA ONION

**ACLARACIÓN IMPORTANTE SOBRE LA ESPECIFICACIÓN ORIGINAL**

La especificación original de este proyecto (ubicada en spec-python/ y spec-.net/) documentaba una **Arquitectura Hexagonal**. Sin embargo, por requerimiento estricto de la evaluación, este proyecto se ha traducido e implementado utilizando **Arquitectura Onion (Cebolla)** de 4 capas.

Las 4 capas son:
1. **Domain** (Centro de la cebolla)
2. **Application**
3. **Infrastructure**
4. **Presentation** (Capa más externa)

Cualquier mención a 'Puertos y Adaptadores' en el sentido Hexagonal debe entenderse bajo el prisma de Onion, donde los puertos viven en Application y los adaptadores se dividen entre Infrastructure (Persistencia) y Presentation (HTTP).
