# Building APK for Yoruba Food WebView App

## Prerequisites
- Flutter SDK (3.35.3 or later)
- Android SDK with API level 34
- Java 17 or later
- At least 8GB free disk space

## Setup Instructions

### 1. Install Flutter
```bash
# Download Flutter
git clone https://github.com/flutter/flutter.git -b stable
export PATH="$PATH:`pwd`/flutter/bin"
```

### 2. Install Android SDK
```bash
# Download Android command line tools
wget https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip
unzip commandlinetools-linux-11076708_latest.zip
mkdir -p android-sdk/cmdline-tools
mv cmdline-tools android-sdk/cmdline-tools/latest

# Set environment variables
export ANDROID_HOME=$PWD/android-sdk
export PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin:$ANDROID_HOME/platform-tools

# Accept licenses and install required packages
yes | sdkmanager --licenses
sdkmanager "platform-tools" "platforms;android-34" "build-tools;34.0.0"

# Configure Flutter
flutter config --android-sdk $ANDROID_HOME
```

### 3. Build APK
```bash
# Navigate to project directory
cd cusineflutter

# Clean and get dependencies
flutter clean
flutter pub get

# Build APK (choose one)
flutter build apk --release                    # Release APK (smaller, optimized)
flutter build apk --debug                      # Debug APK (larger, with debug info)
flutter build apk --split-per-abi             # Multiple APKs for different architectures
```

## APK Locations
After successful build, APKs will be located at:
- **Release APK**: `build/app/outputs/flutter-apk/app-release.apk`
- **Debug APK**: `build/app/outputs/flutter-apk/app-debug.apk`
- **Split APKs**: `build/app/outputs/flutter-apk/app-{architecture}-release.apk`

## App Details
- **Package Name**: com.example.yoruba_food_webview
- **App Name**: Yoruba Food Helper
- **Target URL**: https://v0-yoruba-food-helper.vercel.app/
- **Minimum Android Version**: API 21 (Android 5.0)
- **Target Android Version**: API 34 (Android 14)

## Troubleshooting

### Common Issues:
1. **NDK Error**: Remove NDK requirement from `android/app/build.gradle.kts`
2. **Java Version**: Ensure Java 17 is installed and JAVA_HOME is set
3. **Disk Space**: Ensure at least 8GB free space for build process
4. **Gradle Issues**: Clear Gradle cache with `rm -rf ~/.gradle`

### Alternative Build Methods:
1. **GitHub Actions**: Use CI/CD to build APK automatically
2. **Docker**: Use Flutter Docker image for consistent builds
3. **Cloud Build**: Use services like Codemagic or GitHub Actions

## Installation
Once built, install the APK on Android device:
```bash
adb install build/app/outputs/flutter-apk/app-release.apk
```

Or transfer the APK file to your Android device and install manually.