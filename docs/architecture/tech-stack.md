# 기술 스택

`설치됨`: 저장소 설정·`package.json`에 반영됨 · `도입 예정`: 결정됐지만 아직 적용 전

## 런타임 / 프레임워크

| 영역 | 기술 | 상태 |
| --- | --- | --- |
| 런타임 | Node.js 24 | 설치됨 (`.nvmrc`, `engines`) |
| 패키지 매니저 | pnpm 10 | 설치됨 (`packageManager`) |
| 프레임워크 | Next.js 16 (App Router) | 설치됨 |
| UI 런타임 | React 19 + React Compiler | 설치됨 |
| 언어 | TypeScript (strict) | 설치됨 |
| 스타일 | Tailwind CSS v4 | 설치됨 |

## UI / 데이터

| 영역 | 기술 | 상태 | 비고 |
| --- | --- | --- | --- |
| UI 컴포넌트 | shadcn/ui | 도입 예정 | |
| 아이콘 | lucide-react | 도입 예정 | |
| 애니메이션 | motion (구 framer-motion) | 도입 예정 | import는 `motion/react` |
| 모달 관리 | overlay-kit | 도입 예정 | |
| 조건부 렌더링 | ts-pattern | 도입 예정 | |
| 동적 렌더링 관리 | suspensive | 도입 예정 | Suspense·ErrorBoundary 선언적 처리 |
| 서버 상태 | TanStack Query | 도입 예정 | 뉴스·선수 목록의 페이지네이션/더보기 |
| 클라이언트 상태 | Zustand | 도입 예정 | 사용 기준: [state-management](state-management.md) |
| API 타입 검증 | zod | 도입 예정 | API 응답 검증 |

## 품질 / 테스트

| 영역 | 기술 | 상태 | 비고 |
| --- | --- | --- | --- |
| Lint | ESLint 9 (`eslint-config-next`) | 설치됨 | |
| Format | Prettier + `@ianvs/prettier-plugin-sort-imports` + `prettier-plugin-tailwindcss` | 도입 예정 | import·Tailwind 클래스 자동 정렬 |
| Git hook | Husky + lint-staged | 도입 예정 | → [ci](../collaboration/ci.md#로컬-husky) |
| 단위/컴포넌트 테스트 | Vitest | 도입 예정 | |
| E2E 테스트 | Playwright | 도입 예정 | |
| 접근성 검사 | `@axe-core/playwright` | 도입 예정 | E2E에서 페이지별 검사 |
| 컴포넌트 문서·테스트 | Storybook (`@storybook/addon-vitest`) | 도입 예정 | 공통 컴포넌트 인터랙션 테스트 |
| 시각 회귀 테스트 | Chromatic | 도입 예정 | TurboSnap, `develop` 대상 PR |
| API 모킹 | MSW (`msw-storybook-addon`) | 도입 예정 | Vitest·Storybook·Playwright 공유 |

## CI/CD · 배포 · 모니터링

| 영역 | 기술 | 상태 |
| --- | --- | --- |
| CI/CD | GitHub Actions | 도입 예정 |
| stacked PR | Graphite CLI (`gt`) | 도입 예정 |
| AI 코드 리뷰 | CodeRabbit | 설치됨 (`.coderabbit.yaml`) |
| 알림 | Discord | 도입 예정 |
| 성능 측정 | Vercel Speed Insights | 도입 예정 |
| 행동 분석 | Google Analytics 4 | 도입 예정 |
| 에러 추적 | Sentry | 도입 예정 |
| 프론트 호스팅 | Vercel | 도입 예정 |
| 백엔드 | Spring Boot on AWS (별도 저장소) | 운영 중 |
