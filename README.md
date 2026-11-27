# Organigramme des Ministeriums fuer drakonische Sicherheit

[![PDFs](https://github.com/wy-bbw/df_docs/actions/workflows/build.yml/badge.svg?branch=master)](https://github.com/wy-bbw/df_docs/actions/workflows/build.yml)

## Bauen

Die PDFs werden mit `lualatex` gebaut, nicht mit `pdflatex`. Die Schrift wird ueber
`fontspec` geladen, und das geht nur mit LuaLaTeX (oder XeLaTeX).

`lualatex` muss im jeweiligen Ordner aufgerufen werden, weil die gemeinsame Stildatei
ueber einen relativen Pfad eingebunden wird:

```sh
(cd ministerium_organigramm && lualatex organigramm.tex)
(cd neue_polizei_organigramm && lualatex organigramm.tex)
```

Die `organigramm.dot`-Dateien sind die aeltere Graphviz-Fassung. Ein
`dot -Tpdf organigramm.dot -o organigramm.pdf` ueberschreibt das PDF aus TeX.

## Automatischer Bau

GitHub Actions (`.github/workflows/build.yml`) baut beide PDFs bei jedem Push auf
`master` und bei jedem Pull Request. Die PDFs haengen als Artefakt `organigramme` am
jeweiligen Lauf im Actions-Tab und werden nach 90 Tagen geloescht.

Ein Tag der Form `vX.Y` veroeffentlicht die PDFs dauerhaft als GitHub Release:

```sh
git tag v1.0
git push origin v1.0
```

Die neueste Fassung liegt immer unter
`https://github.com/wy-bbw/df_docs/releases/latest/download/organigramm_ministerium.pdf`
bzw. `.../organigramm_abt13.pdf`.

## Aufbau

`ministerium_stil.tex` enthaelt alles, was beide Organigramme gemeinsam haben:
Seitenformat (A3 quer), Schrift, Silbentrennung, Farben, die Linienstile, den
Leitungskasten und das Wappen (`\wappen{(x,y)}`). Beide `organigramm.tex` binden sie
direkt nach `\documentclass` mit `\input{../ministerium_stil}` ein.

Was nur ein Organigramm braucht, steht in dessen eigener Datei:

- `ministerium_organigramm/organigramm.tex`: Abteilungsspalten mit `\abteilung` und
  nummerierten Referaten mit `\referat`
- `neue_polizei_organigramm/organigramm.tex`: Abteilung 13 mit `\spalte`, `\einheit`
  und `\referat` sowie den M/P-Marken fuer die magische und profane Leitung
