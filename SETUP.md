# Vocalizzi - Setup Completo

## Passi per Build

### 1. Scarica Modello Piper (OBBLIGATORIO)

**Linux/Mac:**
```bash
cd app/src/main/assets/models
curl -L -O https://github.com/rhasspy/piper/releases/download/v1.2.0/en_US-ryan-high.onnx
```

**Windows:**
```batch
cd app\src\main\assets\models
curl -L -O https://github.com/rhasspy/piper/releases/download/v1.2.0/en_US-ryan-high.onnx
```

Oppure usa:
- Linux/Mac: `./scripts/download_model.sh`
- Windows: `scripts\download_model.bat`

### 2. eSpeak-ng Library (OPZIONALE ma consigliato)

Per phonemization di qualità:

Download precompilato ARM64:
https://github.com/rhasspy/piper-phonemize/releases

Posiziona `libespeak-ng.so` in:
`app/src/main/jniLibs/arm64-v8a/`

**NOTA:** L'app funziona anche senza (usa phonemization semplificata)

### 3. Android Studio

1. Apri Android Studio
2. File → Open → Seleziona cartella Vocalizzi
3. Attendi Gradle sync (può richiedere 5-10 minuti la prima volta)
4. Se errori di sync:
   - File → Invalidate Caches / Restart
   - Tools → SDK Manager → verifica Android SDK 34 installato

### 4. Build APK

**Debug APK:**
```
Build → Build Bundle(s) / APK(s) → Build APK(s)
```

APK in: `app/build/outputs/apk/debug/app-debug.apk`

**Release APK (firmato):**
```
Build → Generate Signed Bundle / APK
```

### 5. Installa su Device

**Via USB:**
```bash
adb install app/build/outputs/apk/debug/app-debug.apk
```

**Via Android Studio:**
Run → Run 'app' (con device connesso)

## Troubleshooting

### Errore "Model not found"
- Verifica che `en_US-ryan-high.onnx` sia in `app/src/main/assets/models/`
- File deve essere esattamente 110MB

### Gradle sync fallito
- Verifica connessione internet
- File → Settings → Build → Gradle → usa Gradle wrapper
- Cancella `.gradle` folder e riprova

### APK troppo grande
- Normale! Con modello è ~120MB
- ProGuard in release riduce a ~115MB

### TTS non funziona
- Controlla logcat per errori ONNX Runtime
- Verifica permessi INTERNET nel Manifest

## File Mancanti da Completare

Questo è un progetto base. Per completarlo aggiungi:

1. **UI Screens** (placeholder esistono, da implementare fully):
   - LibraryScreen.kt
   - ReadingScreen.kt
   - ReviewScreen.kt
   - StatisticsScreen.kt

2. **ViewModels** (struttura base esiste):
   - LibraryViewModel.kt
   - ReadingViewModel.kt  
   - ReviewViewModel.kt

3. **Navigation** (skeleton esiste):
   - VocalizziNavigation.kt con NavHost completo

4. **Repository layer**:
   - TranslationRepository.kt
   - BookRepository.kt

Usa i file già creati come riferimento per lo stile di codifica.

## Risorse Utili

- **Compose Tutorial**: https://developer.android.com/jetpack/compose/tutorial
- **Room Database**: https://developer.android.com/training/data-storage/room
- **Piper Docs**: https://github.com/rhasspy/piper/blob/master/README.md

## Support

Per bug o domande apri issue su GitHub (link al tuo repo quando publichi).

