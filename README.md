# TUPONET Android App — Guide de compilation

## 🚀 Option A : Compiler sur GitHub Actions (GRATUIT, en ligne)

### Étapes :
1. Créez un compte sur https://github.com
2. Créez un nouveau dépôt (repository) : "tuponet-android"
3. Uploadez tous les fichiers de ce projet
4. Créez le fichier `.github/workflows/build.yml` avec ce contenu :

```yaml
name: Build APK
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-java@v3
        with:
          java-version: '17'
          distribution: 'temurin'
      - name: Make gradlew executable
        run: chmod +x gradlew
      - name: Build APK
        run: ./gradlew assembleRelease
      - uses: actions/upload-artifact@v3
        with:
          name: tuponet-apk
          path: app/build/outputs/apk/release/app-release-unsigned.apk
```

5. À chaque push, GitHub compile l'APK automatiquement.
6. Téléchargez l'APK dans l'onglet **Actions > Artifacts**.

---

## 🖥️ Option B : Compiler localement (Windows/Mac/Linux)

### 1. Installer Java JDK 17
- Windows/Mac : https://adoptium.net/
- Linux : `sudo apt install openjdk-17-jdk`

### 2. Installer le SDK Android (sans Android Studio)
```bash
# Télécharger cmdline-tools depuis :
# https://developer.android.com/studio#command-line-tools-only

# Extraire et configurer :
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin

# Installer les composants nécessaires :
sdkmanager "platform-tools" "platforms;android-34" "build-tools;34.0.0"
```

### 3. Compiler l'APK
```bash
cd tuponet-android
chmod +x gradlew        # Linux/Mac seulement
./gradlew assembleDebug # Génère un APK de test

# L'APK se trouve dans :
# app/build/outputs/apk/debug/app-debug.apk
```

---

## 📱 Option C : Compiler sur Android Studio (si installé)

1. File > Open > sélectionnez le dossier `tuponet-android`
2. Build > Build Bundle(s) / APK(s) > Build APK(s)
3. L'APK est dans `app/build/outputs/apk/debug/`

---

## ⚡ Option D : Service en ligne (le plus rapide)

Uploadez ce projet sur **https://appetize.io** ou utilisez
**https://buildozer.io** pour compiler sans rien installer.

---

## 📦 Structure du projet

```
tuponet-android/
├── app/
│   ├── src/main/
│   │   ├── java/com/tuponet/app/
│   │   │   └── MainActivity.java    ← Logique principale
│   │   ├── res/
│   │   │   ├── layout/activity_main.xml
│   │   │   └── values/styles.xml
│   │   └── AndroidManifest.xml
│   ├── build.gradle
│   └── proguard-rules.pro
├── build.gradle
├── settings.gradle
└── gradle/wrapper/gradle-wrapper.properties
```

## 🎯 Fonctionnalités de l'app
- ✅ Charge https://tuponet.com dans une WebView
- ✅ Barre de progression pendant le chargement
- ✅ Bouton retour fonctionne dans le site
- ✅ Thème sombre assorti au site
- ✅ Message si pas de connexion internet
- ✅ JavaScript activé (nécessaire pour le site)
