# Ejemplo Beer-Lambert — "confía, pero compara"

El ejemplo de análisis de datos del curso. Con ayuda del agente escribes un skill de
opencode que construye una calibración UV-Vis y predice la concentración de una muestra
desconocida. Luego descubres, al compararla con el valor verdadero, que el resultado es
seguro de sí mismo y está *equivocado*, y lo corriges añadiendo un paso de verificación.
La guía paso a paso está en
[../../guia/03-beer-lambert.md](../../guia/03-beer-lambert.md).

## Archivos

| Archivo | Para qué sirve |
|---|---|
| `generate_data.py` | Genera los datos sintéticos y la respuesta verdadera. Determinista (semilla 42). |
| `SKILL.md.template` | La plantilla del skill que completas, milestone por milestone. |
| `solucion-referencia.ipynb` | La solución completa. Intenta el ejercicio antes de abrirla. |
| `data/` | Se crea al generar los datos (git la ignora): espectros de calibración, índice, incógnita y `ground_truth.txt`. |

## Generar los datos

```
python generate_data.py     # necesita numpy
```

Escribe todo en `data/`. El script también imprime los resultados esperados, incluida
la respuesta verdadera; si quieres calcular tu propio número antes de verla, no leas
esas líneas ni abras `data/ground_truth.txt` hasta el milestone M4.

**Resultado esperado (semilla 42):**

| Pipeline | Predice | Error | R² de calibración |
|---|---|---|---|
| Ingenuo (pico crudo, sin corregir la línea base) | 10.78 µM | **+19.8 %** | **0.9998** |
| Con la línea base corregida | 9.03 µM | +0.3 % | 0.9998 |
| **Verdad** | **9.00 µM** | — | — |

Esa es la lección en una tabla: un ajuste casi perfecto (R² = 0.9998) con una respuesta
equivocada en un 20 %. Solo la comparación contra el valor conocido lo revela.
