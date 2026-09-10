1. Análisis y Definición de Escenarios
Escenario 1

Entrada del Usuario: " El sistema debe ser rapido "
Atributo de Calidad: Rendimiento (Performance) | Refinamiento: Latencia y tiempo de respuesta de transacciones.
Escenario Formal Propuesto (6 Partes):
Fuente: Usuarios concurrentes del sistema.
Estímulo: Envío de solicitudes estándar de consulta y lectura de datos.
Artefacto: Capa de servicios y APIs del sistema.
Entorno: Operación normal de ejecución bajo carga promedio estimada.
Respuesta: El sistema procesa la petición y retorna la información solicitada al cliente.
Medida de Respuesta: Latencia en percentil 95 (p95) ≤ 200 milisegundos y tiempo total de respuesta ≤ 500 milisegundos.
Prioridad: Negocio: Alta | Arquitectura: Media.
Justificación: La solicitud original ("ser rápido") es completamente subjetiva y carece de métricas auditables. Se infirió un contexto de operación normal bajo carga estándar y se cuantificó la rapidez a través de un SLA medible de latencia (p95 ≤ 200 ms). Se asigna una prioridad alta para el negocio por su impacto directo en la retención y experiencia de usuario, y una complejidad arquitectónica media asumible con patrones comunes de optimización y caché.
2. Árbol de Utilidad (Utility Tree)
Utilidad
Rendimiento (Performance)
Latencia y tiempo de respuesta de transacciones
Solicitudes de consulta bajo carga normal resueltas con p95 ≤ 200 ms. -> (Alta, Media)
