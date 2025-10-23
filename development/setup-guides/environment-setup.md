# 개발 환경 설정 가이드

## 필수 도구 설치

### 1. Node.js (22.19.0+)
```bash
# Homebrew로 설치
brew install node

# 버전 확인
node -v
npm -v
```

### 2. pnpm 패키지 매니저
```bash
# pnpm 설치
npm install -g pnpm

# 버전 확인
pnpm -v
```

### 3. Expo CLI
```bash
# Expo CLI 설치
npm install -g @expo/cli

# 버전 확인
expo --version
```

## 프로젝트 설정

### 1. 의존성 설치
```bash
# 루트에서
pnpm install

# 모바일 앱 의존성
cd apps/mobile
pnpm install
```

### 2. 환경 변수 설정
```bash
# .env 파일 생성 (apps/mobile/.env)
EXPO_PUBLIC_SUPABASE_URL=https://mbneolqjelqrbxnetpcp.supabase.co
EXPO_PUBLIC_SUPABASE_ANON_KEY=your_anon_key
EXPO_PUBLIC_GOOGLE_IOS_URL_SCHEME=your_google_scheme
EXPO_PUBLIC_GOOGLE_REVERSED_CLIENT_ID=your_reversed_client_id
EXPO_PUBLIC_APP_DEEP_LINK_SCHEME=my-monorepo-mobile
```

## 개발 서버 실행

### 1. 개발 서버 시작
```bash
cd apps/mobile
pnpm dev
```

### 2. 플랫폼별 실행
```bash
# iOS 시뮬레이터
pnpm ios

# Android 에뮬레이터
pnpm android

# 웹 브라우저
pnpm web
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

## 빌드 및 배포

### 1. EAS Build 설정
```bash
# EAS CLI 설치
npm install -g eas-cli

# 로그인
eas login

# 빌드 프로필 확인
eas build:configure
```

### 2. 빌드 실행
```bash
# 개발 빌드
eas build --platform ios --profile development

# 프로덕션 빌드
eas build --platform all --profile production
```

## 문제 해결

### 1. 캐시 정리
```bash
# Metro 캐시
npx expo r -c

# pnpm 캐시
pnpm store prune

# Node modules 재설치
rm -rf node_modules
pnpm install
```

### 2. 포트 충돌 해결
```bash
# 포트 사용 중인 프로세스 확인
lsof -ti:8081

# 프로세스 종료
kill -9 $(lsof -ti:8081)
```
