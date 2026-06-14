Font Radioactiva
================

Joc Android: hi ha una **font radioactiva amagada** a prop teu i l'has de
localitzar a cegues. L'app crea una ruta cap a un punt objectiu situat a una
distància i direcció aleatòries; la pantalla queda negra i et guies només per
la velocitat dels "clics" d'un comptador Geiger simulat — com més ràpid sonen,
més a prop ets. Quan arribes a la font salta l'alarma nuclear i l'has de
desactivar.

El joc viu sencer dins `app/src/main/assets/radioactivity.html`. La part nativa
(`MainActivity.kt`) només embolcalla aquesta pàgina en un WebView a pantalla
completa i gestiona el permís de localització.

Com es juga
- **Distància inicial**: a quina distància es col·loca la font (100–1000 m).
- **Radi d'arribada**: com de prop has d'estar per "trobar-la" (5–30 m).
- **Vibració de proximitat**: el mòbil vibra més fort com més a prop ets.
- **Mode de prova**: mostra la distància a la pantalla (per validar).
- **Mode simulació**: juga sense GPS movent un control lliscant (per provar a casa).

Tecnologia
- Geolocalització via HTML5 Geolocation API (`navigator.geolocation`) dins el WebView.
- So del Geiger i sirena generats amb la Web Audio API.
- `navigator.wakeLock` manté la pantalla encesa durant la cerca.
- Sense mapa, sense xarxa: el joc funciona offline (només cal el permís de localització).

Run
- Obre la carpeta a Android Studio, deixa sincronitzar Gradle i executa-ho en un dispositiu.
- Recomanat un dispositiu físic a l'aire lliure per al GPS; per provar dins de casa, fes servir el **Mode simulació**.

GitHub Actions
- `.github/workflows/android-apk.yml` compila un APK de depuració.
- Cada execució puja `app/build/outputs/apk/debug/app-debug.apk` com a artefacte `app-debug-apk`.
- Més detalls a `docs/github-actions-apk.md`.

Build per terminal
- `./gradlew assembleDebug` genera l'APK a `app/build/outputs/apk/debug/app-debug.apk`.
- Defineix `ANDROID_HOME` o `ANDROID_SDK_ROOT` apuntant al teu Android SDK abans de compilar.
