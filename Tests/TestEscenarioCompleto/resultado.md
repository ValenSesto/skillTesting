### 1. Análisis y Definición de Escenarios

**Escenario 1**
* **Entrada del Usuario:** "Fuente: Usuario administrador autenticado. Estímulo: Solicita exportar un reporte de 50.000 registros. Artefacto: Módulo de reportes. Entorno: Horario laboral, carga normal. Respuesta: El sistema genera el archivo CSV de forma asíncrona y notifica por email al finalizar. Medida de Respuesta: El archivo se genera en menos de 2 minutos y el email llega en menos de 30 segundos tras la finalización."
* **Atributo de Calidad:** Rendimiento (Performance) | **Refinamiento:** Procesamiento asíncrono de operaciones pesadas.
* **Diagnóstico de Completitud:**
  * Escenario completo - sin partes faltantes. Las 6 partes canónicas fueron provistas explícitamente por el usuario sin ambigüedad.
* **Escenario Formal Propuesto (6 Partes):**
  * **Fuente:** Usuario administrador autenticado.
  * **Estímulo:** Solicita exportar un reporte de 50.000 registros.
  * **Artefacto:** Módulo de reportes.
  * **Entorno:** Horario laboral, carga normal.
  * **Respuesta:** El sistema genera el archivo CSV de forma asíncrona y notifica por email al finalizar.
  * **Medida de Respuesta:** El archivo se genera en menos de 2 minutos y el email llega en menos de 30 segundos tras la finalización.
* **Prioridad:** Negocio: Media | Arquitectura: Media.
* **Justificación:** El escenario llegó completo y sin ambigüedades, por lo que no fue necesario inventar ni ajustar elementos. La prioridad de negocio es Media debido a que se trata de una operación administrativa sin impacto directo en transacciones de clientes finales, y la dificultad arquitectónica es Media al requerir desacoplamiento asíncrono (colas de tareas, workers de fondo y servicio de correo).

---

### 2. Árbol de Utilidad (Utility Tree)

* **Utilidad**
  * **Rendimiento (Performance)**
    * **Procesamiento asíncrono de operaciones pesadas**
      * Exportación de 50.000 registros a CSV en < 2 min, con notificación por email en < 30s. -> **(Media, Media)**
