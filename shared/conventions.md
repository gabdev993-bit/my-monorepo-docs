# 코딩 컨벤션

## TypeScript 컨벤션

### 1. 네이밍 규칙
```typescript
// 변수 및 함수: camelCase
const userName = 'john'
const getUserData = () => {}

// 상수: UPPER_SNAKE_CASE
const API_BASE_URL = 'https://api.example.com'

// 타입 및 인터페이스: PascalCase
interface UserData {
  id: string
  name: string
}

type AuthState = 'loading' | 'authenticated' | 'unauthenticated'

// 컴포넌트: PascalCase
const UserProfile = () => {}

// 파일명: kebab-case
// user-profile.tsx
// auth-service.ts
```

### 2. 함수 작성 규칙
```typescript
// 화살표 함수 (일반적)
const fetchUserData = async (userId: string): Promise<UserData> => {
  // 구현
}

// 일반 함수 (클래스 메서드)
class AuthService {
  async signIn(email: string, password: string): Promise<AuthResult> {
    // 구현
  }
}
```

### 3. 타입 정의
```typescript
// 인터페이스 사용 (객체 구조)
interface User {
  id: string
  email: string
  name?: string
}

// 타입 별칭 사용 (유니온, 프리미티브)
type Status = 'pending' | 'success' | 'error'
type UserId = string
```

## React Native 컨벤션

### 1. 컴포넌트 구조
```typescript
// 1. Import 순서
import React from 'react'
import { View, Text } from 'react-native'
import { Button } from '@ui/components'

// 2. 타입 정의
interface Props {
  title: string
  onPress: () => void
}

// 3. 컴포넌트 정의
const MyComponent: React.FC<Props> = ({ title, onPress }) => {
  // 4. Hooks
  const [state, setState] = useState('')
  
  // 5. 이벤트 핸들러
  const handlePress = () => {
    onPress()
  }
  
  // 6. 렌더링
  return (
    <View>
      <Text>{title}</Text>
      <Button onPress={handlePress} />
    </View>
  )
}

// 7. Export
export default MyComponent
```

### 2. 스타일링
```typescript
// StyleSheet 사용
import { StyleSheet } from 'react-native'

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 16,
  },
  title: {
    fontSize: 18,
    fontWeight: 'bold',
  },
})

// 인라인 스타일 (조건부)
<View style={[styles.container, isActive && styles.activeContainer]} />
```

## 파일 구조 컨벤션

### 1. 폴더 구조
```
src/
├── components/          # 재사용 가능한 컴포넌트
│   ├── Button/
│   │   ├── Button.tsx
│   │   ├── Button.stories.tsx
│   │   └── index.ts
│   └── index.ts
├── screens/           # 화면 컴포넌트
│   ├── HomeScreen.tsx
│   └── ProfileScreen.tsx
├── services/          # 비즈니스 로직
│   ├── authService.ts
│   └── apiService.ts
├── hooks/             # 커스텀 훅
│   ├── useAuth.ts
│   └── useApi.ts
├── types/              # 타입 정의
│   ├── auth.ts
│   └── api.ts
└── utils/              # 유틸리티 함수
    ├── validation.ts
    └── formatting.ts
```

### 2. 파일명 규칙
- 컴포넌트: PascalCase (Button.tsx)
- 서비스: camelCase (authService.ts)
- 훅: camelCase with use prefix (useAuth.ts)
- 타입: camelCase (auth.ts)
- 유틸리티: camelCase (validation.ts)

## Git 컨벤션

### 1. 커밋 메시지
```
type(scope): description

feat(auth): add Google OAuth login
fix(ui): resolve button styling issue
docs(readme): update installation guide
refactor(api): simplify error handling
test(auth): add unit tests for login
```

### 2. 브랜치 네이밍
```
feature/auth-google-oauth
bugfix/button-styling
hotfix/critical-security-issue
docs/update-readme
```

## 주석 및 문서화

### 1. JSDoc 주석
```typescript
/**
 * 사용자 인증을 처리하는 서비스
 * @param email 사용자 이메일
 * @param password 사용자 비밀번호
 * @returns 인증 결과
 */
async function authenticateUser(
  email: string, 
  password: string
): Promise<AuthResult> {
  // 구현
}
```

### 2. TODO 주석
```typescript
// TODO: 에러 처리 개선 필요
// FIXME: 메모리 누수 가능성 있음
// HACK: 임시 해결책, 리팩토링 필요
```

## 성능 가이드라인

### 1. 컴포넌트 최적화
```typescript
// React.memo 사용
const ExpensiveComponent = React.memo(({ data }) => {
  return <View>{data}</View>
})

// useMemo 사용
const expensiveValue = useMemo(() => {
  return heavyCalculation(data)
}, [data])

// useCallback 사용
const handlePress = useCallback(() => {
  onPress()
}, [onPress])
```

### 2. 이미지 최적화
```typescript
// 적절한 이미지 크기
<Image 
  source={{ uri: imageUrl }}
  style={{ width: 200, height: 200 }}
  resizeMode="cover"
/>
```
