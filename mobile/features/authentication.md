# 인증 기능 문서

## 개요
Google OAuth와 Supabase를 활용한 사용자 인증 시스템

## 주요 기능

### 1. Google OAuth 로그인
- 소셜 로그인을 통한 간편 인증
- Deep Link을 통한 안전한 OAuth 플로우
- 자동 세션 관리

### 2. 세션 관리
- 자동 토큰 갱신
- 세션 지속성
- 로그아웃 기능

### 3. 사용자 정보
- 프로필 정보 조회
- 실시간 인증 상태 감지

## 구현 파일

### 서비스 파일
- `src/services/authService.ts`: 인증 로직
- `src/services/supabaseClient.ts`: Supabase 클라이언트

### 설정 파일
- `app.json`: 환경 변수 및 OAuth 설정
- `ios/MyMonorepoMobile/Info.plist`: iOS Deep Link 설정
- `android/app/src/main/AndroidManifest.xml`: Android Deep Link 설정

## 사용법

### 1. 로그인
```typescript
import { signInWithGoogle } from './src/services/authService'

const result = await signInWithGoogle()
if (result.success) {
  console.log('로그인 성공:', result.user)
}
```

### 2. 로그아웃
```typescript
import { signOut } from './src/services/authService'

const result = await signOut()
if (result.success) {
  console.log('로그아웃 성공')
}
```

### 3. 사용자 정보 조회
```typescript
import { getUser } from './src/services/authService'

const user = await getUser()
if (user) {
  console.log('현재 사용자:', user)
}
```

### 4. 인증 상태 감지
```typescript
import { onAuthStateChange } from './src/services/authService'

const unsubscribe = onAuthStateChange((user) => {
  if (user) {
    console.log('사용자 로그인됨:', user)
  } else {
    console.log('사용자 로그아웃됨')
  }
})

// 정리
unsubscribe()
```

## 환경 변수

### 필수 환경 변수
```bash
EXPO_PUBLIC_SUPABASE_URL=https://mbneolqjelqrbxnetpcp.supabase.co
EXPO_PUBLIC_SUPABASE_ANON_KEY=your_anon_key
EXPO_PUBLIC_GOOGLE_IOS_URL_SCHEME=com.googleusercontent.apps.939087202767-8j3bsdb26obnkfi85qtmml2m757hcc84
EXPO_PUBLIC_GOOGLE_REVERSED_CLIENT_ID=com.googleusercontent.apps.939087202767-8j3bsdb26obnkfi85qtmml2m757hcc84
EXPO_PUBLIC_APP_DEEP_LINK_SCHEME=my-monorepo-mobile
```

## 보안 고려사항

1. **토큰 보안**: OAuth 토큰은 Supabase에서 안전하게 관리
2. **Deep Link 보안**: URL Scheme을 통한 안전한 리다이렉트
3. **세션 관리**: 자동 토큰 갱신 및 만료 처리
4. **환경 변수**: 민감한 정보는 환경 변수로 관리

## 문제 해결

### 1. OAuth 로그인 실패
- Google Cloud Console에서 OAuth 설정 확인
- Bundle ID/Package Name 일치 확인
- Deep Link 설정 확인

### 2. 세션 유지 실패
- Supabase Auth 설정 확인
- 네트워크 연결 상태 확인
- 토큰 만료 시간 확인

### 3. Deep Link 작동 안함
- iOS Info.plist URL Schemes 확인
- Android Manifest intent filters 확인
- 앱 재설치 후 테스트
