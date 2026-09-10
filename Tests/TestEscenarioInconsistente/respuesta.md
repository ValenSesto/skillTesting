1. Análisis y Definición de Escenarios
Escenario 1

Entrada del Usuario: "Fuente: Un comprador online. Estímulo: El comprador hace clic en el botón "Agregar al carrito" seleccionando un buzo talle M color negro. Artefacto: Módulo de gestión de inventario y talles de la tienda de indumentaria. Entorno: Operación normal en día de semana. Respuesta: El sistema registra la reserva de la Cancha 3 de sintetico. Medida de respuesta:La cancha queda asignada en la base de datos; Se registra una tasa de cero superposiciones de turnos."
Atributo de Calidad: Consistencia e Integridad de Datos (Data Integrity & Concurrency) | Refinamiento: Control de concurrencia y reserva transaccional de inventario (Prevención de overselling).
Diagnóstico de Completitud:
Fuente: Presente - "Un comprador online" (usuario final externo).
Estímulo: Presente - Selección de variante (talle M, color negro) y acción de agregar al carrito.
Artefacto: Presente - Módulo de gestión de inventario y catálogo de indumentaria.
Entorno: Presente - "Operación normal en día de semana".
Respuesta: Ambiguo / Incoherente (Error semántico) - "El sistema registra la reserva de la Cancha 3 de sintético" pertenece a un dominio de negocio completamente ajeno (alquiler de canchas deportivas) e incompatible con el estímulo y artefacto (tienda de ropa).
Medida de Respuesta: Ambiguo / Incoherente - Medir la no superposición de turnos de una cancha no tiene correlato con el stock de prendas de vestir.
Escenario Formal Propuesto (6 Partes):
Fuente: Comprador online autenticado o anónimo en la tienda web.
Estímulo: El usuario solicita agregar al carrito 1 unidad de buzo talle M color negro.
Artefacto: Módulo de gestión de inventario y reservas temporales de stock.
Entorno: Operación normal de ejecución bajo carga promedio en día hábil.
Respuesta: El sistema verifica la disponibilidad en tiempo real, genera un bloqueo transaccional temporal del artículo en el inventario por 15 minutos y confirma la adición al carrito del comprador.
Medida de Respuesta: Tasa de sobreventa (overselling) = 0% frente a intentos concurrentes sobre la última unidad disponible, con un tiempo de confirmación y bloqueo en la base de datos ≤ 150 milisegundos.
Prioridad: Negocio: Alta | Arquitectura: Media.
Justificación: Se identificó una desconexión crítica entre la primera mitad del escenario (comercio electrónico de indumentaria) y la segunda (reserva de canchas sintéticas). Se corrigió la respuesta y su medida trasladando la lógica de "cero superposiciones" al problema equivalente del ecommerce: bloqueo de stock concurrente y 0% de sobreventa. Se califica con prioridad de negocio alta (la sobreventa destruye la confianza y genera reclamos) y dificultad arquitectónica media (manejo de transacciones atómicas o bloqueos distribuidos en caché/BD).
2. Árbol de Utilidad (Utility Tree)
Utilidad
Consistencia e Integridad de Datos
Control de concurrencia y reserva transaccional de inventario
Reserva temporal de variante de indumentaria en carrito con 0% de sobreventa concurrente en ≤ 150 ms. -> (Alta, Media)
