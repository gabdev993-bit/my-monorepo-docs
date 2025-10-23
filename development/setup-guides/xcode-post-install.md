# Xcode 설치 후 설정 가이드

## 1. Xcode 개발자 디렉토리 설정

Xcode가 설치된 후 다음 명령어를 실행하여 개발자 디렉토리를 설정해야 합니다:

```bash
sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
```

**중요**: 이 명령어는 관리자 권한이 필요하므로 터미널에서 직접 실행해주세요.

## 2. Xcode 라이선스 동의

```bash
sudo xcodebuild -license accept
```

## 3. CocoaPods 설치

iOS 의존성 관리를 위해 CocoaPods를 설치합니다:

```bash
sudo gem install cocoapods
```

## 4. iOS 시뮬레이터 설정

### 시뮬레이터 실행
```bash
# iOS 시뮬레이터 열기
open -a Simulator

# 또는 Xcode에서
# Xcode → Open Developer Tool → Simulator
```

### 시뮬레이터 관리
```bash
# 사용 가능한 시뮬레이터 목록
xcrun simctl list devices

# 특정 시뮬레이터 실행 (예: iPhone 15 Pro)
xcrun simctl boot "iPhone 15 Pro"
```

## 5. 프로젝트 의존성 설치

모바일 앱 디렉토리에서 iOS 의존성을 설치합니다:

```bash
cd apps/mobile/ios
pod install
```

## 6. 프로젝트 빌드 테스트

### Expo를 통한 실행
```bash
cd apps/mobile
npx expo run:ios
```

### Xcode에서 직접 실행
1. `apps/mobile/ios/MyMonorepoMobile.xcworkspace` 파일을 Xcode로 열기
2. Product → Run (⌘+R)

## 7. 문제 해결

### Xcode 개발자 디렉토리 오류
```bash
# 현재 설정 확인
xcode-select -p

# 올바른 경로로 설정
sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
```

### CocoaPods 설치 실패
```bash
# Ruby 버전 확인
ruby --version

# Ruby 업데이트 (필요시)
brew install ruby
```

### 시뮬레이터 실행 실패
```bash
# 시뮬레이터 재설정
xcrun simctl shutdown all
xcrun simctl erase all
```

## 8. 설정 확인

모든 설정이 완료되었는지 확인:

```bash
# Xcode 버전 확인
xcodebuild -version

# 시뮬레이터 확인
xcrun simctl list devices

# CocoaPods 확인
pod --version
```

## 9. 다음 단계

설정이 완료되면:
1. iOS 시뮬레이터에서 앱 실행 테스트
2. Google OAuth 로그인 테스트
3. Deep Link 동작 확인

---

**참고**: 모든 명령어는 터미널에서 순서대로 실행해주세요. 관리자 권한이 필요한 명령어는 `sudo`를 사용합니다.
