# docs

필요한 문서만 골라 읽는다. 각 문서는 한 주제만 다루고, 다른 주제는 링크로 넘긴다.

## architecture/ — 구조와 기술 결정

| 문서 | 내용 |
| --- | --- |
| [overview](architecture/overview.md) | 서비스 소개, 시스템 구성, 도메인 |
| [tech-stack](architecture/tech-stack.md) | 사용 기술과 도입 상태 |
| [folder-structure](architecture/folder-structure.md) | FSD 레이어·세그먼트, import 규칙, 테스트 위치 |
| [rendering](architecture/rendering.md) | Server/Client 경계, 캐시, 로딩·에러 |
| [data-flow](architecture/data-flow.md) | API 응답 형태, fetch → 검증 → 변환, 에러 처리 |
| [state-management](architecture/state-management.md) | 상태를 어디에 둘지 판단표 |
| [routing](architecture/routing.md) | 페이지 목록, `ROUTE_PATHS` |
| [seo-metadata](architecture/seo-metadata.md) | title, OG 이미지, sitemap |
| [env](architecture/env.md) | 환경변수 파일·키, 백엔드 호출 경로 |
| [performance](architecture/performance.md) | Core Web Vitals 목표, 이미지·폰트·동적 import |
| [analytics](architecture/analytics.md) | Speed Insights, GA4, Sentry |

## convention/ — 코드 작성 규칙

| 문서 | 내용 |
| --- | --- |
| [naming](convention/naming.md) | 파일·폴더·이벤트·boolean·상수·타입 이름, import |
| [comment](convention/comment.md) | 주석 금지, NOTE/TODO 예외 |
| [typescript](convention/typescript.md) | type/interface, enum, 타입 안전 |
| [ui-component](convention/ui-component.md) | shadcn, props, suspensive, overlay-kit, cva, ts-pattern, motion |
| [style](convention/style.md) | Tailwind, 토큰, 반응형, 다크 모드 |
| [accessibility](convention/accessibility.md) | WCAG 2.1 AA 규칙, 자동 검사 |
| [query](convention/query.md) | TanStack Query 팩토리, 페이지네이션 |
| [test](convention/test.md) | Vitest·Storybook·Chromatic·Playwright·MSW, 커버리지 |

## collaboration/ — 협업 프로세스

| 문서 | 내용 |
| --- | --- |
| [branch-strategy](collaboration/branch-strategy.md) | Git flow 브랜치, 작업 브랜치 이름, 머지 방식 |
| [commit](collaboration/commit.md) | 커밋 헤더·타입 (상세는 commit-message-generator 스킬) |
| [pr-flow](collaboration/pr-flow.md) | 기본 플로우, 템플릿, stacked PR(`gt`), hotfix |
| [code-review](collaboration/code-review.md) | CodeRabbit 리뷰 기준 체크리스트, 지적 처리 |
| [ci](collaboration/ci.md) | Husky, GitHub Actions 잡, Vercel, Discord 알림 |

## feature/ — 페이지별 기록

| 문서 | 내용 |
| --- | --- |
| [feature/README](feature/README.md) | 폴더·파일명 규칙, 읽는 순서, 설계 문서 템플릿 |

## 문서 운영 규칙

1. 문서는 한국어로 쓴다.
2. 문서 하나는 300줄 이내로 쓴다. 넘으면 하위 문서로 나누고 상위 문서에서 링크한다.
3. 여러 문서에 반복되는 내용은 한 문서에만 정의하고, 나머지는 링크한다.
4. 합의되지 않은 규칙은 문서에 쓰지 않는다. 미정인 항목은 "미정"으로 표시한다.
5. 새 문서를 추가하면 이 파일의 표에 등록한다.
6. `feature/` 문서 규칙은 [feature/README](feature/README.md#규칙)를 따른다.
