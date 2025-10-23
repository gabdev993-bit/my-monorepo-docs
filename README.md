# 📚 프로젝트 문서

이 폴더는 My Monorepo 프로젝트의 모든 문서를 포함합니다.

## 📁 문서 구조

### 📋 Planning (계획 및 설계)
- [프로젝트 개요](./planning/project-overview.md) - 프로젝트 기본 정보 및 기술 스택
- [아키텍처 설계](./planning/architecture.md) - 시스템 아키텍처 및 데이터 플로우
- [로드맵](./planning/roadmap.md) - 개발 단계별 계획
- [요구사항 명세서](./planning/requirements.md) - 기능 및 비기능 요구사항

### 🛠️ Development (개발 환경)
- [환경 설정 가이드](./development/setup-guides/environment-setup.md) - 전체 개발 환경 설정
- [Xcode 설정](./development/setup-guides/xcode-setup.md) - iOS 개발 환경
- [Android 설정](./development/setup-guides/android-setup.md) - Android 개발 환경

### 📱 Mobile (모바일 앱)
- [인증 설정](./mobile/auth-setup.md) - Supabase + Google OAuth 설정
- [인증 기능](./mobile/features/authentication.md) - 인증 시스템 사용법
- [네비게이션](./mobile/features/navigation.md) - 라우팅 및 네비게이션

### 🔄 Shared (공유 문서)
- [프로젝트 규칙](./shared/project-rules.md) - 핵심 개발 규칙 및 가이드라인
- [코딩 컨벤션](./shared/conventions.md) - TypeScript, React Native 코딩 규칙
- [문제 해결](./shared/troubleshooting.md) - 일반적인 문제 및 해결 방법

## 🚀 빠른 시작

### 1. 개발 환경 설정
```bash
# 의존성 설치
pnpm install

# 모바일 앱 개발 서버 시작
cd apps/mobile
pnpm dev
```

### 2. 주요 명령어
```bash
# iOS 시뮬레이터 실행
pnpm ios

# Android 에뮬레이터 실행
pnpm android

# 빌드
eas build --platform all
```

### 3. 문서 읽기 순서
1. [프로젝트 규칙](./shared/project-rules.md) - 핵심 개발 규칙 숙지
2. [프로젝트 개요](./planning/project-overview.md) - 프로젝트 이해
3. [환경 설정 가이드](./development/setup-guides/environment-setup.md) - 개발 환경 구축
4. [인증 설정](./mobile/auth-setup.md) - 인증 시스템 설정
5. [코딩 컨벤션](./shared/conventions.md) - 상세 코딩 규칙

## 📝 문서 업데이트

문서를 업데이트할 때는 다음 사항을 확인하세요:

- [ ] 관련 코드 변경사항 반영
- [ ] 스크린샷 및 예시 코드 업데이트
- [ ] 링크 유효성 확인
- [ ] 버전 정보 업데이트

## 🤝 기여하기

문서 개선 제안이나 오류 발견 시:
1. 이슈 생성
2. 수정 사항 제안
3. Pull Request 생성

---

**마지막 업데이트**: 2024년 12월
