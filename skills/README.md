# Skills de terceros

## `mattpocock-skills/`

Repositorio de skills de Matt Pocock ([github.com/mattpocock/skills](https://github.com/mattpocock/skills),
licencia MIT), incluido aquí como submódulo de git: es un enlace a su repositorio, no una copia.

El skill que se usa en el curso es **grilling** (parte 3, «Planificar con el agente»):

```
mattpocock-skills/skills/productivity/grilling/SKILL.md
```

El agente te entrevista por rondas antes de escribir código. Cada pregunta trae una respuesta
recomendada, y basta con responder «sí» para aceptarla. Los datos los busca el agente; las
decisiones son tuyas. Termina cuando no queda ninguna decisión abierta.

## Si la carpeta está vacía

Un submódulo no se descarga con un `git clone` normal. Desde la carpeta del repositorio:

```
git submodule update --init
```

O, al clonar, usa `git clone --recursive`.

## Usarlo en opencode

Un skill es una carpeta con un archivo `SKILL.md`. Para instalarlo, copia la carpeta
`grilling/` a donde opencode busca los skills (ver «Instalar una skill» en
[`guia/01-instalacion.md`](../guia/01-instalacion.md)). Después pídele al agente, por ejemplo:
«Usa el skill grilling para planificar este análisis antes de escribir código».
