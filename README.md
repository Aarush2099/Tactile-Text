# 🖨️ TactileText: Affordable Digital Braille Solution

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Flutter](https://img.shields.io/badge/Flutter-3.0+-blue.svg)](https://flutter.dev)
[![Dart](https://img.shields.io/badge/Dart-2.1%2B-blue.svg)](https://dart.dev)
[![Arduino](https://img.shields.io/badge/Arduino-Uno-00979D.svg)](https://www.arduino.cc/)
[![Platform Support](https://img.shields.io/badge/Platforms-Android%20%7C%20iOS-brightgreen.svg)](#)

> **Empowering 253 Million Visually Impaired People with Affordable, Accessible Digital Braille Technology**

---

## 📖 Table of Contents

- [About](#about)
- [Inspiration](#inspiration)
- [What It Does](#what-it-does)
- [Technology Stack](#technology-stack)
- [Hardware](#hardware)
- [Software Features](#software-features)
- [Getting Started](#getting-started)
- [Installation](#installation)
- [Usage](#usage)
- [Architecture](#architecture)
- [Challenges & Solutions](#challenges--solutions)
- [Accomplishments](#accomplishments)
- [Future Roadmap](#future-roadmap)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## 🎯 About

TactileText is a revolutionary, cost-effective solution that combines custom hardware with intelligent software to provide digital braille display and content conversion for the visually impaired. By bringing down the cost from thousands of dollars to under $20 USD, TactileText makes quality assistive technology accessible to people in developing nations.

---

## 💖 Inspiration

My mother, an expert in teaching children with diverse abilities, opened my eyes to the profound struggles faced by the visually impaired. A gut-wrenching realization hit me:

- **253 million people** globally are visually impaired
- A **significant majority** are in developing nations like India
- Existing solutions (Digital Braille Displays) cost **thousands of dollars**
- This creates a **catastrophic education barrier** for the underprivileged

Witnessing this profound inequality, I was compelled to leverage my skills to create an innovative solution that could truly make a difference in the lives of millions.

---

## 🚀 What It Does

TactileText is a comprehensive two-part solution:

### 🖨️ Hardware: Digital Braille Cell
- **Custom-designed and prototyped** affordable braille display
- **6 electromagnetic actuators** for dynamic braille dot formation
- **Driven by** Darlington transistor array
- **Microcontroller** Arduino Uno
- **Cost:** Less than $20 USD (vs. thousands for competitors)

### 📱 Software: Intelligent Mobile App
- **Built with Flutter** for cross-platform compatibility (Android & iOS)
- **Real-time Bluetooth connectivity** with braille display
- **Azure Cognitive Services Integration** providing:
  - Digital text → Braille & Speech conversion
  - Printed text (OCR) → Braille & Speech conversion
  - Speech → Text → Braille conversion
  - Real-time audio feedback

---

## 🛠️ Technology Stack

### Frontend
- **Flutter** - Cross-platform mobile development framework
- **Dart** - Programming language
- **flutter_bluetooth_serial** - Bluetooth communication
- **image_picker** - Camera and gallery access for OCR
- **Provider** - State management
- **Hive** - Local data persistence

### Backend/Services
- **Azure Cognitive Services** - OCR, Text-to-Speech, Speech-to-Text
- **Azure Text Analytics** - Language detection and processing

### Hardware
- **Arduino Uno** - Microcontroller
- **Darlington Transistor Array** - Actuator drivers
- **6 Electromagnetic Actuators** - Braille dot actuators
- **Bluetooth Module** - Wireless communication

---

## 📋 Hardware

### Components
```
Arduino Uno
├── 6 GPIO pins → Darlington Transistor Array
├── Serial Communication (RX/TX)
└── Bluetooth Module (HC-05)

Electromagnetic Actuators Array
├── Dot 1 (Top-Left)
├── Dot 2 (Top-Center)
├── Dot 3 (Top-Right)
├── Dot 4 (Bottom-Left)
├── Dot 5 (Bottom-Center)
└── Dot 6 (Bottom-Right)
```

### Communication Protocol
- **Serial Protocol:** Byte-encoded command structure
- **Real-time Control:** Direct PORTB manipulation for synchronized dot actuation
- **Baud Rate:** 9600 bps
- **Data Format:** Single byte per braille character with bit mapping to actuators

---

## 💻 Software Features

### Core Capabilities
✨ **Multi-Modal Input Processing**
- Digital text input via keyboard or file upload
- Camera capture for printed text (OCR)
- Voice input via speech-to-text

📖 **Content Conversion Engine**
- Seamless conversion between digital text, braille, and speech
- Real-time synchronization between display and audio output
- Character-by-character navigation with Bluetooth transmission

🔊 **Accessibility Features**
- Text-to-Speech for audio feedback
- Real-time braille display updates
- File management for educational content
- Bluetooth connection management

🎨 **User Experience**
- Intuitive touch interface
- Visual feedback for connection status
- Persistent storage of user preferences
- Support for multiple document formats

---

## 🚀 Getting Started

### Prerequisites
- **Flutter SDK** (version 3.0 or higher)
- **Dart SDK** (version 2.1 or higher)
- **Android Studio** or **Xcode** for platform-specific builds
- **Arduino IDE** for hardware programming
- **Bluetooth device** (Android or iOS with Bluetooth support)

### System Requirements
- **Android:** API level 21 or higher
- **iOS:** iOS 11.0 or higher
- **Bluetooth 4.0+** compatible device

---

## 📦 Installation

### Step 1: Clone the Repository
```bash
git clone https://github.com/yourusername/TactileText.git
cd TactileText
```

### Step 2: Install Dependencies
```bash
flutter pub get
```

### Step 3: Configure Azure Cognitive Services
1. Create an Azure account and enable Cognitive Services
2. Obtain your API key and endpoint
3. Update configuration in the app (see Configuration section)

### Step 4: Build for Android
```bash
flutter build apk --release
# or
flutter run
```

### Step 5: Build for iOS
```bash
flutter build ios --release
# or
flutter run
```

### Hardware Setup
1. Flash Arduino with braille control firmware
2. Wire electromagnetic actuators to Darlington transistor array
3. Connect Bluetooth module to Arduino
4. Pair Bluetooth device with your phone

---

## 💡 Usage

### Basic Workflow

#### 1. **Connect to Braille Display**
```
Home Screen → Bluetooth Settings → Select your device → Connect
```

#### 2. **Input Method Options**
- **Keyboard Input:** Type text directly in the app
- **File Upload:** Select .txt files from device storage
- **Camera (OCR):** Capture printed text for real-time conversion
- **Voice Input:** Speak into microphone

#### 3. **View & Interact**
- Characters display on braille display in real-time
- Audio narration accompanies display
- Navigate through content character by character
- Adjust speech rate and tone as preferred

#### 4. **Save & Store**
- Processed content is stored locally
- Create collections for educational materials
- Export in multiple formats

---

## 🏗️ Architecture

### Application Layer
```
┌─────────────────────────────┐
│   Flutter Mobile App        │
│  (UI / User Interaction)    │
└──────────────┬──────────────┘
               │
┌──────────────▼──────────────┐
│  Content Processing Layer   │
│  (Text, OCR, Voice Input)   │
└──────────────┬──────────────┘
               │
┌──────────────▼──────────────┐
│  Azure Cognitive Services   │
│  (Text-to-Speech, OCR,      │
│   Speech-to-Text)           │
└──────────────┬──────────────┘
               │
┌──────────────▼──────────────┐
│  Bluetooth Communication    │
│  (Serial Protocol)          │
└──────────────┬──────────────┘
               │
┌──────────────▼──────────────┐
│  Arduino Microcontroller    │
│  (Braille Display Control)  │
└─────────────────────────────┘
```

---

## 🚧 Challenges & Solutions

### Challenge 1: Hardware to Software Bridge
**Problem:** Creating real-time communication between Arduino and mobile app without lag
**Solution:** Developed custom byte-encoding protocol with optimized serial transmission

### Challenge 2: Rapid App Development Learning Curve
**Problem:** Learning Flutter from scratch while building a complex application
**Solution:** Leveraged Flutter's excellent documentation and community resources, managed time effectively through agile development

### Challenge 3: API Integration Complexity
**Problem:** First experience with Azure Cognitive Services and multipart POST requests
**Solution:** Studied Microsoft documentation thoroughly, implemented error handling and retry logic

### Challenge 4: Cross-Platform Compatibility
**Problem:** Ensuring seamless operation across Android and iOS
**Solution:** Used Flutter's widget architecture and tested extensively on both platforms

### Challenge 5: Power Efficiency
**Problem:** Battery drain from continuous Bluetooth and Azure API calls
**Solution:** Implemented intelligent caching, batch processing, and optimized API usage

---

## ✨ Accomplishments

### 🏆 Cost-Effective Innovation
Successfully created a hardware braille solution costing **less than $20 USD**, a monumental reduction from the thousands of dollars competitors charge. This makes it truly accessible to those in developing nations.

### 🔗 Full-Stack Integration
Developed an app that seamlessly integrates Azure Cognitive Services for content conversion and communicates in real-time with a custom-built digital braille display via Bluetooth.

### 🎯 Pioneering Real-time Actuation
Designed a unique, custom protocol for real-time data transmission from a mobile app to an array of linear actuators – a novel approach not commonly seen in similar projects.

### 😊 Ultimate Validation
The most profound achievement was witnessing **Akshat**, a 100% visually impaired individual preparing for law school, read from the braille display for the very first time. His smile of satisfaction was everything; all the sleepless nights became unequivocally worthwhile.

---

## 🚀 Future Roadmap

### Phase 1: Robustness (Current Focus)
- [x] Core functionality implementation
- [ ] Enhanced exception handling
- [ ] Comprehensive error recovery
- [ ] User feedback integration
- [ ] Performance optimization

### Phase 2: Language Expansion
- [ ] Support for Hindi, Spanish, French, and other major languages
- [ ] Leverage Azure Cognitive Services' multilingual capabilities
- [ ] Localization for UI and documentation
- [ ] Community translations

### Phase 3: User-Centric Refinement
- [ ] Extended user testing with visually impaired students
- [ ] Accessibility audit and improvements
- [ ] Feature expansion based on feedback
- [ ] Simplified onboarding process

### Phase 4: Hardware Improvements
- [ ] Modular braille cell design
- [ ] Battery optimization
- [ ] Touch feedback integration
- [ ] Manufacturing guidelines for open-source production

### Phase 5: Community & Outreach
- [ ] Open-source hardware specifications
- [ ] Tutorial videos for assembly
- [ ] Educational partnership programs
- [ ] Impact measurement and reporting

---

## 📂 Project Structure

```
TactileText/
├── lib/
│   ├── main.dart              # App entry point
│   ├── home.dart              # Home screen
│   ├── bluetoothsettings.dart # Bluetooth connection management
│   ├── ocr.dart               # OCR functionality
│   ├── recorder.dart          # Audio recording for speech-to-text
│   ├── openTextFile.dart      # File handling
│   ├── SelectAndOpen.dart     # File selection UI
│   ├── SaveTextFile.dart      # File saving functionality
│   └── assets/                # App assets
├── android/                   # Android-specific build files
├── ios/                       # iOS-specific build files
├── pubspec.yaml              # Flutter dependencies
└── README.md                 # This file
```

---

## 🤝 Contributing

We welcome contributions from the community! This project impacts millions of lives, and your contributions can make a real difference.

### How to Contribute
1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/AmazingFeature`)
3. **Commit** your changes (`git commit -m 'Add some AmazingFeature'`)
4. **Push** to the branch (`git push origin feature/AmazingFeature`)
5. **Open** a Pull Request

### Contribution Areas
- 🐛 **Bug Fixes:** Report and fix issues
- ✨ **Features:** Add new functionality following the roadmap
- 📚 **Documentation:** Improve guides and comments
- 🌍 **Localization:** Help translate to other languages
- 🎨 **UI/UX:** Improve user interface and experience
- 🔬 **Testing:** Add test coverage
- 📱 **Platform Support:** Enhance Android/iOS compatibility

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

---

## 📄 License

TactileText is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

By using this project, you agree to help us build a more accessible world for everyone.

---

## 🙋 Support & Contact

### Get Help
- **Issues:** Report bugs and request features on [GitHub Issues](https://github.com/yourusername/TactileText/issues)
- **Discussions:** Join community discussions on [GitHub Discussions](https://github.com/yourusername/TactileText/discussions)
- **Email:** tactiletext@example.com

### Follow Us
- 🌐 **Website:** [tactiletext.dev](https://tactiletext.dev)
- 🐦 **Twitter:** [@TactileText](https://twitter.com/TactileText)
- 💼 **LinkedIn:** [TactileText Project](https://linkedin.com/company/tactiletext)

---

## 🌍 Impact

With your help, TactileText can reach students and professionals who have been left behind by the lack of affordable assistive technology. Every line of code, every bug fix, every documentation improvement brings us closer to a world where **visual impairment is no barrier to education and opportunity**.

---

## 🎓 Acknowledgments

- Special thanks to Akshat for being the inspiration and validation of this project
- Gratitude to my mother for opening my eyes to this critical need
- The Flutter and Dart communities for exceptional documentation
- Azure Cognitive Services team for powerful APIs
- Every contributor working to make the world more accessible

---

**Made with ❤️ for accessibility and inclusion**

*Last Updated: March 2026*
