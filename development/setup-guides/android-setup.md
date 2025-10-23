# Android 개발 환경 설정

## Android Studio 설치

### 1. Android Studio 다운로드
- [Android Studio 공식 사이트](https://developer.android.com/studio)에서 다운로드
- macOS용 .dmg 파일 설치

### 2. SDK 설정
- Android Studio 실행
- SDK Manager에서 다음 설치:
  - Android SDK Platform 34
  - Android SDK Build-Tools 34.0.0
  - Android Emulator
  - Android SDK Platform-Tools

## 환경 변수 설정

### 1. ~/.zshrc 또는 ~/.bash_profile에 추가
```bash
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/platform-tools
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin
```

### 2. 설정 적용
```bash
source ~/.zshrc
```

## Android 에뮬레이터 설정

### 1. AVD Manager에서 에뮬레이터 생성
- Android Studio → Tools → AVD Manager
- Create Virtual Device
- Pixel 7 또는 최신 기기 선택
- API Level 34 (Android 14) 선택

### 2. 에뮬레이터 실행
```bash
# 에뮬레이터 목록 확인
emulator -list-avds

# 특정 에뮬레이터 실행
emulator -avd Pixel_7_API_34
```

## 프로젝트 실행

### 1. Android 프로젝트 실행
```bash
cd apps/mobile
npx expo run:android
```

### 2. 디바이스 연결 (실제 기기)
```bash
# USB 디버깅 활성화 후
adb devices
```

## 문제 해결

### 1. ADB 연결 문제
```bash
# ADB 서버 재시작
adb kill-server
adb start-server
```

### 2. 빌드 오류
```bash
# Gradle 캐시 정리
cd apps/mobile/android
./gradlew clean
```

### 3. 에뮬레이터 성능 최적화
- AVD Manager → Edit → Advanced Settings
- RAM: 4GB 이상
- VM Heap: 512MB
- Graphics: Hardware - GLES 2.0
