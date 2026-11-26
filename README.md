# IA agéntica para la investigación

Materiales del curso, una sesión de demostración de 3 horas. Entender qué es un agente
de IA, ver cómo se aplica a dos tareas reales de investigación (reproducir los
resultados de un artículo publicado a partir de sus datos, y construir un análisis de
datos que se verifica a sí mismo), y aprender a verificar sus resultados. Este repositorio te permite repetir ambos ejemplos por tu cuenta
y adaptarlos a tus propios datos.

> **En construcción.** El repositorio se está preparando para el curso. Algunas partes
> todavía pueden cambiar.

## Qué encuentras aquí

| Carpeta o archivo | Qué es |
|---|---|
| [`guia/01-instalacion.md`](guia/01-instalacion.md) | Cómo instalar opencode (el agente que usamos) en Mac o Windows |
| [`guia/02-conceptos.md`](guia/02-conceptos.md) | Los conceptos del curso: qué es un LLM, el bucle del agente, el contexto, los skills, la seguridad y la confianza |
| [`guia/03-beer-lambert.md`](guia/03-beer-lambert.md) | Guía paso a paso del ejemplo de análisis de datos |
| [`ejemplos/beer-lambert/`](ejemplos/beer-lambert/) | Datos, plantilla del skill y solución del ejemplo de análisis de datos |
| [`skills/`](skills/) | Skills de terceros: el skill *grilling* de Matt Pocock (licencia MIT), para planificar con el agente |
| [`AGENTS.md`](AGENTS.md) | Instrucciones para tu propio agente de IA (ver abajo) |

<!-- Pendiente: el ejemplo de reproducir un artículo a partir de sus datos (guía y carpeta en ejemplos/). -->

## Cómo empezar

1. **Instala opencode** siguiendo [`guia/01-instalacion.md`](guia/01-instalacion.md).
2. **Descarga este repositorio** (botón verde *Code* → *Download ZIP* en GitHub) y
   descomprímelo.
3. **Abre la carpeta en opencode** y sigue las guías en orden, o pregúntale directamente
   a tu agente.

## Los ejemplos

- **Análisis de datos: calibración Beer-Lambert.** Con ayuda del agente construyes una
  herramienta que calcula una concentración a partir de espectros UV-Vis. El ajuste sale
  casi perfecto (R² = 0.9998) y aun así la respuesta está equivocada en casi un 20 %. El
  ejemplo enseña a verificar un resultado contra una respuesta conocida.
  **Intenta el ejercicio antes de abrir la solución**
  (`ejemplos/beer-lambert/solucion-referencia.ipynb`); si la lees primero, pierdes la lección.
- **Reproducir un artículo a partir de sus datos.** *(En preparación.)* Un agente lee un
  artículo publicado, descarga los datos que los autores depositaron y reproduce sus
  figuras y tablas. Luego se comprueba cada número contra el artículo, incluido cuántos
  datos entran en cada cálculo.

## Pregúntale a tu agente

Este repositorio incluye un archivo [`AGENTS.md`](AGENTS.md) que los agentes de IA leen
automáticamente. Si abres esta carpeta en opencode (u otro agente), puedes preguntarle en
español sobre cualquier parte del curso: cómo instalar, qué significa un concepto, o por
qué tu resultado no coincide.

## Autor y licencia

Curso preparado por **Juan M. Arce-Ramos**.

El texto, las guías y las figuras están bajo licencia
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.es); el código, bajo licencia
MIT. Puedes reutilizar y adaptar todo citando la fuente. Detalles en [`LICENSE`](LICENSE).
