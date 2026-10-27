# MUV 360

APK dell'app **MUV 360**, la postazione VR del Museo della civiltà villanoviana (MUV): il Visitatore indossa un Meta Quest 3S e guarda un Film a 360° sul villaggio villanoviano, con una schermata Home e una finale (Outro).

Qui si pubblica solo l'APK. Gli APK si scaricano dalla pagina [Releases](../../releases).

## Contenuto dell'APK

- Dispositivo: Meta Quest 3S (OpenXR), Android arm64.
- Package: `io.ispira.muv360`.
- Build Release firmata, non debuggable.
- Nessun Platform SDK né Insight SDK Meta (niente passthrough, scene o ancore spaziali).

## Installazione sul visore

1. Scarica `MUV360-<versione>.apk` dall'ultima release.
2. Installalo con `adb install -r MUV360-<versione>.apk` (modalità sviluppatore attiva sul Quest).
3. Copia il Film sul visore, fuori dall'APK:

   ```
   adb shell mkdir -p /sdcard/MUV
   adb push film.mp4 /sdcard/MUV/film.mp4
   ```

   Il Film deve essere un video equirettangolare mono **H.265/HEVC Main 8 bit, 5760×2880, 30 fps, tag `hvc1`, audio AAC stereo**, circa 50 Mb/s di media (picchi fino a 80 Mb/s), circa 2 GB per 5 minuti. Se manca, l'app mostra "Film non trovato: /sdcard/MUV/film.mp4".

   Anche copia e incolla da Esplora file va bene (`Quest 3S > Archivio condiviso interno > MUV`), purché il file si chiami esattamente `film.mp4`.

   Il lettore video di sistema del visore mostra questo formato nero: per controllare il Film usa l'app.

4. Al primo avvio accetta il permesso di accesso ai video, che serve all'app per leggere il Film. In alternativa:

   ```
   adb shell pm grant io.ispira.muv360 android.permission.READ_MEDIA_VIDEO
   ```

5. Accendi i controller prima di avviare l'app: il visore lo richiede.

Gli aggiornamenti si installano sopra la versione precedente (`adb install -r`) perché tutti gli APK sono firmati con la stessa chiave e hanno un `versionCode` crescente.

## Verifica del file

L'hash SHA-256 di ogni APK è nelle note della release.
