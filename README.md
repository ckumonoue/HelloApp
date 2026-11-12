# HelloApp

Materiał M01 – Android, start (Java). Aplikacja z jednym ekranem: nagłówek „Sklep 4A”, krótki opis i przycisk „Start”, który pokazuje Toast „Wkrótce”.

## Technologie

- Java 11 (kod aplikacji), widoki XML (*Empty Views Activity*)
- Android Gradle Plugin 9.4.0, Gradle 9.6.0
- `minSdk` 26 (Android 8.0), `compileSdk`/`targetSdk` 37
- Android Studio Rabbit 2 (2026.2.2)
- `applicationId`: `com.ckumonoue.helloapp`

## Uruchomienie

1. Otwórz folder projektu w Android Studio (*File → Open*).
2. Poczekaj na Gradle sync (pierwszy raz kilka minut, potrzebny internet).
3. Wybierz emulator lub telefon z włączonym debugowaniem USB i kliknij ▶ (`Shift + F10`).

## Zadanie 2 – uruchomienie

Zrzut ekranu z uruchomionej aplikacji: **Słaby computer**.

## Zadanie 3 – mapa plików

| Plik | Za co odpowiada | Odpowiednik w Django |
|---|---|---|
| `MainActivity.java` | klasa ekranu: wczytuje layout, obsługuje kliknięcia | `views.py` |
| `res/layout/activity_main.xml` | wygląd ekranu: co, gdzie i jakiego rozmiaru | `templates/index.html` |
| `AndroidManifest.xml` | nazwa, ikona, lista ekranów, uprawnienia, ekran startowy | `settings.py` + `urls.py` |
| `res/values/strings.xml` | wszystkie teksty aplikacji (tłumaczenie = drugi plik w `values-en/`) | – (pliki tłumaczeń `locale/`) |
| `app/build.gradle.kts` | zależności, `minSdk`, `targetSdk`, wersja aplikacji | `requirements.txt` |
| `res/` | zasoby: layouty, teksty, kolory, ikony; każdy dostaje stałą w klasie `R` | `static/` |
| `gradle/libs.versions.toml` | wersje bibliotek w jednym miejscu | `requirements.txt` (wersje) |
| `.gitignore` | pliki, które nie idą do Gita (`build/`, `local.properties`) | `.gitignore` |

## Zadanie 4 – teksty i tłumaczenie

Wszystkie teksty są w `res/values/strings.xml` (polski, domyślny). Angielskie tłumaczenie jest w `res/values-en/strings.xml` (te same `name`, inne wartości). Po zmianie języka emulatora na angielski (*Settings → System → Languages*) aplikacja wyświetla się po angielsku bez zmian w kodzie.

## Zadanie 5 – przycisk i licznik

Wersja z licznikiem (przyciski „Kliknij mnie” i „Reset”) jest w historii Gita w commitach `feat: add greeting text and click counter` oraz `feat: add Log.d logging`. W commicie `feat: add shop home screen` ekran został zamieniony na ekran sklepu (zadanie 6).

## Zadanie 7 – Logcat

`Log.d` z tagiem `MainActivity` jest w `onCreate` i w obsłudze kliknięcia. W Logcat filtr: `tag:MainActivity` (albo `package:mine`).

Celowy błąd: `findViewById` wywołane **przed** `setContentView` zwraca `null`, więc pierwsze użycie takiego pola kończy się `NullPointerException` i zamknięciem aplikacji. Stack trace: **Słaby computer**.

Jedna linia o tym, która linia kodu zawiniła: **Słaby computer** (to ta linia `MainActivity.java`, w której wywołano metodę na polu `null`).

## Zadanie 8 – obrót ekranu

Po obróceniu emulatora (zrobione na wersji z licznikiem) licznik wraca do zera, bo obrót niszczy Activity i tworzy je od nowa, więc `onCreate` wykonuje się drugi raz, a pole `clickCount` dostaje wartość początkową 0 (pełne wyjaśnienie cyklu życia – materiał M02).
