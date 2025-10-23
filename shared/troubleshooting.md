# 문제 해결 가이드

## 일반적인 문제

### 1. Metro 서버 문제

#### 문제: Metro 서버가 시작되지 않음
```bash
# 해결 방법
npx expo r -c
rm -rf node_modules
pnpm install
```

#### 문제: 포트 충돌
```bash
# 포트 사용 중인 프로세스 확인
lsof -ti:8081

# 프로세스 종료
kill -9 $(lsof -ti:8081)
```

### 2. iOS 시뮬레이터 문제

#### 문제: 시뮬레이터가 실행되지 않음
```bash
# 시뮬레이터 재설정
xcrun simctl shutdown all
xcrun simctl erase all

# Xcode 재시작
killall Xcode
open -a Xcode
```

#### 문제: 빌드 실패
```bash
# 캐시 정리
cd apps/mobile/ios
rm -rf build
pod deintegrate
pod install
```

### 3. Android 에뮬레이터 문제

#### 문제: ADB 연결 실패
```bash
# ADB 서버 재시작
adb kill-server
adb start-server

# 디바이스 목록 확인
adb devices
```

#### 문제: 에뮬레이터 성능 저하
- AVD Manager에서 에뮬레이터 설정 수정:
  - RAM: 4GB 이상
  - VM Heap: 512MB
  - Graphics: Hardware - GLES 2.0

## 인증 관련 문제

### 1. Google OAuth 로그인 실패

#### 원인: Bundle ID 불일치
```bash
# iOS Bundle ID 확인
# ios/MyMonorepoMobile/Info.plist
# CFBundleIdentifier 확인

# Google Cloud Console에서 Bundle ID 일치 확인
```

#### 원인: Deep Link 설정 오류
```xml
<!-- iOS Info.plist 확인 -->
<key>CFBundleURLSchemes</key>
<array>
  <string>com.googleusercontent.apps.939087202767-8j3bsdb26obnkfi85qtmml2m757hcc84</string>
</array>
```

### 2. Supabase 연결 실패

#### 원인: 환경 변수 누락
```bash
# 환경 변수 확인
echo $EXPO_PUBLIC_SUPABASE_URL
echo $EXPO_PUBLIC_SUPABASE_ANON_KEY
```

#### 원인: 네트워크 문제
```typescript
// Supabase 연결 테스트
import { supabase } from './src/services/supabaseClient'

const testConnection = async () => {
  try {
    const { data, error } = await supabase.from('test').select('*')
    console.log('Connection test:', { data, error })
  } catch (err) {
    console.error('Connection failed:', err)
  }
}
```

## 빌드 관련 문제

### 1. EAS Build 실패

#### 문제: 환경 변수 누락
```bash
# EAS 환경 변수 설정
eas secret:create --scope project --name EXPO_PUBLIC_SUPABASE_URL --value "your_url"
eas secret:create --scope project --name EXPO_PUBLIC_SUPABASE_ANON_KEY --value "your_key"
```

#### 문제: iOS 서명 문제
```bash
# Apple Developer 계정 확인
eas credentials

# 프로비저닝 프로파일 재생성
eas credentials --platform ios
```

### 2. Android 빌드 실패

#### 문제: 키스토어 문제
```bash
# 키스토어 재생성
eas credentials --platform android
```

#### 문제: Gradle 빌드 실패
```bash
# Gradle 캐시 정리
cd apps/mobile/android
./gradlew clean
./gradlew build
```

## 성능 문제

### 1. 앱 시작 속도 느림

#### 해결 방법:
```typescript
// 지연 로딩 사용
const LazyComponent = lazy(() => import('./LazyComponent'))

// 불필요한 import 제거
// Tree shaking 확인
```

### 2. 메모리 누수

#### 해결 방법:
```typescript
// 이벤트 리스너 정리
useEffect(() => {
  const subscription = onAuthStateChange(callback)
  return () => subscription.unsubscribe()
}, [])

// 타이머 정리
useEffect(() => {
  const timer = setInterval(callback, 1000)
  return () => clearInterval(timer)
}, [])
```

## 디버깅 도구

### 1. React Native Debugger
```bash
# 설치
brew install --cask react-native-debugger

# 실행
open -a "React Native Debugger"
```

### 2. Flipper
```bash
# 설치
brew install --cask flipper

# 실행
open -a Flipper
```

### 3. 로그 확인
```bash
# iOS 시뮬레이터 로그
xcrun simctl spawn booted log stream --predicate 'process == "MyMonorepoMobile"'

# Android 로그
adb logcat | grep "MyMonorepoMobile"
```

## 네트워크 문제

### 1. API 호출 실패
```typescript
// 네트워크 상태 확인
import NetInfo from '@react-native-community/netinfo'

const checkNetwork = async () => {
  const state = await NetInfo.fetch()
  console.log('Network state:', state)
}
```

### 2. CORS 문제
```typescript
// Supabase CORS 설정 확인
// Supabase Dashboard → Settings → API
// CORS origins에 앱 URL 추가
```

## 도움 요청 시 포함할 정보

### 1. 환경 정보
- OS 버전
- Node.js 버전
- React Native 버전
- Expo 버전

### 2. 오류 로그
- 전체 오류 메시지
- 스택 트레이스
- 재현 단계

### 3. 시도한 해결 방법
- 실행한 명령어
- 확인한 설정
- 참고한 문서
