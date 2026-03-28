# TactileText Installation Guide 🚀

Complete step-by-step instructions for setting up the TactileText project on your local machine.

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [Flutter & Dart Setup](#flutter--dart-setup)
- [Project Setup](#project-setup)
- [Android Setup](#android-setup)
- [iOS Setup](#ios-setup)
- [Azure Services Configuration](#azure-services-configuration)
- [Hardware Setup](#hardware-setup)
- [Running the Application](#running-the-application)
- [Troubleshooting](#troubleshooting)

---

## 📋 Prerequisites

### System Requirements

- **Windows, macOS, or Linux** operational system
- **8 GB RAM** minimum (16 GB recommended)
- **10 GB free disk space**
- **Internet connection** for downloading dependencies

### Software Requirements

- **Git**: [Download Git](https://git-scm.com/)
- **Flutter SDK**: [Download Flutter](https://flutter.dev/docs/get-started/install)
- **Dart SDK**: Comes bundled with Flutter
- **IDE**: VS Code or Android Studio

---

## 🔧 Flutter & Dart Setup

### Step 1: Install Flutter

#### Windows

1. Download Flutter SDK from https://flutter.dev/docs/get-started/install/windows
2. Extract to a location (e.g., `C:\flutter`)
3. Add Flutter to PATH:
   - Open Environment Variables
   - Add `C:\flutter\bin` to PATH
4. Verify installation:
   ```bash
   flutter --version
   dart --version
   ```

#### macOS

```bash
# Using Homebrew (recommended)
brew install flutter

# Or download manually from https://flutter.dev/docs/get-started/install/macos
# Then add to ~/.zshrc or ~/.bash_profile:
export PATH="$PATH:[/path/to/flutter]/bin"

flutter --version
```

#### Linux

```bash
# Download Flutter
mkdir ~/development
cd ~/development
git clone https://github.com/flutter/flutter.git

# Add to PATH in ~/.bashrc or ~/.zshrc
export PATH="$PATH:~/development/flutter/bin"

flutter --version
```

### Step 2: Run Flutter Doctor

```bash
flutter doctor
```

This checks your environment and displays status. Address any warnings.

### Step 3: Accept Licenses

```bash
flutter doctor --android-licenses
```

---

## 📦 Project Setup

### Step 1: Clone Repository

```bash
git clone https://github.com/yourusername/TactileText.git
cd TactileText
```

### Step 2: Get Dependencies

```bash
flutter pub get
```

### Step 3: Generate Build Files (if needed)

```bash
flutter pub pub run build_runner build
```

### Step 4: Verify Project

```bash
flutter analyze
```

---

## 🤖 Android Setup

### Requirements

- **Android SDK 21+** (API level)
- **Android Studio** or **Android Command Line Tools**

### Setup Steps

1. **Install Java Development Kit (JDK)**
   ```bash
   # Windows - using Chocolatey
   choco install openjdk

   # macOS
   brew install openjdk
   ```

2. **Configure Android SDK**
   - Open Android Studio
   - Go to SDK Manager
   - Install Android SDK 21-33
   - Install Build-tools 33.0.0

3. **Accept Android Licenses**
   ```bash
   flutter doctor --android-licenses
   ```

4. **Configure gradle** (if needed)
   - Edit `android/local.properties`
   - Add: `sdk.dir=/path/to/android/sdk`

### Building for Android

```bash
# Debug build
flutter build apk

# Release build
flutter build apk --release

# Install on connected device
flutter install

# Run with logging
flutter run -v
```

---

## 🍎 iOS Setup

### Requirements

- **macOS 10.15+**
- **Xcode 12.0+**
- **CocoaPods**

### Setup Steps

1. **Install Xcode Command Line Tools**
   ```bash
   xcode-select --install
   ```

2. **Install CocoaPods**
   ```bash
   sudo gem install cocoapods
   ```

3. **Configure Podfile**
   ```bash
   cd ios
   pod deintegrate
   pod install
   cd ..
   ```

4. **Check iOS Setup**
   ```bash
   flutter doctor -v
   ```

### Building for iOS

```bash
# Build for iOS
flutter build ios

# Build and run on simulator
flutter run -d "iPhone 14 Pro"

# Build for physical device
flutter run -d [device-id]

# Get device list
flutter devices
```

---

## ☁️ Azure Services Configuration

### Step 1: Create Azure Account

1. Go to [Azure Portal](https://portal.azure.com)
2. Create a free account or sign in
3. Verify payment method (free tier available)

### Step 2: Create Cognitive Services Resource

1. **Search for "Cognitive Services"**
2. **Click "Create"**
3. **Select "Multi-service account"** (for all services)
4. **Configure:**
   - Subscription: Your subscription
   - Resource group: Create new
   - Region: Closest to your location
   - Name: `tactiltext-services`
   - Pricing tier: `Free (F0)` or `Standard (S0)`
5. **Review and Create**

### Step 3: Get API Keys

1. Go to created resource
2. **Left panel → Keys and Endpoint**
3. Copy:
   - **Key 1** or **Key 2**
   - **Endpoint**

### Step 4: Configure in App

Create/update `lib/config/azure_config.dart`:

```dart
class AzureConfig {
  static const String API_KEY = 'YOUR_API_KEY_HERE';
  static const String ENDPOINT = 'https://REGION.tts.speech.microsoft.com';
  static const String REGION = 'your-region'; // e.g., 'eastus'
}
```

**⚠️ Security Note:** Never commit API keys. Use environment variables:

```bash
export AZURE_API_KEY='your-key'
export AZURE_ENDPOINT='your-endpoint'
export AZURE_REGION='your-region'
```

### Step 5: Test Configuration

```bash
flutter run -v
# Watch logs for Azure connection confirmation
```

---

## 🖨️ Hardware Setup

### Components Needed

- Arduino Uno microcontroller
- Bluetooth module (HC-05 or HC-06)
- 6 Electromagnetic actuators (solenoids)
- Darlington transistor array (ULN2803)
- Resistors, capacitors, wiring
- 12V power supply

### Wiring Diagram

```
Arduino Uno
├── GND ──────────┐
├── +5V ──────┐   │
│             │   │
│    HC-05    │   │
│  Bluetooth  │   │
│  Rx ← TX1   │   │
│  Tx → RX1   │   │
│  GND ───────┴───┤
│                 │
│  ULN2803        │
│  In1-6 ← Pin 2-7│
│  Common ────────┘
│
├── Actuators
│  Pin2 → Dot 1 (TL)
│  Pin3 → Dot 2 (TC)
│  Pin4 → Dot 3 (TR)
│  Pin5 → Dot 4 (BL)
│  Pin6 → Dot 5 (BC)
│  Pin7 → Dot 6 (BR)
```

### Arduino Code Setup

1. Download [Arduino IDE](https://www.arduino.cc/en/software)
2. Load firmware to Arduino:
   - Connect Arduino via USB
   - Select board: Tools → Board → Arduino Uno
   - Select port: Tools → Port → COM* (Windows) or /dev/cu.* (Mac)
   - Upload provided firmware

### Pairing Bluetooth Module

1. HC-05 comes pre-configured (usually)
2. Pair with your device:
   - **Windows**: Settings → Devices → Add Bluetooth device
   - **macOS**: System Preferences → Bluetooth
   - **Android**: Settings → Bluetooth → Pair new device
   - **iOS**: Settings → Bluetooth

Default PIN (if needed): `1234` or `0000`

---

## ▶️ Running the Application

### First Run

```bash
# Get dependencies (if not done)
flutter pub get

# Run the app
flutter run

# Run on specific device
flutter run -d "device-id"

# Run with verbose logging
flutter run -v
```

### Using Emulator/Simulator

```bash
# Android Emulator
flutter emulators
flutter emulators launch <emulator_name>
flutter run

# iOS Simulator  
open -a Simulator
flutter run
```

---

## 🔍 Troubleshooting

### Flutter Issues

**Problem: `flutter` command not found**
```bash
# Solution: Add Flutter to PATH
export PATH="$PATH:[path-to-flutter]/bin"
```

**Problem: Outdated dependencies**
```bash
flutter clean
flutter pub get
```

**Problem: Build fails**
```bash
flutter clean
rm -rf build/
flutter pub get
flutter pub pub run build_runner build --delete-conflicting-outputs
```

### Android Issues

**Problem: Android SDK not found**
```bash
# Set ANDROID_HOME
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools
```

**Problem: Gradle sync issues**
```bash
cd android
./gradlew clean
cd ..
flutter clean
flutter pub get
```

### iOS Issues

**Problem: Pod dependency issues**
```bash
cd ios
pod repo update
pod install
cd ..
flutter clean
```

**Problem: Code signing issues**
- Open `ios/Runner.xcworkspace` in Xcode
- Select Runner → Signing & Capabilities
- Select your team

### Bluetooth Issues

**Problem: Bluetooth not connecting**
- Ensure device is paired at OS level
- Verify Bluetooth is enabled on both devices
- Check Arduino serial communication (9600 baud)
- Restart app and device

**Problem: Character data not displaying**
- Verify Arduino firmware is loaded correctly
- Check voltage levels on actuators (should be ~12V)
- Test with serial monitor to Arduino directly

### Azure API Issues

**Problem: Authentication failed**
- Verify API key and endpoint are correct
- Check API key hasn't expired
- Ensure API key is for correct region
- Verify request format matches Azure documentation

**Problem: OCR not working**
- Check image quality and lighting
- Verify language settings
- Ensure internet connection is active
- Check Azure subscription limits

---

## ✅ Verification Checklist

After setup, verify everything works:

- [ ] Flutter and Dart installed (`flutter --version`)
- [ ] Project dependencies installed (`flutter pub get`)
- [ ] No analyze errors (`flutter analyze`)
- [ ] Android build successful (`flutter build apk`)
- [ ] iOS build successful (`flutter build ios`)
- [ ] App runs on device/emulator (`flutter run`)
- [ ] Azure services configured and tested
- [ ] Bluetooth module paired and operational
- [ ] Arduino sketch uploaded and tested
- [ ] Actuators respond to serial commands

---

## 🆘 Need Help?

- 📚 [Flutter Documentation](https://flutter.dev/docs)
- 🐛 [Open an Issue](https://github.com/TactileText/issues)
- 💬 [GitHub Discussions](https://github.com/TactileText/discussions)
- 📧 Email: setup@tactiletext.example.com

---

**Happy coding! Your setup is now complete.** 🎉
