# Documentación sobre el proceso de creación de la skill

## 1. Elección de la IA y definición de la base

Decidimos implementar **Gemini** como nuestra IA para armar y probar las skills debido a ya estar familiarizados con la misma al usarla desde antes. 

* Comenzamos por pedirle a la propia inteligencia artificial que arme la skill e ir comparando con el libro y ejercicios hechos previamente para ir encontrando una base.
* Al utilizar la propia IA como referente, pudimos ir acomodando cada una de las partes para que la IA las identifique por separado:
  * **Fuente**
  * **Estímulo**
  * **Artefacto**
  * **Ambiente (Entorno)**
  * **Respuesta**
  * **Medida de respuesta**

---

## 2. Pruebas, validación cruzada y ajustes

Luego nos pusimos a probarla utilizando:
* Casos existentes sacados del libro.
* Casos pensados por nosotros.
* E incluso recurrimos a otras IAs como **Claude** para poder verificar que nuestros casos estaban bien armados y que la skill fuera utilizada de la manera adecuada.

### Aspectos corregidos durante las pruebas:
* Al momento de realizar una respuesta, **evitar la generación de contenido redundante**.
* **Acomodar la ambigüedad de las respuestas** para que fuera posible aplicar a más casos.
* **Identificar contenido erróneo**, como atributos de calidad mal interpretados y su debida corrección y seguimiento, entre otros.

---

## 3. Resultado final

Finalmente, luego de armar varios testeos, conseguimos armar una skill a la que una IA pueda acceder eficazmente para:

1. **Identificar atributos de calidad.**
2. **Reconocer en caso de información faltante.**
3. **Definir correctamente el escenario de calidad.**
4. **Proponer una prioridad de arquitectura y negocio.**
5. **Justificar sus decisiones.**
