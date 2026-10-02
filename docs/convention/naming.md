# 네이밍

## 파일

| 대상 | 규칙 | 예 |
| --- | --- | --- |
| 컴포넌트 파일 | PascalCase | `MatchCard.tsx` |
| 그 외 파일 (훅, 함수, 스키마 등) | camelCase | `useMatchFilter.ts`, `toMatch.ts` |
| Next.js 특수 파일 | 프레임워크 규칙 그대로 | `page.tsx`, `layout.tsx`, `not-found.tsx` |
| shadcn 생성 파일 (`f_shared/ui/shadcn/`) | CLI 생성 이름 그대로 (kebab-case) | `button.tsx`, `dropdown-menu.tsx` |

## 폴더

- camelCase: `e_entities/match`, `d_features/loadMoreNews`
- 레이어 폴더(`b_pages` 등)는 [folder-structure](../architecture/folder-structure.md#레이어) 규칙을 따른다.

## 상수 · 타입

| 대상 | 규칙 | 예 |
| --- | --- | --- |
| 전역 상수 | UPPER_SNAKE_CASE | `ROUTE_PATHS` |
| 타입 | PascalCase, `I`/`T` 접두사 금지 | `Match`, `MatchCardProps` |
| 서버 응답 타입 | `Dto` 접미사 | `MatchDto` |

## 이벤트: on- / handle-

- props로 받는 콜백: `on` + 대상 + 동작 → `onPlayerSelect`
- 컴포넌트 안에서 정의한 처리 함수: `handle` + 대상 + 동작 → `handlePlayerSelect`
- 연결: `<PlayerList onPlayerSelect={handlePlayerSelect} />`

## boolean: is- / has- / can-

| 접두사 | 쓰임 | 예 |
| --- | --- | --- |
| `is` | 상태·성질 | `isOpen`, `isLoading` |
| `has` | 소유·존재 | `hasNextPage` |
| `can` | 가능 여부 | `canLoadMore` |

- 부정형 이름을 쓰지 않는다: `isNotOpen` ✗ → `!isOpen`

## import

- 다른 레이어·슬라이스는 `@/` alias로 import한다: `@/e_entities/match/ui/MatchCard`
- 같은 슬라이스 안은 상대경로로 import한다.
- import 순서는 `@ianvs/prettier-plugin-sort-imports`로 자동 정렬한다. (외부 패키지 → `@/` → 상대경로)
- 배럴 금지 규칙은 [folder-structure § import 규칙](../architecture/folder-structure.md#import-규칙) 참고.
