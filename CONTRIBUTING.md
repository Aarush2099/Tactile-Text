# Contributing to TactileText 🤝

First off, thank you for considering contributing to TactileText! Your efforts help make technology more accessible for 253 million visually impaired people worldwide.

This document provides guidelines and instructions for contributing to the project.

---

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [How to Contribute](#how-to-contribute)
- [Commit Guidelines](#commit-guidelines)
- [Pull Request Process](#pull-request-process)
- [Coding Standards](#coding-standards)
- [Testing](#testing)
- [Documentation](#documentation)
- [Report a Bug](#report-a-bug)
- [Suggest Enhancements](#suggest-enhancements)

---

## 📋 Code of Conduct

### Our Pledge

In the interest of fostering an open and welcoming environment, we as contributors and maintainers pledge to making participation in our project and our community a harassment-free experience for everyone, regardless of age, body size, disability, ethnicity, gender identity and expression, level of experience, nationality, personal appearance, race, religion, or sexual identity and orientation.

### Our Standards

Examples of behavior that contributes to creating a positive environment include:

- Using welcoming and inclusive language
- Being respectful of differing viewpoints and experiences
- Gracefully accepting constructive criticism
- Focusing on what is best for the community
- Showing empathy towards other community members

Examples of unacceptable behavior include:

- The use of sexualized language or imagery and unwelcome sexual attention or advances
- Trolling, insulting/derogatory comments, and personal or political attacks
- Public or private harassment
- Publishing others' private information without explicit permission
- Other conduct which could reasonably be considered inappropriate

### Enforcement

Project maintainers are responsible for clarifying the standards of acceptable behavior and are expected to take appropriate and fair corrective action in response to any instances of unacceptable behavior.

---

## 🚀 Getting Started

### Prerequisites

Before you start, ensure you have:

- **Flutter SDK** (v3.0+): [Install Flutter](https://flutter.dev/docs/get-started/install)
- **Dart SDK** (v2.1+): Comes with Flutter
- **Git**: [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- **Android Studio** or **Xcode** (for platform-specific development)
- **A GitHub account**

### Fork & Clone

1. **Fork the repository** on GitHub
2. **Clone your fork** locally:
   ```bash
   git clone https://github.com/YOUR_USERNAME/TactileText.git
   cd TactileText
   ```
3. **Add upstream remote** for syncing:
   ```bash
   git remote add upstream https://github.com/ORIGINAL_OWNER/TactileText.git
   ```

---

## 🛠️ Development Setup

### 1. Install Dependencies

```bash
flutter pub get
```

### 2. Configure Flutter

Verify your setup:
```bash
flutter doctor
```

Fix any issues reported by the doctor.

### 3. Set Up Your IDE

We recommend **VS Code** with Flutter extension:
- Install [Flutter extension](https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter)
- Install [Dart extension](https://marketplace.visualstudio.com/items?itemName=Dart-Code.dart-code)

**OR Android Studio:**
- Install Flutter and Dart plugins

### 4. Create a Feature Branch

```bash
git checkout -b feature/your-feature-name
```

Use descriptive names:
- `feature/ocr-improvement`
- `fix/bluetooth-connection-lag`
- `docs/setup-guide`

---

## 💡 How to Contribute

### Types of Contributions

#### 🐛 Bug Fixes
- Identify bugs in the issue tracker
- Create a fix with tests
- Submit a pull request with clear description

#### ✨ New Features
- Check the [Roadmap](README.md#-future-roadmap)
- Discuss major features in Issues first
- Implement following code standards
- Add tests and documentation

#### 📚 Documentation
- Improve README or guides
- Add code comments for complex logic
- Create tutorials or how-to guides
- Fix typos and clarify instructions

#### 🌍 Localization
- Add language support
- Translate UI strings
- Localize documentation

#### 🎨 UI/UX Improvements
- Enhance user interface
- Improve accessibility
- Submit screenshots of changes

#### 🔬 Testing
- Add unit tests
- Add integration tests
- Improve test coverage

#### 📱 Platform Support
- Improve Android compatibility
- Improve iOS compatibility
- Report platform-specific issues

---

## 📝 Commit Guidelines

We follow conventional commits for clear history:

### Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types

- **feat**: A new feature
- **fix**: A bug fix
- **docs**: Documentation changes
- **style**: Code style changes (formatting, etc.)
- **refactor**: Code refactoring without feature changes
- **perf**: Performance improvements
- **test**: Adding or updating tests
- **chore**: Build, dependency, or tooling changes

### Examples

```bash
# Simple fix
git commit -m "fix(bluetooth): resolve connection timeout issue"

# Feature with body
git commit -m "feat(ocr): add language selection for text recognition

- Add dropdown for language selection
- Update Azure API calls to respect language choice
- Add localization strings for supported languages"

# Documentation
git commit -m "docs(readme): add hardware assembly instructions"
```

### Best Practices

- ✅ Keep commits atomic (one logical change per commit)
- ✅ Use imperative mood ("add feature" not "added feature")
- ✅ Start with lowercase (unless starting with a name)
- ✅ No period at end of subject
- ✅ Write descriptive commit messages
- ✅ Reference issues: "fixes #123" or "relates to #456"

---

## 🔄 Pull Request Process

### Before Submitting

1. **Sync with upstream:**
   ```bash
   git fetch upstream
   git rebase upstream/main
   ```

2. **Run tests:**
   ```bash
   flutter test
   ```

3. **Format code:**
   ```bash
   flutter format .
   dart analyze .
   ```

4. **Build successfully:**
   ```bash
   flutter build apk --release
   ```

### Creating a PR

1. **Push your branch:**
   ```bash
   git push origin feature/your-feature-name
   ```

2. **Create Pull Request** on GitHub with:
   - Clear title and description
   - Reference related issues (e.g., "Fixes #123")
   - Screenshots for UI changes
   - List of changes made
   - Any breaking changes noted

### PR Template

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Related Issues
Fixes #(issue number)

## Testing Done
- [ ] Unit tests added/updated
- [ ] Tested on Android
- [ ] Tested on iOS

## Screenshots (if applicable)
Add before/after screenshots

## Checklist
- [ ] My code follows the style guidelines
- [ ] I have performed a self-review
- [ ] I have commented my code
- [ ] I have updated documentation
- [ ] My changes generate no new warnings
- [ ] I have added tests that prove my fix is effective
```

### Review Process

1. Maintainers will review within 5-7 business days
2. Address requested changes with new commits
3. Once approved, maintainer will merge

---

## 🎨 Coding Standards

### Dart/Flutter Best Practices

```dart
// ✅ Good
class BluetoothController extends ChangeNotifier {
  BluetoothConnection? _connection;
  
  Future<void> connect(String deviceId) async {
    try {
      _connection = await BluetoothConnection.toAddress(deviceId);
      notifyListeners();
    } catch (e) {
      print('Connection failed: $e');
      rethrow;
    }
  }
}

// ❌ Avoid
class BT {  // Unclear name
  var conn;  // No type annotation
  void connect(id) {  // No type annotations
    // No error handling
  }
}
```

### Style Guide

- **Naming**: Use camelCase for variables, PascalCase for classes
- **Documentation**: Add /// comments for public APIs
- **Line length**: Preferably under 80 characters
- **Imports**: Sort alphabetically, separate standard/package/local
- **Constants**: Use CONSTANT_CASE
- **Error handling**: Always handle exceptions

Example:

```dart
/// Connects to Bluetooth device with given [deviceId].
/// 
/// Throws [BluetoothException] if connection fails.
/// 
/// Returns `true` if successfully connected, `false` otherwise.
Future<bool> connectToDevice(String deviceId) async {
  // Implementation
}

const int MAX_RETRIES = 3;
const String DEFAULT_TIMEOUT = '30s';

enum ConnectionState { disconnected, connecting, connected, error }
```

---

## 🧪 Testing

### Running Tests

```bash
# Run all tests
flutter test

# Run specific test file
flutter test test/bluetooth_test.dart

# Run with coverage
flutter test --coverage
```

### Writing Tests

```dart
void main() {
  group('BluetoothConnection', () {
    test('connects successfully', () async {
      // Arrange
      final bluetooth = MockBluetoothConnection();
      
      // Act
      final result = await bluetooth.connect('device-id');
      
      // Assert
      expect(result, isTrue);
    });
    
    test('throws on invalid device ID', () async {
      final bluetooth = BluetoothConnection();
      
      expect(
        () => bluetooth.connect('invalid'),
        throwsA(isA<BluetoothException>()),
      );
    });
  });
}
```

---

## 📖 Documentation

### Code Comments

```dart
/// High-level overview of what the function does.
/// 
/// More detailed explanation if needed, including edge cases.
/// 
/// Parameters:
/// - [parameter1]: Description
/// - [parameter2]: Description
/// 
/// Returns: Description of return value
/// 
/// Throws: [SpecificException] when condition occurs
Future<void> importantFunction(String parameter1, int parameter2) {
  // Comment for complex logic
  // explaining the 'why', not the 'what'
}
```

### Update Documentation

When adding features:
1. Update README.md
2. Add code comments
3. Update relevant guides
4. Add example usage

---

## 🐛 Report a Bug

### Before Reporting

- Check [existing issues](https://github.com/TactileText/issues)
- Test with latest version
- Verify it's reproducible

### Bug Report Template

```markdown
## Description
Clear description of the bug

## Steps to Reproduce
1. First step
2. Second step
3. ...

## Expected Behavior
What should happen

## Actual Behavior
What actually happens

## Screenshots
If applicable

## Environment
- Flutter version: (output of `flutter --version`)
- Device: Android/iOS, model
- OS version: 

## Logs
```
Paste relevant error logs
```
```

---

## ✨ Suggest Enhancements

### Enhancement Request Template

```markdown
## Description
What would you like to add/improve?

## Use Case
Why would this be useful?

## Proposed Solution
How should it work?

## Alternatives Considered
Other approaches?

## Related Issues
Any existing issues related?
```

---

## 📚 Additional Resources

- [Flutter Documentation](https://flutter.dev/docs)
- [Dart Language Tour](https://dart.dev/guides/language/language-tour)
- [Git Basics](https://git-scm.com/book)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Project README](README.md)

---

## 🙏 Thank You!

Your contributions make TactileText better and help create a more accessible world for millions of visually impaired individuals. We appreciate your time and effort!

**Happy Contributing!** 🎉

---

## Questions?

- 💬 Join discussions on [GitHub Discussions](https://github.com/TactileText/discussions)
- 📧 Email us at tactiletext@example.com
- 🐦 Follow us on Twitter [@TactileText](https://twitter.com/TactileText)
