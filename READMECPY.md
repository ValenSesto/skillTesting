# SEI Quality Attribute & Utility Tree Expert (Skill para IA)

Esta skill transforma cualquier modelo de Inteligencia Artificial en un **Arquitecto de Software Experto** basado en los estándares del **SEI (Software Engineering Institute)** y el método **ATAM** (*Software Architecture in Practice*, 4ta Edición).

Permite auditar requisitos no funcionales, completar escenarios vagos en su estructura canónica de **6 partes** y consolidarlos en un **Árbol de Utilidad (Utility Tree)** con priorización bidimensional (Negocio vs. Arquitectura).

---

## 📁 Ubicación del Archivo de la Skill

El archivo principal con la definición, reglas de negocio y ejemplos *few-shot* se encuentra en:
```text
./.agents/skills/QAScenarios/SKILL.md
```

---

## 🚀 Cómo ejecutar la Skill con cualquier IA (Guía paso a paso)

Dependiendo de la herramienta o entorno de Inteligencia Artificial que utilices, ejecuta los siguientes comandos en tu terminal desde la raíz de este repositorio:

---

### Opción 1: Con Google Antigravity (`agy` CLI o Antigravity IDE)

Google Antigravity lee de forma nativa los archivos `SKILL.md` dentro de la ruta `./.agents/skills/`.

#### A. A nivel de Proyecto (Workspace local)
Si ejecutas `agy` o abres esta carpeta en el IDE, la skill ya está disponible automáticamente por convención de workspace:
```bash
# Iniciar Antigravity dentro del directorio del proyecto
agy
```

#### B. A nivel Global (disponible en cualquier proyecto o carpeta de tu máquina)
Para que la skill esté activa en cualquier conversación de Antigravity sin importar en qué carpeta estés parado:
```bash
# Crear el directorio de skills globales si aún no existe
mkdir -p ~/.gemini/config/skills

# Copiar la skill a la configuración global
cp -r "./.agents/skills/QAScenarios" ~/.gemini/config/skills/
```

---

### Opción 2: Con Agentes y Editores de Código (Claude Code, Cursor, Aider)

Si utilizas otros asistentes de desarrollo basados en terminal o editor, puedes vincular o copiar la skill a los puntos de configuración que cada herramienta espera:

#### Para Claude Code:
```bash
# Configura las instrucciones de contexto para Claude Code
cp ./.agents/skills/QAScenarios/SKILL.md ./CLAUDE.md
```

#### Para Cursor IDE:
```bash
# Configura las instrucciones como reglas globales del proyecto
cp ./.agents/skills/QAScenarios/SKILL.md ./.cursorrules
```

---

### Opción 3: Con Modelos Locales en Terminal (Ollama)

Si ejecutas modelos de forma local con **Ollama**, puedes pasarle el archivo directamente como prompt de sistema:

```bash
# Ejecutar con Llama 3 (o el modelo que tengas instalado)
ollama run llama3 "$(cat ./.agents/skills/QAScenarios/SKILL.md)"
```

---

### Opción 4: Con cualquier IA Web (ChatGPT, Claude.ai, Gemini, DeepSeek, Copilot)

Si vas a usar una interfaz web en el navegador, no necesitas la terminal. Puedes activarla siguiendo estos sencillos pasos con atajos de teclado:

1. **Abrir el archivo:**
   Abre el archivo [SKILL.md](./.agents/skills/QAScenarios/SKILL.md) con tu editor de texto preferido (VS Code, Bloc de notas, o directamente desde GitHub/GitLab).

2. **Copiar todo el contenido:**
   * Presiona <kbd>Ctrl</kbd> + <kbd>A</kbd> (o <kbd>Cmd</kbd> + <kbd>A</kbd> en Mac) para seleccionar todo el texto.  
   * Presiona <kbd>Ctrl</kbd> + <kbd>C</kbd> (o <kbd>Cmd</kbd> + <kbd>C</kbd> en Mac) para copiarlo.

3. **Cargar la skill en la IA:**
   * Abre la web de tu IA favorita en el navegador.
   * Pégalo con <kbd>Ctrl</kbd> + <kbd>V</kbd> (o <kbd>Cmd</kbd> + <kbd>V</kbd> en Mac) en:
     * Las **Instrucciones Personalizadas** (*Custom Instructions* / *System Prompt* en los ajustes del perfil), **O**
     * Directamente como el **primer mensaje** del chat y envíalo con <kbd>Enter</kbd>.

4. **Comenzar a usar:**
   * A partir de ahí, escribe en el chat tus requisitos o ideas de arquitectura (incluso si están incompletos o en lenguaje coloquial). La IA responderá aplicando la metodología SEI.

---

## 📋 Estructura Canónica del SEI aplicada por la Skill

La IA descompondrá cada requisito en las 6 partes obligatorias:
1. **Fuente del estímulo (*Source*):** Quién o qué genera el evento (usuario, atacante, sensor, falla interna).
2. **Estímulo (*Stimulus*):** Condición o evento que arriba al sistema (concurrencia pico, caída de nodo, intento de acceso).
3. **Artefacto (*Artifact*):** Componente o subsistema estimulado (UI, API Gateway, base de datos).
4. **Entorno (*Environment*):** Estado operacional (modo normal, sobrecarga pico, recuperación, tiempo de desarrollo).
5. **Respuesta (*Response*):** Comportamiento observable de la arquitectura (failover, degradación elegante, registro).
6. **Medida de respuesta (*Response Measure*):** Métrica cuantificable (latencias p95, RTO/RPO, porcentaje de error, horas-hombre).

---

## 💡 Flujo de Salida de la IA

Ante cualquier entrada, la IA entregará:
1. **Diagnóstico de Completitud:** Tabla indicando qué partes están *Presentes*, *Ausentes* o *Ambiguas*.
2. **Escenario Formal Propuesto:** Las 6 partes completadas sin ambigüedad técnica.
3. **Prioridad y Justificación:** Priorización en formato `(Negocio, Arquitectura)`.
4. **Árbol de Utilidad (Utility Tree):** Consolidación jerárquica de todos los escenarios tratados.
