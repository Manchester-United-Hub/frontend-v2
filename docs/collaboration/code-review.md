# 코드 리뷰

1인 개발이므로 사람 승인 없이 **CodeRabbit 리뷰 + CI 통과** 후 작성자가 머지한다. → [pr-flow](pr-flow.md)

## 지적 처리 (심각도 기준)

| 지적 종류 | 처리 |
| --- | --- |
| 버그 | 반영 필수 |
| docs 규칙 위반 (아래 체크리스트) | 반영 필수 |
| 그 외 (개선 제안, 취향) | 선택 |

## 리뷰 체크리스트

CodeRabbit은 아래 항목을 기준으로 리뷰하고, 지적할 때 근거 문서를 함께 제시한다.

| 항목 | 근거 |
| --- | --- |
| FSD 레이어 방향, 같은 레이어 슬라이스 간 import, 배럴 파일 | [folder-structure](../architecture/folder-structure.md) |
| `"use client"`가 허용 트리거에 해당하는가 | [rendering](../architecture/rendering.md) |
| `fetch` 직접 호출, zod 검증 누락, 화면에서 DTO 직접 사용 | [data-flow](../architecture/data-flow.md) |
| 상태를 둔 위치가 판단표와 맞는가 | [state-management](../architecture/state-management.md) |
| 경로 문자열 하드코딩 (`ROUTE_PATHS` 미사용) | [routing](../architecture/routing.md) |
| `process.env` 직접 접근, 백엔드 주소 `NEXT_PUBLIC_` 노출 | [env](../architecture/env.md) |
| `next/image`·`next/font` 미사용 | [performance](../architecture/performance.md) |
| 파일·폴더·이벤트·boolean 이름 | [naming](../convention/naming.md) |
| `NOTE`/`TODO(#이슈)` 외 주석, JSDoc | [comment](../convention/comment.md) |
| `any`, `as` 단언, `!` 단언, props에 `type` 사용 | [typescript](../convention/typescript.md) |
| shadcn 원본 수정, `overlay.open` 직접 호출, `cn` 미사용 | [ui-component](../convention/ui-component.md) |
| Tailwind 임의값, 색 이름 토큰 | [style](../convention/style.md) |
| alt, 시맨틱 태그, 키보드 조작, `aria-label` | [accessibility](../convention/accessibility.md) |
| query key를 호출부에서 조립 | [query](../convention/query.md) |
| 필수 테스트 누락 | [test](../convention/test.md) |
| PR 제목·커밋 헤더 형식 | [commit](commit.md) |

## CodeRabbit 설정

- 저장소가 Public이므로 Pro 기능을 무료로 쓴다.
- 설정 파일: [`.coderabbit.yaml`](../../.coderabbit.yaml)
  - `AGENTS.md`, `docs/**/*.md`를 코딩 가이드라인으로 읽는다.
  - 지적에 `[버그]` / `[규칙 위반]` / `[제안]`을 붙이게 해 위 "지적 처리" 기준과 맞춘다.
  - 모든 base 브랜치 대상 PR을 리뷰한다. (stacked PR은 앞 단계 브랜치를 base로 하기 때문)
  - `pnpm-lock.yaml`, `f_shared/ui/shadcn/`(수정 금지 영역)은 리뷰에서 제외한다.
