# 폴더 구조

FSD(Feature-Sliced Design)를 따른다. 레이어 폴더에 알파벳 접두사를 붙여 의존 방향을 이름 순서로 드러낸다.

## 레이어

```
src/
├── app/          # Next.js 라우트 + FSD app 레이어 (전역 providers, 전역 스타일)
├── b_pages/      # 페이지 단위 조합
├── c_widgets/    # 여러 entity/feature를 조합한 큰 UI 블록
├── d_features/   # 사용자 행동 단위 (더보기, 필터 등)
├── e_entities/   # 도메인 (match, news, team, player, rank, season)
└── f_shared/     # 도메인을 모르는 공용 코드
```

- 상위 레이어는 하위 레이어만 import한다. (`app` → `b_pages` → `c_widgets` → `d_features` → `e_entities` → `f_shared`)
- `app/`은 Next.js 라우팅 폴더이므로 접두사를 붙이지 않는다.
- 같은 레이어의 다른 슬라이스는 import하지 않는다. (예: `e_entities/match` → `e_entities/team` 금지) 함께 필요하면 상위 레이어에서 조합한다.
- `e_entities`의 슬라이스는 [overview § 도메인](overview.md#도메인)의 도메인과 1:1로 맞춘다.

## app/ (Next.js 라우트)

`page.tsx`, `layout.tsx`는 라우트 관심사만 다루고, 화면은 `b_pages`에 맡긴다.

| `page.tsx`에서 하는 일 | `b_pages`에서 하는 일 |
| --- | --- |
| `params` / `searchParams` 처리 | 화면 구성 (widgets/features/entities 조합) |
| `generateMetadata` | |
| 데이터 prefetch | |
| 결과를 props로 `b_pages`에 전달 | |

## f_shared/ui

- shadcn/ui가 생성한 컴포넌트: `f_shared/ui/shadcn/` (`components.json`의 alias를 이 경로로 설정)
- 직접 만든 공용 컴포넌트: `f_shared/ui/`

## 세그먼트

슬라이스 안은 아래 세그먼트로 나눈다. 필요한 것만 만든다.

| 세그먼트 | 내용 |
| --- | --- |
| `ui/` | 컴포넌트 |
| `api/` | API 호출 함수 |
| `schema/` | zod 스키마 + `z.infer` 추론 타입 |
| `model/` | 화면에서 쓰는 타입, 변환, query key |
| `lib/` | 슬라이스 전용 유틸 |
| `config/` | 슬라이스 전용 상수 |

```
e_entities/match/
├── ui/
├── api/
├── schema/
├── model/
└── lib/
```

## Zustand 스토어 위치

[state-management § Zustand 스토어 위치](state-management.md#zustand-스토어-위치) 참고.

## import 규칙

- 배럴(`index.ts` re-export) 파일을 만들지 않는다.
- 파일 경로로 직접 import한다: `import { MatchCard } from "@/e_entities/match/ui/match-card"`

## 테스트 위치

Vitest 테스트는 루트 `__tests__/`에 `src/`와 같은 구조로 둔다.

```
src/e_entities/match/model/to-match.ts
__tests__/e_entities/match/model/to-match.test.ts
```

| 종류 | 위치 |
| --- | --- |
| Playwright E2E | 루트 `e2e/` |
| Storybook 스토리 | 루트 `stories/` (src 미러링) |
| MSW 핸들러·fixture | 루트 `mocks/handlers/`, `mocks/fixtures/` |
