Font Radioactiva
================

Joc Android amb **tres modes** de localització a cegues. A la pantalla d'inici
tries entre **Radioactivity**, **Radar** i **Lidar**. Tots tres col·loquen
un objectiu en un punt aleatori a la distància que demanis i et fan caminar-hi
fins a sobre.

L'app viu sencera dins `app/src/main/assets/radioactivity.html`. La part nativa
(`MainActivity.kt`) només embolcalla aquesta pàgina en un WebView a pantalla
completa i gestiona el permís de localització.

Radioactivity
- Hi ha una **font radioactiva amagada** a prop teu. La pantalla queda negra i et
  guies per la velocitat dels "clics" d'un comptador Geiger simulat — com més
  ràpid sonen, més a prop ets — i per una **boira verda** que apareix a la vora o
  cantonada **en la direcció de la font** (segons cap a on mires, via la brúixola
  del dispositiu) i que s'intensifica a mesura que t'hi acostes. Quan arribes
  salta l'alarma nuclear i l'has de desactivar.
- **Distància inicial**: a quina distància es col·loca la font (100–1000 m).
- **Radi d'arribada**: com de prop has d'estar per "trobar-la" (5–30 m).
- El marcador s'**ajusta al carrer o plaça caminable més proper** (servei
  `nearest` d'OSRM, perfil a peu) perquè el punt sigui sempre accessible. Si no
  hi ha xarxa, es manté el punt aleatori original.

Radar
- El **radar** ha detectat una **mina** amagada que has de **desactivar**. A la
  pantalla només veus el radar (les ones i el feix que gira) i un **punt** que
  marca on és la mina: la mina és el **punt fix del terreny** i el radar **gira
  amb tu**, de manera que el punt apareix **a dalt de tot** quan mires cap a ella
  i es reubica si gires o et desvies cap a un costat (brúixola del dispositiu via
  `deviceorientation`). Com més s'acosta al centre, més a prop ets. Cada escombrada sona com un **ping de
  sonar**. En arribar a **5 m** apareix el botó de desactivació amb una **alarma
  de submarí**.
- **Distància inicial**: a quina distància es col·loca la mina (100–1000 m).

Lidar
- El **lidar** dispara **polsos de llum** (un **flaix**) i, amb el rebot, dibuixa
  el que té al davant. És l'eina ideal per caçar un **dron espia** furtiu que vola
  en silenci: és l'objecte que millor lliga amb el lidar, perquè es localitza pel
  reflex dels polsos i s'ha de **desactivar**. A cada flaix la pantalla
  s'il·lumina un instant i apareixen **una o dues petjades** que apunten cap on és
  el dron **segons cap a on mires** (brúixola via `deviceorientation`). **Dues
  petjades** = encara queda camí; **una petjada** = ja ets molt a prop. En arribar
  a **5 m** apareix el botó de desactivació.
- **Distància inicial**: a quina distància es col·loca el dron (100–1000 m).
- **Flaix cada**: cada quants segons es dispara el pols de llum (1–10 s).
- Com a Radioactivity, el dron s'**ajusta al carrer o plaça caminable més proper**.

Comú als tres modes
- **Vibració de proximitat**: el mòbil vibra més fort com més a prop ets.
- **Historial**: cada partida completada es guarda (data, tipus de joc
  —Radioactivity, Radar o Lidar—, distància del marcador, distància caminada i
  temps utilitzat) i es pot consultar des de la pantalla d'inici o la final. Es
  desa localment al dispositiu.
- **Distància caminada**: es calcula **en relació a l'objectiu**, sumant tot el
  que t'hi has anat **apropant i allunyant** (canvis de la distància al marcador),
  per donar una xifra precisa i estable enfront del soroll del GPS.

Tecnologia
- Geolocalització via HTML5 Geolocation API (`navigator.geolocation`) dins el WebView.
- So del Geiger, sirena, sonar i pols de lidar generats amb la Web Audio API.
- `navigator.wakeLock` manté la pantalla encesa durant la cerca.
- Per situar el marcador en un carrer o plaça (Radioactivity i Lidar) es consulta
  el servei públic `nearest` d'OSRM. És l'única crida de xarxa i és **opcional**:
  si falla, s'utilitza el punt aleatori original i el joc continua funcionant
  offline (només cal el permís de localització).

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
