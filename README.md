# Gąbka Mengera – Projekt M-I

Projekt na zajęcia z wizualizacji. Gąbka Mengera w 3D, działa w przeglądarce, jeden plik HTML.

## Jak uruchomić

Otwórz `menger.html` w przeglądarce. Tyle. Nic nie trzeba instalować.

## Co to w ogóle jest

Gąbka Mengera to fraktal 3D. Bierzesz sześcian, dzielisz na 27 mniejszych, wycinasz 7 środkowych, i to samo robisz dla każdego z pozostałych 20. I tak w kółko.

Po każdej iteracji masz 20x więcej sześcianów:
- poziom 0 → 1 kostka
- poziom 1 → 20 kostek
- poziom 2 → 400
- poziom 3 → 8 000
- poziom 4 → 160 000 (tu już przeglądarka trochę się dusi)

## Sterowanie

| Co | Jak |
|---|---|
| Obrót | Przeciągnij myszką |
| Poziom rekurencji | Suwak "Poziom" |
| Zoom | Suwak "Zoom" |
| Animacja budowania | ▶ Buduj |
| Zatrzymanie | ⏸ Stop |
| Jeden krok | ⊞ Krok |
| Reset | ↺ Reset |

Suwak prędkości działa dwutrybowo — przy niskich wartościach dodaje jedną kostkę co kilka klatek (widać każdą z osobna), przy wysokich dodaje ich dużo na raz.

## Technologie

Czysty JavaScript + HTML5 Canvas. Zero bibliotek, zero frameworków. Cała logika — generowanie, obrót 3D, rzutowanie, rysowanie — napisana ręcznie.

## Struktura kodu

Kod podzielony na sekcje komentarzami:

- **Generowanie** – rekurencyjna funkcja `generujKostki()`, warunek usunięcia w `czyUsunac()`
- **Projekcja** – `obrocPunkt()` (macierze rotacji) + `rzutuj()` (perspektywa)
- **Rysowanie** – algorytm malarza, sortowanie ścian po głębokości
- **Animacja** – `requestAnimationFrame`, dwie prędkości
- **UI** – obsługa myszy, suwaki, przyciski

## Znane problemy

Poziom 4 działa ale obrót myszką przestaje być płynny — canvas 2D nie ma Z-bufora więc wszystko liczymy na CPU. Na WebGL działałoby lepiej ale to już inny projekt.

Algorytm malarza przy pewnych kątach może lekko błędnie posortować ściany — sporadycznie widać mały artefakt. Przy normalnym użytkowaniu praktycznie niezauważalne.