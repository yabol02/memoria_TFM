# UPM Match - Memoria del Trabajo de Fin de Máster

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

## Compilación

La memoria usa $\LaTeX$ clásico con BibTeX (estilo `elsarticle-num-names`) y `makeglossaries` para la tabla de acrónimos. Desde la raíz del repositorio:

```bash
pdflatex main.tex
bibtex main
makeglossaries main
pdflatex main.tex
pdflatex main.tex
```

El resultado es `main.pdf`. También compila sin cambios en **Overleaf**.

> Si tras compilar aparecen referencias `??` o citas `[?]`, ejecuta una pasada adicional de `pdflatex main.tex` (suele ocurrir en la primera compilación, cuando aún no existen los ficheros auxiliares).

### Con Docker (sin LaTeX local)

```bash
docker run --rm -v "$PWD:/work" -w /work texlive/texlive:latest \
  sh -c 'pdflatex -interaction=nonstopmode main.tex; bibtex main; makeglossaries main; pdflatex -interaction=nonstopmode main.tex; pdflatex -interaction=nonstopmode main.tex'
```

## Estructura del repositorio

```
.
├── main.tex            # Documento principal (orden de capítulos)
├── settings.tex        # Paquetes, estilos y comandos propios
├── thesisDetails.tex   # Metadatos (título, autor, tutor, año)
├── references.bib      # Bibliografía
├── preliminares/       # Cubierta, portada, resumen, acrónimos…
├── cuerpo/             # Un fichero por capítulo
└── figures/            # Figuras e imágenes
```

## Descargar el PDF

La versión compilada de la memoria se publica automáticamente en cada **release** (la genera un workflow de GitHub Actions a partir del fuente LaTeX).

1. Ve a la sección **[Releases](../../releases)** del repositorio.
2. Abre la release más reciente.
3. En **Assets** (abajo del todo), descarga `UPM-Match-Memoria-<versión>.pdf`.

> Las versiones marcadas como *Pre-release* son borradores en desarrollo; la entrega final será la release sin esa etiqueta.

## Licencia

El texto y las figuras de la memoria son propiedad del autor.
La plantilla base es una adaptación del *UPM Thesis Template* (María Blanco, UPM), distribuida bajo la [LaTeX Project Public License (LPPL)](https://www.latex-project.org/lppl.txt).