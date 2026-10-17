# PGE_MAKER — generator opracowań projektu linii nN ze światłowodem

Z jednego pliku **planu DXF** program tworzy komplet opracowań projektu linii nN
z projektowanym światłowodem. Okno ma osobną zakładkę dla każdego modułu:

| Moduł | Co tworzy |
|---|---|
| **Numeracja słupów** | automatyczna numeracja słupów nN → `<plan> - ponumerowane.dxf` (wymaga `ezdxf`) |
| **Przewieszenia** | rysunki zwisów przęseł → `<plan> - przewieszenia.dxf` + kopia kontrolna |
| **Zestawienie** | zestawienie słupów nN per stacja trafo → `.xlsx` |
| **Obliczenia** | obliczenia nośności słupów → `.xlsx` (z zestawienia albo własnego pliku) |
| **Rysunki stałe** | plan orientacyjny DXF per stacja + zestawienie (opcjonalny podkład mapowy) |
| **Arkusze PZT** | arkusze A3 1:1000 per stacja (nr stacji i miejscowości wg zasięgu / WT) |
| **Opisy techniczne** | opis `.docx` per stacja z szablonu Word |
| **PPW** | zbiorczy opis `.docx` dla całego projektu + renumeracja numerów rysunku w DXF |

Rdzeń działa na samym Pythonie (biblioteka standardowa + `tkinter`). Biblioteki
zewnętrzne są **opcjonalne** i dotyczą wybranych modułów (patrz `requirements.txt`):
`Pillow` (podkład mapowy w rysunkach stałych), `python-docx` + `openpyxl`
(opisy techniczne i PPW), `ezdxf` (zapis numeracji słupów).

## Uruchomienie (Windows)

- `setup.bat` — sprawdza Pythona i `tkinter` (oraz opcjonalnie instaluje PyInstaller),
- `uruchom.bat` — otwiera **okno** programu,
- `generuj.bat "plan.dxf"` — wersja **wiersza poleceń** (można przeciągnąć plik DXF na `.bat`).

Pliki `.bat` obsługują polskie znaki (`chcp 65001`) i same wykrywają Pythona (`py -3` lub `python`).

## Uruchomienie (dowolny system)

```bash
python -m generator            # okno programu  (albo: python generator_gui.py)
python -m generator.pipeline "plan.dxf"            # cały łańcuch (wiersz poleceń)
python generator_cli.py "plan.dxf" --tylko zestawienie,obliczenia -o wyniki
```

## Program dla Windows (.exe)

Plik `PGE_MAKER.exe` jest budowany automatycznie przez GitHub Actions po każdej zmianie
kodu (zakładka **Releases**). Wbudowane są wszystkie szablony — nie trzeba niczego instalować.

## Pliki programu

```
generator_gui.py        – start okna
generator_cli.py        – start wiersza poleceń
generator/              – kod programu (pipeline, moduły, własny czytnik/zapis DXF bez CAD-a)
  numeruj_slupy/        – automatyczna numeracja słupów nN (wymaga ezdxf)
przewieszenia baza.dxf, arkusze.dxf, szablon.dxf, orientacja.png,
szablon_opisu.docx, PPW miński szablon.docx, wzorce/  – wbudowane szablony/zasoby
```
