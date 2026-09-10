### 1. Análisis y Definición de Escenarios
  ──────
  #### Escenario 1
  • Entrada del Usuario: "El sistema debe reportar cualquier alarma crítica (por ej., una alarma de incendio), aún cuando existan problemas de conectividad, sin que se degrade el tiempo de respuesta desde que sucede el
  evento hasta que el sistema la reporta (por ej., 2 segundos)."
  • Atributo de Calidad: Disponibilidad (Availability) | Refinamiento: Tolerancia a fallos de conectividad y latencia garantizada en alarmas críticas.
  • Diagnóstico de Completitud:
      • Fuente: Ambiguo - Menciona "alarma crítica/incendio", pero no delimita el sensor o subsistema detector que emite la señal física original.
      • Estímulo: Presente - Detección y activación de una alarma crítica de emergencia.
      • Artefacto: Ambiguo - "El sistema" no especifica si corresponde al controlador local (edge), al bus de eventos o a la estación central de monitoreo.
      • Entorno: Presente - Operación bajo condiciones de fallo o degradación en la red de conectividad.
      • Respuesta: Presente - Reportar y notificar la alarma crítica sin degradar la operación.
      • Medida de Respuesta: Parcial - Propone a modo de ejemplo "2 segundos", pero falta acotar la cota estricta de entrega y la tasa de pérdida tolerable (0%).
  • Escenario Formal Propuesto (6 Partes):
      • Fuente: Sensor de seguridad física en campo (ej. detector de humo o conato de incendio).
      • Estímulo: Activación y envío de una señal de alarma de severidad crítica.
      • Artefacto: Controlador local / Gateway de campo (Edge Controller) y servicio de despacho de emergencias.
      • Entorno: Modo degradado por pérdida total o fluctuación severa de la conectividad de red principal (WAN / Internet).
      • Respuesta: El controlador local procesa la alarma de forma autónoma con máxima prioridad de scheduling, conmuta a canal redundante local (red mesh / enlace celular de contingencia) y activa los protocolos de
      notificación sonoro-visuales y brigadas de respuesta.
      • Medida de Respuesta: La alarma es despachada y reportada al personal/sistemas de respuesta en un tiempo ≤ 2 segundos desde la ocurrencia del evento físico, con 0% de pérdida de alarmas críticas.
  • Prioridad: Negocio: Alta | Arquitectura: Alta.
  • Justificación: La preservación de vidas humanas y activos físicos hace indispensable este escenario. A nivel arquitectónico, garantizar latencias acotadas ante particiones de red requiere arquitecturas de borde (Edge
  Computing), persistencia local tolerante a desconexión y conmutación por fallo (failover) sin intervención manual.
  ──────
  #### Escenario 2
  • Entrada del Usuario: "El sistema debe dar soporte para integrar dispositivos de un abanico de fabricantes, y permitir que estos dispositivos puedan interactuar entre si y con el resto del sistema (por ej., dispositivos
  Siemens, Honeywell, etc.)"
  • Atributo de Calidad: Interoperabilidad (Interoperability) | Refinamiento: Integración sintáctica y semántica de dispositivos heterogéneos (multi-vendor).
  • Diagnóstico de Completitud:
      • Fuente: Ausente - No indica quién integra los dispositivos ni qué actor dispara la interacción inter-dispositivo.
      • Estímulo: Ambiguo - "Integrar dispositivos" y "permitir que interactúen" no detalla los protocolos industriales ni el formato de los mensajes.
      • Artefacto: Ambiguo - "El sistema" no señala la capa de abstracción, adaptadores o broker de integración.
      • Entorno: Ausente - No especifica si ocurre en tiempo de configuración o durante la ejecución normal en campo.
      • Respuesta: Ambiguo - "Interactuar entre sí y con el resto" no detalla la normalización ni traducción sintáctica/semántica de mensajes.
      • Medida de Respuesta: Ausente - No establece métricas de esfuerzo de integración, tiempo de procesamiento ni tasas de éxito en la comunicación.
  • Escenario Formal Propuesto (6 Partes):
      • Fuente: Integrador de automatización o dispositivos de campo de fabricantes heterogéneos (ej. Honeywell, Siemens, Schneider).
      • Estímulo: Solicitud de incorporación de un nuevo dispositivo y flujo bidireccional continuo de comandos/telemetría bajo protocolos industriales diversos (BACnet, Modbus, OPC UA o MQTT).
      • Artefacto: Capa de Interoperabilidad y Adaptadores de Dispositivos (Device Integration Gateway & Message Broker).
      • Entorno: Operación normal en tiempo de ejecución (runtime) con múltiples dispositivos concurrentes en la red de control.
      • Respuesta: El sistema registra el nuevo dispositivo a través de su adaptador específico, transforma los mensajes al modelo canónico de datos de la plataforma y enruta las órdenes posibilitando la comunicación
      directa y coordinada entre dispositivos y hacia el core.
      • Medida de Respuesta: Integración y configuración de un nuevo protocolo de fabricante en ≤ 3 días-hombre, y tasa de entrega exitosa de mensajes inter-dispositivo ≥ 99.9% con una sobrecarga (overhead) de
      transformación ≤ 100 ms.
  • Prioridad: Negocio: Alta | Arquitectura: Alta.
  • Justificación: Es un factor clave de negocio para evitar el vendor lock-in y ganar competitividad en licitaciones de edificios inteligentes/industria. En la arquitectura, demanda desacoplamiento estricto mediante
  patrones de integración (Adapter Pattern, Canonical Data Model y Message Routing) para evitar que cambios de un fabricante afecten a los demás.
  ──────
  #### Escenario 3

  • Entrada del Usuario: "El sistema debe permitir que se puedan incorporar extensiones de funcionalidad (por ej., soporte para tablets para el monitoreo, mecanismos de auto-control de temperatura, etc.) sin necesidad de
  tener que desarrollar todo el sistema de nuevo."
  • Atributo de Calidad: Modificabilidad (Modifiability) | Refinamiento: Extensibilidad modular e independencia de componentes.
  • Diagnóstico de Completitud:
      • Fuente: Ausente - No aclara qué equipo o rol realiza la incorporación de la nueva funcionalidad.
      • Estímulo: Presente (parcial) - Incorporar extensiones como interfaces para tablets o auto-control de temperatura.
      • Artefacto: Ambiguo - "Todo el sistema" no delimita las capas o límites arquitectónicos impactados.
      • Entorno: Ambiguo - No define en qué fase del ciclo de vida del software se efectúa el cambio.
      • Respuesta: Ambiguo - "Sin necesidad de tener que desarrollar todo el sistema de nuevo" es un objetivo cualitativo sin especificación técnica.
      • Medida de Respuesta: Ausente - No incluye métricas cuantitativas de esfuerzo, costo, tiempo ni aislamiento de cambios.
  • Escenario Formal Propuesto (6 Partes):
      • Fuente: Desarrollador del equipo de ingeniería de producto.
      • Estímulo: Requerimiento de incorporar una nueva capacidad funcional o canal de usuario (ej. lógica de auto-control de temperatura o cliente de monitoreo para tablets).
      • Artefacto: Arquitectura modular del sistema (núcleo de la aplicación, APIs de integración y sistema de plugins/extensiones).
      • Entorno: Tiempo de diseño, desarrollo y despliegue continuo (fase de evolución).
      • Respuesta: El desarrollador implementa la nueva funcionalidad mediante contratos de interfaz definidos (APIs abiertas / SPIs) y despliega el componente sin modificar ni recompilar el código base central (core).
      • Medida de Respuesta: La nueva extensión se desarrolla, testea y despliega en ≤ 5 días-hombre, con 0 líneas de código modificadas en el núcleo existente y 0% de regresiones en las pruebas automáticas.
  • Prioridad: Negocio: Alta | Arquitectura: Media.
  • Justificación: La extensibilidad continua reduce el costo total de propiedad (TCO) y acelera el time-to-market. Arquitectónicamente se resuelve aplicando estilos probados de bajo acoplamiento (arquitectura hexagonal /
  ports & adapters, o arquitectura de microkernel/plugins) con dificultad técnica media.
  ──────
  #### Escenario 4

  • Entrada del Usuario: "El sistema debe poder correrse en una versión Web, tanto en Safari como en Chrome."
  • Atributo de Calidad: Portabilidad (Portability) | Refinamiento: Compatibilidad multiplataforma y soporte cross-browser.
  • Diagnóstico de Completitud:
      • Fuente: Ausente - No especifica el actor que interactúa con la plataforma web.
      • Estímulo: Ambiguo - "Poder correrse", sin describir las operaciones interactivas ni el flujo de uso.
      • Artefacto: Ambiguo - "El sistema" no delimita la aplicación web cliente (frontend).
      • Entorno: Parcial - Nombra Chrome y Safari, pero omite versiones soportadas, resoluciones o sistemas operativos subyacentes.
      • Respuesta: Ambiguo - No detalla la paridad visual, funcional ni de rendimiento esperada en cada motor de renderizado.
      • Medida de Respuesta: Ausente - No establece umbrales de compatibilidad, tiempos de carga ni límites de errores de ejecución.
  • Escenario Formal Propuesto (6 Partes):
      • Fuente: Usuario final (operador de monitoreo o administrador de planta).
      • Estímulo: Acceso y operación completa de la plataforma web desde las últimas dos versiones estables de Google Chrome y Apple Safari.
      • Artefacto: Aplicación cliente Web (Single Page Application / Frontend UI).
      • Entorno: Operación normal en estaciones de trabajo y dispositivos móviles sobre macOS, iOS, Windows y Android.
      • Respuesta: La interfaz web se renderiza correctamente adoptando un diseño responsivo y ejecutando todas las capacidades interactivas utilizando exclusivamente estándares abiertos W3C (HTML5, CSS3, ECMAScript
      estándar), sin requerir extensiones propietarias.
      • Medida de Respuesta: 100% de paridad funcional y consistencia visual entre ambos navegadores, tiempo interactivo inicial (Time to Interactive - TTI) ≤ 2 segundos bajo conexión estándar, y 0 defectos críticos de
      compatibilidad en la suite de pruebas automatizadas cross-browser.
  • Prioridad: Negocio: Media | Arquitectura: Baja.
  • Justificación: Brinda flexibilidad y acceso ubicuo al usuario corporativo. Arquitectónicamente la complejidad es baja, dado que los frameworks web modernos (React, Angular o Vue) junto con herramientas estándar de
  transpilación y empaquetado (bundlers) resuelven de forma transparente las diferencias entre los motores Blink (Chrome) y WebKit (Safari).
  ──────
  ### 2. Árbol de Utilidad (Utility Tree)

  • Utilidad
      • Disponibilidad (Availability)
	  • Tolerancia a fallos de conectividad y latencia garantizada en alarmas críticas
              • Alarma crítica procesada localmente y reportada en ≤ 2 s ante fallas de red con 0% de pérdida. → (Alta, Alta)

      • Interoperabilidad (Interoperability)
	  • Integración sintáctica y semántica de dispositivos heterogéneos
              • Integración de nuevo fabricante (Siemens, Honeywell, etc.) en ≤ 3 días-hombre con entrega de mensajes ≥ 99.9%. → (Alta, Alta)

      • Modificabilidad (Modifiability)
	  • Extensibilidad modular e independencia de componentes
              • Incorporación de extensiones funcionales (tablets, auto-control) en ≤ 5 días-hombre con 0 cambios en el core. → (Alta, Media)

      • Portabilidad (Portability)
	  • Compatibilidad multiplataforma y soporte cross-browser
              • Ejecución web en Chrome y Safari con 100% de paridad funcional y TTI ≤ 2 s. → (Media, Baja)
