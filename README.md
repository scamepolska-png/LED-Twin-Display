# LED Twin Display — Android project

## Co robi ta wersja
- aplikacja Android (Kotlin + Jetpack Compose),
- skanowanie paneli BLE,
- wybór panelu lewego i prawego,
- edycja komunikatu i koloru,
- bufor logiczny 128×16 dzielony na dwa obrazy 64×16,
- wysyłanie obrazu do dwóch niezależnych paneli,
- workflow GitHub Actions do zbudowania instalacyjnego APK.

## Ważne: status
To jest **projekt prototypowy, nie gotowy i przetestowany APK**. W tym środowisku nie ma Android SDK ani Gradle, więc nie mogę uczciwie przekazać skompilowanego pliku instalacyjnego. Dołączony workflow buduje debug APK po umieszczeniu projektu w repozytorium GitHub.

Protokół iPixel Color został odtworzony niezależnie. Repozytorium `mx2rel/BK-Light-LED-rx-engine` opisuje komendę pełnej klatki 64×16: 9-bajtowy nagłówek `09 0C 00 00 00 00 0C 00 00` oraz 3072 bajty RGB. Inny projekt GifPack deklaruje potwierdzoną obsługę iPixel Color 64×16 (typ urządzenia 0x83). To są mocne przesłanki zgodności, ale **nie jest to test na konkretnych dwóch egzemplarzach ACT1033**.

## Jak uzyskać APK
1. Rozpakuj ZIP.
2. Utwórz prywatne lub publiczne repozytorium na GitHub.
3. Wgraj zawartość folderu `LEDTwinDisplay` do repozytorium (gałąź `main`).
4. Otwórz zakładkę **Actions** i uruchom workflow **Build Android APK**.
5. Po zakończeniu otwórz wynikowy run i pobierz artefakt `LED-Twin-debug-APK`.
6. Rozpakuj artefakt na telefonie i zainstaluj `app-debug.apk`. Android może poprosić o zgodę na instalację z tej przeglądarki/pliku.

## Ograniczenia pierwszego prototypu
- Wysyłanie pełnej klatki jest eksperymentalne; dokładne UUID, handshake, rozmiar MTU i tempo fragmentacji muszą być zweryfikowane na panelach.
- Wysyłanie do dwóch paneli może wymagać korekty kolejności i opóźnień po pierwszym teście.
- To wydanie nie zawiera jeszcze importu GIF ani pełnego edytora osi czasu. Najpierw trzeba potwierdzić stabilną transmisję do obu urządzeń.
- Android i firmware paneli mogą ograniczać równoległe połączenia BLE.

## Wymagania do lokalnego builda
JDK 17, Android SDK 35 i Gradle 8.9. Otwórz projekt w Android Studio i uruchom `:app:assembleDebug`.

## Źródła protokołu
- https://github.com/mx2rel/BK-Light-LED-rx-engine
- https://github.com/PeterkoCZ91/iledcolor-backpack
