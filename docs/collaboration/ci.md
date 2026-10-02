# CI / 배포

## 로컬: Husky

| 훅 | 실행 |
| --- | --- |
| `pre-commit` | lint-staged — 스테이지된 파일에 `eslint --fix`, `prettier --write` |
| `commit-msg` | 커밋 헤더 정규식 검사 → [commit](commit.md#헤더) |

## GitHub Actions

환경: Node 24, pnpm → [tech-stack](../architecture/tech-stack.md)

| 잡 | 명령 | 실행 시점 |
| --- | --- | --- |
| lint | `eslint`, `prettier --check` | 모든 PR |
| type-check | `tsc --noEmit` | 모든 PR |
| build | `next build` | 모든 PR |
| test | `vitest run --passWithNoTests` (기존 테스트 전체) | 모든 PR |
| coverage | 커버리지 임계값 검사 | PR diff에 테스트 파일이 있을 때 → [test § 커버리지](../convention/test.md#커버리지) |
| Chromatic | 스토리 시각 비교 (TurboSnap) | `develop` 대상 PR → [test § Chromatic](../convention/test.md#chromatic) |
| E2E | Playwright + axe | 배포 전: `main` 대상 PR (`develop` → `main`, `hotfix/*` → `main`) |

- 실패한 잡이 있으면 머지할 수 없다. (branch protection의 required status checks)

## Vercel 배포

| 브랜치 | 환경 |
| --- | --- |
| `main` | Production |
| `develop` | Preview (고정 도메인) |
| PR | Preview (PR별 URL) |

## Discord 알림

| 이벤트 | 내용 |
| --- | --- |
| CI 실패 | 실패한 잡 이름 + 링크 |
| Production 배포 결과 | `main` 배포 성공/실패 |
| Sentry 에러 | 운영 에러 발생 (Sentry 알림 연동) → [analytics](../architecture/analytics.md) |
