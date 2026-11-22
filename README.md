# Organigramme des Ministeriums fuer drakonische Sicherheit

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
