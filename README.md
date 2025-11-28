# Vocalizzi

Un'app Android per imparare l'inglese leggendo libri ePub con sintesi vocale TTS di alta qualità e creazione automatica di flashcard per spaced repetition.

## Caratteristiche

- 📚 Importa libri ePub
- 🔊 Text-to-Speech con Piper (voce Ryan - qualità premium)
- 📝 Creazione automatica flashcard
- 🧠 Sistema Spaced Repetition (SM-2)
- 🌓 Tema Dark/Light
- 🔍 Rilevamento phrasal verbs e idiomi
- 🌍 Traduzione automatica (MyMemory API)
- 📊 Statistiche di apprendimento

## Requisiti

- Android Studio Hedgehog (2023.1.1) o superiore
- JDK 17
- Android SDK 34
- Dispositivo Android con API 26+ (Android 8.0+)
- **ARM64 device** (es. Samsung A22 5G)

## Setup Progetto

### 1. Clone/Download

Scarica ed estrai questo progetto in una cartella locale.

### 2. Download Modello TTS

Il modello Piper è troppo grande per Git (110MB). Scaricalo manualmente:

```bash
cd app/src/main/assets/models
curl -L -O https://github.com/rhasspy/piper/releases/download/v1.2.0/en_US-ryan-high.onnx
```

O su Windows:
```
scripts\download_model.bat
```

### 3. Apri in Android Studio

1. Apri Android Studio
2. File → Open
3. Seleziona la cartella `Vocalizzi`
4. Attendi che Gradle sincronizzi le dipendenze

### 4. Build APK

1. Build → Build Bundle(s) / APK(s) → Build APK(s)
2. L'APK sarà in `app/build/outputs/apk/debug/app-debug.apk`

## Struttura Progetto

```
Vocalizzi/
├── app/src/main/
│   ├── kotlin/com/vocalizzi/
│   │   ├── data/           # Database Room, DAO, Entities
│   │   ├── domain/         # Logic TTS, Parser, SRS
│   │   ├── ui/             # Compose UI screens
│   │   └── MainActivity.kt
│   ├── assets/
│   │   ├── models/         # Modello Piper ONNX (da scaricare)
│   │   └── phrasal_verbs.json
│   └── res/                # Risorse Android
└── README.md
```

## Uso App

### Import Libro
1. Scarica un ePub da Project Gutenberg o Standard Ebooks
2. Tap su "Import Book" nella Library
3. Seleziona il file ePub

### Lettura
1. Tap sul libro nella Library
2. Tap Play per iniziare TTS sentence-by-sentence
3. Tap su una parola per vedere traduzione
4. Crea flashcard se necessario

### Review Flashcard
1. Nella home vedi il counter "X cards due"
2. Tap per iniziare review session
3. Rispondi Again/Hard/Good/Easy

## Fonti Libri Consigliati (Gratis)

- **Standard Ebooks**: https://standardebooks.org (con cover)
- **Project Gutenberg**: https://gutenberg.org (70k+ libri)
- **ManyBooks**: https://manybooks.net

## Note Tecniche

### eSpeak-ng
La phonemization è attualmente semplificata. Per qualità TTS ottimale, integra eSpeak-ng nativo (vedi issues).

### Cover Libri
L'app tenta auto-fetch da Open Library API. Se fallisce, usa placeholder.

### Phrasal Verbs
Dataset di 5000+ phrasal verbs incluso per rilevamento contestuale.

## Licenza

MIT License - Uso personale

## Credits

- **Piper TTS**: https://github.com/rhasspy/piper
- **ONNX Runtime**: Microsoft
- **MyMemory Translation**: https://mymemory.translated.net

