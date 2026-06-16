Font Radioactiva
================

Joc Android amb **dos modes** de localització a cegues. A la pantalla d'inici
tries entre **Radioactivity** (a dalt) i **Radar** (a baix). Tots dos col·loquen
un objectiu en un punt aleatori a la distància que demanis i et fan caminar-hi
fins a sobre.

L'app viu sencera dins `app/src/main/assets/radioactivity.html`. La part nativa
(`MainActivity.kt`) només embolcalla aquesta pàgina en un WebView a pantalla
completa i gestiona el permís de localització.

Radioactivity
- Hi ha una **font radioactiva amagada** a prop teu. La pantalla queda negra i et
  guies només per la velocitat dels "clics" d'un comptador Geiger simulat — com
  més ràpid sonen, més a prop ets. Quan arribes salta l'alarma nuclear i l'has de
  desactivar.
- **Distància inicial**: a quina distància es col·loca la font (100–1000 m).
- **Radi d'arribada**: com de prop has d'estar per "trobar-la" (5–30 m).

Radar
- El **radar** ha detectat una **mina** amagada que has de **desactivar**. A la
  pantalla només veus el radar (les ones i el feix que gira) i un **punt** que
  marca on és la mina: com més s'acosta al centre, més a prop ets, i sempre
  apareix en la direcció correcta **segons cap a on mires** (brúixola del
  dispositiu via `deviceorientation`). Cada escombrada sona com un **ping de
  sonar**. En arribar a **5 m** apareix el botó de desactivació amb una **alarma
  de submarí**.
- **Distància inicial**: a quina distància es col·loca la mina (100–1000 m).

Comú als dos modes
- **Vibració de proximitat**: el mòbil vibra més fort com més a prop ets.
- **Historial**: cada partida completada es guarda (data, tipus de joc
  —Radioactivity o Radar—, distància del marcador, distància realment caminada i
  temps utilitzat) i es pot consultar des de la pantalla d'inici o la final. Es
  desa localment al dispositiu.

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
