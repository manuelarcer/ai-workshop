# Ejemplo Gong 2022: explorar y reproducir una base de datos publicada

El ejemplo de datos reales del curso. Usamos la base de datos que depositaron los autores
de un artículo, la exploramos con un tablero (dashboard) interactivo y comprobamos si los
números del artículo salen de los archivos. Los datos **no** están en este repositorio:
se descargan del depósito de los autores (abajo).

## El artículo

S. Gong, S. Wang, T. Xie, W. H. Chae, R. Liu, Y. Shao-Horn, J. C. Grossman,
"Calibrating DFT Formation Enthalpy Calculations by Multifidelity Machine Learning",
*JACS Au* **2022**, 2, 1964–1977. https://doi.org/10.1021/jacsau.2c00235

| Archivo | Contenido |
|---|---|
| `gong-2022-jacsau.pdf` | El artículo (14 páginas). |
| `gong-2022-jacsau-SI.pdf` | La información suplementaria (SI). |

El artículo es de acceso abierto bajo licencia
[CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/deed.es): se incluye
aquí sin cambios, con fines no comerciales y citando a los autores.

**En dos frases.** Un random forest aprende la diferencia entre la entalpía de formación
experimental y la de Materials Project (MP), usando la composición y el valor de MP como
entradas (1143 materiales). El modelo baja el error frente a experimento de 0.0955 a
0.0617 eV/átomo y los autores lo aplican a unos 98 000 materiales de MP para recalcular
la energía sobre el casco convexo (*energy above hull*).

## Los datos: dónde descargarlos

- **Depósito (figshare):** https://doi.org/10.6084/m9.figshare.19100645.v1
- Descarga el archivo comprimido (unos 29 MB; sin comprimir, unos 100 MB con scripts y
  modelos) y descomprímelo en una carpeta `data/` junto a tu proyecto.
- Empieza por `data/README.txt`, que es la descripción de los propios autores.

| Archivo del depósito | Qué contiene | Figura o tabla |
|---|---|---|
| `datasets/mp_corrected_formation_energies_with_corrected_ehull.csv` | **La base principal del ejemplo**: ΔHf de MP y de ML, y Ehull de MP y de ML, por material | Fig. 3b, Tabla 3 |
| `datasets/experimental_dataset.csv` | Los 1143 materiales con ΔHf experimental y de MP | Fig. 1c,d |
| `datasets/train.csv`, `datasets/test.csv` | La división 80/20 usada para la Fig. 2a | Fig. 2a |
| `datasets/comparision_with_functionals_corrections.csv` | 122 materiales con ΔHf de varios funcionales | Tabla 1 |
| `datasets/rf_leave_one_out_result_1.csv` | Predicciones *leave-one-out* de los 1143 materiales | Tabla 1, Fig. S1 |
| `scripts/`, `models/` | Código de entrenamiento y el modelo de producción | — |

Para el panel de estructuras cristalinas del tablero necesitas una clave de la API de
Materials Project (gratuita, desde tu cuenta en https://next-gen.materialsproject.org), guardada en
la variable de entorno `MP_API_KEY`.

## Qué hicimos en la demo

1. **Leer el artículo** y pedir al agente la pregunta, los conjuntos de datos y dónde
   están depositados, con número de página para cada dato.
2. **Describir los archivos**: filas, columnas, unidades y qué figura sostiene cada uno.
3. **Reproducir**: recalcular cada número de figura o tabla desde los archivos y explicar
   cada diferencia.
4. **Planear el tablero con el skill `grilling`**: el agente inspecciona los datos y luego
   pregunta, por rondas y con una recomendación por pregunta, hasta que no queda ninguna
   decisión abierta. Resultado: 3 rondas, 19 decisiones y un `PLAN.md` con 6 pruebas de
   aceptación, antes de escribir código.
5. **Construir el tablero** (Streamlit + plotly + py3Dmol) a partir de ese plan.

## Lo que encontramos al reproducir (para comentar en clase)

Medido sobre los archivos el 2026-11-26.

| Qué | Artículo | Archivos |
|---|---|---|
| Materiales en la base principal | 98 338 (p. 11) | 98 337 filas |
| Ehull_MP > 0.16 y Ehull_ML < 0.06 eV/átomo (Fig. 3b) | "800" (p. 7) | 802 |
| Ehull_MP < 0.06 y Ehull_ML > 0.16 eV/átomo | "1000" (p. 7) | 1030 |
| MnSnIr: Ehull_MP / ΔHf_ML (eV/átomo) | 0.5117 / −0.2363 (p. 7) | 0.5117 / −0.2363 |
| MnSnIr: ΔHf de MP (eV/átomo) | 0.2945 (p. 7) | 0.2852 en la base principal; 0.2945 en el conjunto experimental |

Trampas que el agente encontró en los datos:

- **Dos versiones del valor de MP.** El conjunto experimental y la base principal no traen
  el mismo ΔHf de MP: difieren en más de 0.01 eV/átomo para 127 de los 824 materiales que
  están en ambos. El texto del artículo cita el del conjunto experimental.
- **Fórmulas dañadas por Excel.** Cuatro fórmulas aparecen como fechas ("2-Feb", "3-Feb",
  "4-Feb").
- **Identificadores `mvc-`.** Hay 2440. La API de MP los convierte sin aviso en otro
  material: `mvc-3470` es YAgO3 en el archivo, pero MP devuelve MgSiO3.
- **Estructuras de hoy, no de 2021.** MP sirve las estructuras actuales, no las de la
  versión V2021.03.22 que usó el artículo.
- **Extrapolación.** El entrenamiento tiene casi solo binarios y ternarios; cerca del 40 %
  de la base principal tiene más de 3 elementos (p. 8–9).

La lección es la misma que en Beer-Lambert: confía, pero compara.
