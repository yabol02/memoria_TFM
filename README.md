# UPM Match - Memoria del TFM

Memoria (en $\LaTeX$) del Trabajo de Fin de Máster **UPM Match: Sistema de Recomendación de Tutores y Colaboraciones**, desarrollado en el marco del Máster Universitario en Aprendizaje Automático y Datos Masivos (MAADM) de la Universidad Politécnica de Madrid.

- **Autor:** Yago Boleas Francisco
- **Tutor:** Carlos Badenes Olmedo
- **Universidad:** Universidad Politécnica de Madrid (UPM)
- **Curso:** 2025-2026

## Resumen

**UPM Match** es un sistema que recomienda tutores de TFG/TFM a partir de una idea descrita en lenguaje libre por el estudiante.
Se construye exclusivamente sobre la actividad pública del profesorado de la UPM: se adquieren y estructuran los datos en un grafo de conocimiento, se enriquece cada perfil con biografías y dominios de especialización mediante modelos de lenguaje ejecutados en local y se indexa con representaciones léxicas (dispersas) y semánticas (densas) para emparejar la consulta con los investigadores más afines.
El trabajo incluye, además, un marco de evaluación reproducible que usa la supervisión histórica como verdad de referencia.

Este repositorio contiene únicamente el código fuente $\LaTeX$ de la memoria.
El código del sistema vive en el repositorio del proyecto: <https://github.com/cbadenes/upm-match>.

---

## Compilación

El documento usa **LaTeX clásico + BibTeX** (estilo `elsarticle-num-names`, citas numéricas con `natbib`) y **glossaries** para la tabla de acrónimos (`makeglossaries`).

### Compilación completa

Genera bibliografía, glosario y resuelve todas las referencias cruzadas:

```bash
pdflatex main.tex
bibtex main
makeglossaries main
pdflatex main.tex
pdflatex main.tex
```

Tras tocar references.bib o añadir citas/referencias cruzadas pdflatex reutiliza la bibliografía ya generada (main.bbl); para incorporar referencias nuevas o resolver [?] / ?? hay que volver a pasar BibTeX y recompilar dos veces:

```bash
bibtex main
pdflatex main.tex
pdflatex main.tex
```

### Sin LaTeX instalado (Docker)
Imagen oficial texlive/texlive. El comando monta el directorio actual, así que funciona en cualquier proyecto sin editar rutas. Ejecútalo desde la carpeta de la memoria:

```shell
# PowerShell (Windows)
docker run --rm -v "${PWD}:/work" -w /work texlive/texlive:latest `
  sh -c 'pdflatex -interaction=nonstopmode main.tex; bibtex main; makeglossaries main; pdflatex -interaction=nonstopmode main.tex; pdflatex -interaction=nonstopmode main.tex'
```

```bash
# Bash (Linux/macOS)
docker run --rm -v "$(pwd):/work" -w /work texlive/texlive:latest \
sh -c 'pdflatex -interaction=nonstopmode main.tex && bibtex main && makeglossaries main && pdflatex -interaction=nonstopmode main.tex && pdflatex -interaction=nonstopmode main.tex'
```

> En Overleaf compila directamente (pdfLaTeX; ejecuta BibTeX y makeglossaries automáticamente), sin necesidad de estos comandos.

## Estructura del proyecto
```bash
.
├── main.tex            # Documento principal (orden de capítulos)
├── settings.tex        # Paquetes, estilos y comandos propios
├── thesisDetails.tex   # Metadatos (título, autor, tutor, año)
├── references.bib      # Bibliografía
├── preliminares/       # Cubierta, portada, resumen, acrónimos…
├── cuerpo/             # Un fichero por capítulo
└── figures/            # Figuras e imágenes
```
El contenido se escribe en cuerpo/ y preliminares/; main.tex solo ordena los capítulos y no debe contener texto.

## Estructura de la memoria
\# | Capítulo | De qué trata
:----------:|:-------------|:-----------
1 | Introducción: la elección de tutor como problema de información | ¿Por qué es necesario este trabajo?
2 | Un problema abierto: por qué la orientación académica sigue artesanal | ¿Por qué no se ha resuelto antes?
3 | Estado del arte: de la recuperación léxica a los modelos de lenguaje | ¿Qué se ha hecho y cómo nos posicionamos?
4 | Aproximación metodológica: del dato público al perfil semántico | ¿Cuál es el flujo? (sin tecnologías)
5 | Marco de evaluación: la supervisión histórica como verdad de referencia | ¿Cómo se mide el rendimiento?
6 | Resultados: arquitectura, prototipo y comparación de estrategias | Tecnologías + demostración + comparación
7 | Discusión: alcance e implicaciones | ¿Qué significan los resultados?
8 | Problemas encontrados y lecciones aprendidas | ¿Qué dificultades surgieron y qué se aprendió?
9 | Conclusiones y líneas futuras | ¿Qué queda demostrado y qué continúa?
A–D | Anexos | Material complementario

## Descargar el PDF

La versión compilada de la memoria se publica automáticamente en cada **release** (la genera un workflow de GitHub Actions a partir del fuente LaTeX).

1. Ve a la sección **[Releases](../../releases)** del repositorio.
2. Abre la release más reciente.
3. En **Assets** (abajo del todo), descarga `UPM-Match-Memoria-<versión>.pdf`.

> Las versiones marcadas como *Pre-release* son borradores en desarrollo; la entrega final será la release sin esa etiqueta.

## Licencia

El texto y las figuras de la memoria son propiedad del autor.
La plantilla base es una adaptación del *UPM Thesis Template* (María Blanco, UPM), distribuida bajo la [LaTeX Project Public License (LPPL)](https://www.latex-project.org/lppl.txt).