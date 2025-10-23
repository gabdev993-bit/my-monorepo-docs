# Xcode 설정 가이드

## Xcode 설치

### 1. App Store에서 설치
1. Mac App Store를 열기
2. "Xcode" 검색
3. 설치 (약 15GB, 시간 소요)

### 2. Command Line Tools 설치
```bash
# Xcode Command Line Tools 설치
xcode-select --install

# 설치 확인
xcode-select --version
xcodebuild -version
```

## iOS 시뮬레이터 설정

### 1. 시뮬레이터 실행
```bash
# iOS 시뮬레이터 열기
open -a Simulator

# 또는 Xcode에서
# Xcode → Open Developer Tool → Simulator
```

### 2. 시뮬레이터 관리
```bash
# 사용 가능한 시뮬레이터 목록
xcrun simctl list devices

# 특정 시뮬레이터 실행
xcrun simctl boot "iPhone 15 Pro"
```

## 프로젝트 설정

### 1. iOS 프로젝트 열기
```bash
cd apps/mobile
npx expo run:ios
```

### 2. Xcode 프로젝트 설정
- `apps/mobile/ios/MyMonorepoMobile.xcodeproj` 열기
- Bundle Identifier 확인: `com.mymonorepo.mobile`
- Signing & Capabilities 설정
- Info.plist에서 URL Schemes 확인

## 개발 도구

### 1. React Native Debugger
```bash
# React Native Debugger 설치
brew install --cask react-native-debugger
```

### 2. Flipper (선택사항)
```bash
# Flipper 설치
brew install --cask flipper
```

## 문제 해결

### 1. 시뮬레이터가 실행되지 않는 경우
```bash
# 시뮬레이터 재설정
xcrun simctl shutdown all
xcrun simctl erase all
```

### 2. 빌드 오류 해결
```bash
# 캐시 정리
cd apps/mobile
npx expo r -c
rm -rf node_modules
pnpm install
```

### 3. CocoaPods 문제
```bash
cd apps/mobile/ios
pod deintegrate
pod install
```
