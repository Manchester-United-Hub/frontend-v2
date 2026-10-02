# 테스트

## 도구

| 도구 | 용도 | 파일명 |
| --- | --- | --- |
| Vitest | 단위·훅·컴포넌트 테스트 | `*.test.ts(x)` |
| Storybook + Chromatic | 공통 컴포넌트 시각 회귀 + 인터랙션(`play`) | `*.stories.tsx` |
| Playwright | E2E + 접근성 검사(axe) | `*.spec.ts` |
| MSW | API 모킹 (Vitest·Storybook·Playwright 핸들러 공유) | `[domain].ts` |

파일 위치는 [folder-structure § 테스트 위치](../architecture/folder-structure.md#테스트-위치)를 따른다.

## 대상

| 대상 | 도구 |
| --- | --- |
| `lib/` 순수 함수 | Vitest |
| `model/` 변환 함수 | Vitest — 입력은 실제 응답 형태의 fixture를 `schema.parse()`에 통과시킨 결과를 쓴다 (schema 단독 테스트는 작성하지 않는다) |
| 커스텀 훅 | Vitest (`renderHook`) |
| 공통 컴포넌트 (`f_shared/ui`) 인터랙션 | Storybook `play` 함수 (`@storybook/addon-vitest`로 Vitest에서 실행) |
| 그 외 인터랙션 컴포넌트 | Vitest + Testing Library |

## Chromatic

- PR마다 스토리 스크린샷을 `develop` 기준과 비교해 시각 변경을 감지한다. 변경은 Chromatic 화면에서 승인/거절한다.
- TurboSnap을 적용해 변경과 관련된 스토리만 촬영한다. (무료 플랜 월 5,000 스냅샷)
- `develop` 대상 PR에서만 실행한다.

## 작성 규칙

- `describe`는 대상 이름, `it`은 한국어로 작성한다: `it("score가 null이면 '-'를 반환한다")`
- 함수 사용 방식은 주석 대신 테스트로 설명한다. → [comment](comment.md)

## 커버리지

| 지표 | 기준 |
| --- | --- |
| `functions` | 80% 이상 |
| `branches` | 80% 이상 |

- 측정 범위: `develop` 대비 변경된 파일
- 제외: `app/`, `b_pages/` (async Server Component), `f_shared/ui/shadcn/`, `*.stories.tsx`, 타입 파일
- 미달 시 CI를 실패시킨다.
- PR diff에 테스트 파일(`*.test.ts(x)`)이 있을 때만 적용한다. (stacked PR의 테스트 단계 전에는 검사하지 않음)
- 테스트 실행 자체는 모든 PR에서 한다. → [ci](../collaboration/ci.md#github-actions)
