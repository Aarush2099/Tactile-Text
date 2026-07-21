# TactileText Architecture 🏗️

Comprehensive technical documentation of TactileText system design and architecture.

---

## Table of Contents

- [System Overview](#system-overview)
- [Hardware Architecture](#hardware-architecture)
- [Software Architecture](#software-architecture)
- [Communication Protocol](#communication-protocol)
- [Application Layers](#application-layers)
- [Data Flow](#data-flow)
- [Design Patterns](#design-patterns)
- [Cloud Services Integration](#cloud-services-integration)
- [Security Considerations](#security-considerations)
- [Performance Optimization](#performance-optimization)

---

## System Overview

TactileText is a two-component integrated system:

```
┌─────────────────────────────────────────────────────────────┐
│                    TactileText System                       │
├───────────────────────────────────────────────────────────────┤
│                                                               │
│  ┌──────────────────────────────────────────────────────┐   │
│  │         Mobile Application (Flutter)                 │   │
│  │  ┌─────────────────────────────────────────────┐    │   │
│  │  │  Presentation Layer (UI/UX)                 │    │   │
│  │  │  - Home Screen                              │    │   │
│  │  │  - Bluetooth Connection                     │    │   │
│  │  │  - Input Methods (Text/OCR/Voice)          │    │   │
│  │  │  - Settings                                 │    │   │
│  │  └─────────────────────────────────────────────┘    │   │
│  │  ┌─────────────────────────────────────────────┐    │   │
│  │  │  Business Logic Layer                       │    │   │
│  │  │  - Content Processing                       │    │   │
│  │  │  - Braille Conversion                       │    │   │
│  │  │  - State Management (Provider)              │    │   │
│  │  │  - File Management                          │    │   │
│  │  └─────────────────────────────────────────────┘    │   │
│  │  ┌─────────────────────────────────────────────┐    │   │
│  │  │  Data & Service Layer                       │    │   │
│  │  │  - Bluetooth Communication                  │    │   │
│  │  │  - Azure Service Integration                │    │   │
│  │  │  - Local Storage (Hive)                     │    │   │
│  │  │  - HTTP Client                              │    │   │
│  │  └─────────────────────────────────────────────┘    │   │
│  └──────────────────────────────────────────────────────┘   │
│                           │                                  │
│                           ▼ (Bluetooth Serial)               │
│  ┌──────────────────────────────────────────────────────┐   │
│  │        Hardware (Arduino + Actuators)               │   │
│  │  ┌─────────────────────────────────────────────┐    │   │
│  │  │  Arduino Uno Microcontroller                │    │   │
│  │  │  - Serial Communication                     │    │   │
│  │  │  - GPIO Control                             │    │   │
│  │  │  - Byte Encoding/Decoding                   │    │   │
│  │  │  - Real-time Actuator Control               │    │   │
│  │  └─────────────────────────────────────────────┘    │   │
│  │  ┌─────────────────────────────────────────────┐    │   │
│  │  │  Actuator Driver Array (ULN2803)            │    │   │
│  │  │  Pins 2-7 → 6 Actuators                     │    │   │
│  │  └─────────────────────────────────────────────┘    │   │
│  │  ┌─────────────────────────────────────────────┐    │   │
│  │  │  6 Electromagnetic Actuators                │    │   │
│  │  │  ┌─────────────────────────────────────┐   │    │   │
│  │  │  │ Dot 1  Dot 2  Dot 3                │   │    │   │
│  │  │  │ (TL)   (TC)   (TR)                 │   │    │   │
│  │  │  │                                    │   │    │   │
│  │  │  │ Dot 4  Dot 5  Dot 6                │   │    │   │
│  │  │  │ (BL)   (BC)   (BR)                 │   │    │   │
│  │  │  └─────────────────────────────────────┘   │    │   │
│  │  └─────────────────────────────────────────────┘    │   │
│  └──────────────────────────────────────────────────────┘   │
│                           │                                  │
│                           ▼ (HTTP/HTTPS)                     │
│  ┌──────────────────────────────────────────────────────┐   │
│  │        Azure Cognitive Services                     │   │
│  │  ┌─────────────────────────────────────────────┐    │   │
│  │  │  Computer Vision (OCR)                      │    │   │
│  │  │  - Image to Text conversion                 │    │   │
│  │  │  - Language detection                       │    │   │
│  │  └─────────────────────────────────────────────┘    │   │
│  │  ┌─────────────────────────────────────────────┐    │   │
│  │  │  Speech Services                            │    │   │
│  │  │  - Text-to-Speech (TTS)                     │    │   │
│  │  │  - Speech-to-Text (STT)                     │    │   │
│  │  │  - Language support                         │    │   │
│  │  └─────────────────────────────────────────────┘    │   │
│  │  ┌─────────────────────────────────────────────┐    │   │
│  │  │  Text Analytics                             │    │   │
│  │  │  - Language detection                       │    │   │
│  │  │  - Sentiment analysis (future)              │    │   │
│  │  └─────────────────────────────────────────────┘    │   │
│  └──────────────────────────────────────────────────────┘   │
│                                                               │
└───────────────────────────────────────────────────────────────┘
```

---

## Hardware Architecture

### Components

```
Arduino Uno (ATmega328P)
├── Microcontroller
│   ├── Flash Memory: 32 KB (program storage)
│   ├── SRAM: 2 KB (runtime memory)
│   ├── EEPROM: 1 KB (persistent storage)
│   └── Clock: 16 MHz
│
├── Communication Interfaces
│   ├── UART (Serial) - HC-05 Bluetooth module
│   │   ├── Baud Rate: 9600 bps
│   │   ├── Protocol: Serial communication
│   │   └── Pins: RX0, TX1
│   │
│   └── GPIO Pins - Actuator control
│       ├── Pin 2 → Dot 1 (Top-Left)
│       ├── Pin 3 → Dot 2 (Top-Center)
│       ├── Pin 4 → Dot 3 (Top-Right)
│       ├── Pin 5 → Dot 4 (Bottom-Left)
│       ├── Pin 6 → Dot 5 (Bottom-Center)
│       └── Pin 7 → Dot 6 (Bottom-Right)
│
└── Peripheral
    └── Darlington Transistor Array (ULN2803)
        ├── 8 Input channels (using 6)
        ├── High current output drivers
        ├── Input: 5V from Arduino GPIO
        └── Output: 12V to actuators
```

### Braille Cell Design

```
Standard 6-dot Braille Configuration:

Position Layout:
┌─────────────┐
│ 1 │ 2 │ 3  │  Top Row
├───┼───┼────┤
│ 4 │ 5 │ 6  │  Bottom Row
└─────────────┘

Character 'A' (dots 1):
┌─────────────┐
│●│ │ │       (dot 1 raised)
├───┼───┼────┤
│ │ │ │       (rest flat)
└─────────────┘

Character 'B' (dots 1,2,4,5):
┌─────────────┐
│●│●│ │       (dots 1,2 raised)
├───┼───┼────┤
│●│●│ │       (dots 4,5 raised)
└─────────────┘
```

---

## Software Architecture

### Technology Stack

```
Frontend
├── Flutter Framework (v3.0+)
├── Dart Language
├── Material Design UI
├── Provider (State Management)
└── Hive (Local Storage)

Services & Integration
├── flutter_bluetooth_serial (Bluetooth)
├── image_picker (Camera/Gallery)
├── dio (HTTP Client)
├── tts_azure (Text-to-Speech)
└── file_picker (File Selection)

Backend Services
├── Microsoft Azure Cognitive Services
│   ├── Computer Vision (OCR)
│   ├── Speech Services (TTS/STT)
│   └── Text Analytics
└── External APIs

Hardware Communication
└── Serial Protocol (Custom)
```

---

## Communication Protocol

### Serial Protocol Format

#### Command Structure

```
┌─────────────┬──────────────┬──────────────┬─────────────┐
│  HEADER     │  COMMAND     │  DATA        │  CHECKSUM   │
│  (1 byte)   │  (1 byte)    │  (N bytes)   │  (1 byte)   │
└─────────────┴──────────────┴──────────────┴─────────────┘

HEADER:     0xFF (synchronization marker)
COMMAND:
  0x01 → BRAILLE_DISPLAY (display braille)
  0x02 → CLEAR_DISPLAY (clear all dots)
  0x03 → SENSOR_READ (read sensors, if applicable)
  0x04 → STATUS_CHECK (health check)

DATA:       
  For BRAILLE_DISPLAY:
  - Bit 0 → Dot 1
  - Bit 1 → Dot 2
  - Bit 2 → Dot 3
  - Bit 3 → Dot 4
  - Bit 4 → Dot 5
  - Bit 5 → Dot 6
  - Bits 6-7 → Reserved

CHECKSUM:   XOR of all previous bytes
```

#### Example Commands

```
Display character 'A' (binary: 00000001):
Frame: 0xFF 0x01 0x01 0xFF (Header, Command, Data, Checksum)

Clear display:
Frame: 0xFF 0x02 0x00 0xFD (Header, Command, No data, Checksum)

Status check:
Frame: 0xFF 0x04 0x00 0xFB (Header, Command, No data, Checksum)
```

### Bluetooth Communication

```
Device Setup
├── Baud Rate: 9600 bps
├── Data Bits: 8
├── Stop Bits: 1
├── Parity: None
├── Flow Control: None
/>

Connection Flow
1. Discovery (scan for HC-05)
2. Pairing (if not paired)
3. Connection (establish link)
4. Pin Setup (verify compatibility)
5. Data Transmission (start sending bytes)

Error Handling
├── Timeout Recovery (3s without response)
├── Checksum Validation
├── Automatic Reconnection
└── Fallback Modes
```

---

## Application Layers

### 1. Presentation Layer (UI)

```dart
// Main screens
lib/home.dart                   → Home screen, navigation
lib/bluetoothsettings.dart      → Device pairing, connection
lib/openTextFile.dart           → File browser
lib/selectAndOpen.dart          → File selection UI

// Widgets
lib/main.dart                   → App root, theme setup
```

**Responsibilities:**
- User input handling
- Visual feedback
- Navigation
- Error display
- Settings management

### 2. Business Logic Layer

**Content Processing Module**
```dart
lib/ocr.dart
├── OCR request handling
├── Image preprocessing
├── Azure API calls
└── Result processing

lib/recorder.dart
├── Audio recording
├── Speech-to-text
├── Audio playback

lib/texttobraille/
├── Text to Braille conversion
├── Braille formatting
└── Character encoding
```

**State Management**
```
Provider pattern
├── BluetoothProvider (connection state)
├── ContentProvider (loaded content)
├── SettingsProvider (user preferences)
└── RecorderProvider (audio state)
```

### 3. Data & Service Layer

```dart
lib/main.dart (Services)
├── BluetoothService
│   ├── Device discovery
│   ├── Connection management
│   ├── Data transmission
│   └── Error handling
│
├── AzureService
│   ├── OCR processing
│   ├── TTS streaming
│   ├── STT processing
│   └── Configuration management
│
└── StorageService
    ├── File I/O
    ├── Local database (Hive)
    ├── Cache management
    └── Preference storage
```

---

## Data Flow

### Text to Braille Display Flow

```
User Input
    │
    ▼
Text Processing
    │
    ├─ Plain Text
    │   │
    │   └─ Direct use
    │
    ├─ Captured Image
    │   │
    │   ▼
    │  Azure OCR Service
    │   │
    │   ▼
    │  Extracted Text
    │
    └─ Speech Input
        │
        ▼
       Azure STT Service
        │
        ▼
       Converted Text
        │
        ▼
    Text Normalization
    │
    ├─ Lowercase conversion
    ├─ Remove special chars
    └─ Validate input
    │
    ▼
    Unicode to Braille Conversion
    │
    ├─ Character code → Braille pattern
    ├─ Apply language rules
    └─ Generate dot patterns
    │
    ▼
    Bluetooth Transmission
    │
    ├─ Encode to bytes
    ├─ Add checksum
    ├─ Serialize transmission
    └─ Handle ACK/NACK
    │
    ▼
    Arduino Processing
    │
    ├─ Decode byte
    ├─ Extract dot pattern
    ├─ Drive actuators
    └─ Provide haptic feedback
    │
    ▼
    Physical Display
    │
    User reads braille
    
    Parallel: Azure TTS
    │
    ├─ Text to audio
    ├─ Stream to device
    └─ Play audio feedback
```

---

## Design Patterns

### 1. Provider Pattern (State Management)

```dart
class BluetoothProvider extends ChangeNotifier {
  BluetoothConnection? _connection;
  
  void updateConnection(BluetoothConnection conn) {
    _connection = conn;
    notifyListeners(); // Rebuild widgets
  }
}

// Usage in widgets
Consumer<BluetoothProvider>(
  builder: (context, provider, _) {
    return Text(provider.connectionStatus);
  },
)
```

### 2. Singleton Pattern (Services)

```dart
class AzureService {
  static final AzureService _instance = AzureService._internal();
  
  factory AzureService() {
    return _instance;
  }
  
  AzureService._internal();
}
```

### 3. Factory Pattern (Device Creation)

```dart
abstract class BrailleDisplay {
  Future<void> displayCharacter(int brailleCode);
}

class BluetoothBrailleDisplay implements BrailleDisplay {
  // Implementation
}

class SerialBrailleDisplay implements BrailleDisplay {
  // Implementation
}
```

### 4. Observer Pattern (Event Handling)

```dart
StreamController<BrailleEvent> brailleEvents = StreamController();

brailleEvents.stream.listen((event) {
  // Handle braille display event
});
```

---

## Cloud Services Integration

### Azure Cognitive Services

```
┌─────────────────────────────────┐
│  Azure Cognitive Services       │
│  (Shared Multi-service Account) │
└─────────────────────────────────┘
        │
        ├─────────────┬───────────────┬──────────────┐
        │             │               │              │
        ▼             ▼               ▼              ▼
    Computer      Speech           Text         Language
    Vision        Services       Analytics      Understanding
        │             │               │              │
        ├─ OCR        ├─ TTS          ├─ Detect      └─ Not yet
        ├─ Read       ├─ STT          └─ Extract
        └─ Analyze    └─ Translation

Authentication
├─ API Key (Header)
└─ Endpoint URL (Region-specific)

Rate Limits
├─ Free: 20 calls/minute
├─ Standard: 100 calls/minute
└─ Custom: Based on tier

Pricing (as of 2026)
├─ OCR: $1 per 1000 images
├─ TTS: $16 per 1M characters
└─ STT: $1 per 1 hour
```

### API Integration Pattern

```dart
// Multipart form data for OCR
final FormData formData = FormData.fromMap({
  'image': await MultipartFile.fromFile(imagePath),
  'language': 'en'
});

// HTTP request
final response = await dio.post(
  'https://{region}.api.cognitive.microsoft.com/vision/v3.2/ocr',
  data: formData,
  options: Options(
    headers: {'Ocp-Apim-Subscription-Key': apiKey}
  ),
);
```

---

## Security Considerations

### 1. API Key Management

```
❌ DO NOT:
- Hardcode API keys in source code
- Commit keys to Git repository
- Display keys in logs

✅ DO:
- Use environment variables
- Store in secure config files (not tracked)
- Use platform-specific secure storage
- Rotate keys regularly
```

### 2. Data Privacy

```
User Data Protection
├─ Local storage encrypted (Hive supports encryption)
├─ No data sent without consent
├─ Clear data retention policies
├─ GDPR compliance for EU users
└─ Accessibility audit for compliance

Azure Requests
├─ HTTPS only (TLS 1.2+)
├─ Minimal data transmission
├─ No logging of personal data
└─ Compliance with Azure security standards
```

### 3. Bluetooth Security

```
Pairing Process
├─ Device discovery (pairing mode)
├─ PIN verification (default: 0000 or 1234)
├─ Link key generation
└─ Trusted device storage

During Communication
├─ Encrypted pairing
├─ Checksum validation
├─ No sensitive data in clear text
└─ Connection timeout security
```

---

## Performance Optimization

### 1. Bluetooth Optimization

```
Reduce Latency
├─ Increase baud rate (if supported)
├─ Batch character transmissions
├─ Use binary encoding instead of text
└─ Implement local buffering

Power Efficiency
├─ Disable Bluetooth when not in use
├─ Reduce transmission frequency
├─ Optimize packet size
└─ Use low-energy protocols (BLE future)
```

### 2. Azure API Optimization

```
Reduce Costs & Latency
├─ Cache OCR results for identical images
├─ Batch TTS requests
├─ Use regional endpoints
├─ Implement retry with exponential backoff

Efficient Requests
├─ Compress images before upload
├─ Use language hints for better accuracy
├─ Limit image resolution to necessary
└─ Stream audio for TTS
```

### 3. App Performance

```
Memory Optimization
├─ Lazy load features
├─ Dispose resources properly
├─ Cache frequently accessed data
└─ Monitor memory usage

UI Performance
├─ Use const constructors
├─ Implement efficient list rendering
├─ Debounce user inputs
└─ Profile with DevTools
```

---

## Future Architecture Considerations

### Planned Enhancements

```
Cloud Backend (Optional Future)
├─ Cloud storage for user content
├─ User account synchronization
├─ Analytics and usage tracking
└─ Multi-device synchronization

Hardware Expansion
├─ BLE instead of classic Bluetooth
├─ WiFi direct communication
├─ Cloud-connected hardware
└─ IoT integration

Advanced Features
├─ Machine learning for content understanding
├─ Real-time translation
├─ Offline braille generation
└─ Edge computing support
```

---

## Deployment Architecture

### Production Deployment

```
GitHub Repository
    │
    ├─ Feature branch development
    ├─ Pull request reviews
    │
    ▼
    Test Suite
    ├─ Unit tests
    ├─ Integration tests
    └─ UI tests
    │
    ▼
    Build Pipeline
    ├─ Android: APK generation
    ├─ iOS: IPA generation
    └─ Artifact storage
    │
    ▼
    Version Release
    ├─ Beta testing (TestFlight/Google Play Beta)
    ├─ Production release
    └─ Changelog & documentation
    │
    ▼
    App Stores
    ├─ Google Play Store
    ├─ Apple App Store
    └─ GitHub Releases
    │
    ▼
    Monitoring
    ├─ Crash reporting
    ├─ Analytics
    └─ User feedback
```

---

## Documentation Resources

- [Flutter Architecture Patterns](https://flutter.dev/docs)
- [Dart Best Practices](https://dart.dev/guides)
- [Azure Cognitive Services Docs](https://docs.microsoft.com/azure/cognitive-services/)
- [Arduino Documentation](https://docs.arduino.cc/)
- [Bluetooth Serial Communication](https://en.wikipedia.org/wiki/Bluetooth#Protocol)

---

**Architecture maintained for clarity, scalability, and accessibility.** 🏛️
