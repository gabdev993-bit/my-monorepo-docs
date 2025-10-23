# 네비게이션 기능

## 개요
Expo Router를 활용한 파일 기반 라우팅 시스템

## 라우팅 구조

### 현재 구조
```
app/
├── _layout.tsx          # 루트 레이아웃
├── index.tsx            # 홈 화면
└── llm-demo.tsx         # LLM 데모 화면
```

### 계획된 구조
```
app/
├── _layout.tsx          # 루트 레이아웃
├── index.tsx            # 홈 화면
├── auth/
│   ├── login.tsx        # 로그인 화면
│   └── register.tsx     # 회원가입 화면
├── profile/
│   ├── index.tsx        # 프로필 메인
│   └── settings.tsx     # 설정 화면
└── (tabs)/              # 탭 네비게이션
    ├── _layout.tsx      # 탭 레이아웃
    ├── home.tsx         # 홈 탭
    └── profile.tsx      # 프로필 탭
```

## 네비게이션 타입

### 1. Stack Navigation
- 화면 간 이동
- 뒤로가기 지원
- 헤더 커스터마이징

### 2. Tab Navigation
- 하단 탭 바
- 아이콘 및 라벨
- 상태 유지

### 3. Modal Navigation
- 모달 오버레이
- 전체 화면 모달
- 드롭다운 모달

## 구현 예시

### 1. 기본 네비게이션
```typescript
import { router } from 'expo-router'

// 화면 이동
router.push('/profile')
router.replace('/auth/login')
router.back()

// 파라미터 전달
router.push({
  pathname: '/profile',
  params: { userId: '123' }
})
```

### 2. 탭 네비게이션
```typescript
import { Tabs } from 'expo-router'

export default function TabLayout() {
  return (
    <Tabs>
      <Tabs.Screen name="home" options={{ title: '홈' }} />
      <Tabs.Screen name="profile" options={{ title: '프로필' }} />
    </Tabs>
  )
}
```

### 3. 인증 가드
```typescript
import { useEffect } from 'react'
import { router } from 'expo-router'
import { isAuthenticated } from '../services/authService'

export default function AuthGuard({ children }) {
  useEffect(() => {
    const checkAuth = async () => {
      const authenticated = await isAuthenticated()
      if (!authenticated) {
        router.replace('/auth/login')
      }
    }
    checkAuth()
  }, [])

  return children
}
```

## 상태 관리

### 1. 전역 상태
- 인증 상태
- 사용자 정보
- 앱 설정

### 2. 로컬 상태
- 화면별 상태
- 폼 데이터
- UI 상태

## 성능 최적화

### 1. 지연 로딩
```typescript
import { lazy } from 'react'

const ProfileScreen = lazy(() => import('./ProfileScreen'))
```

### 2. 메모이제이션
```typescript
import { memo } from 'react'

const ExpensiveComponent = memo(({ data }) => {
  // 렌더링 로직
})
```

## 접근성

### 1. 스크린 리더 지원
- 적절한 라벨링
- 네비게이션 힌트
- 포커스 관리

### 2. 키보드 네비게이션
- Tab 순서
- 엔터 키 처리
- 화살표 키 지원
