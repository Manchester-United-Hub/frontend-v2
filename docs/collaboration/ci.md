# CI / 배포

## 로컬: Husky

| 훅 | 실행 |
| --- | --- |
| `pre-commit` | lint-staged — 스테이지된 파일에 `eslint --fix`, `prettier --write`<br>`vitest run --changed origin/develop` — `develop` 대비 변경 파일과 관련된 테스트만 실행 (`origin/develop`이 없으면 전체 테스트) |
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

Vercel의 Git 자동 배포는 끄고(`vercel.json`), GitHub Actions에서 Vercel CLI로 배포한다. (`.github/workflows/deploy.yml`)

| 트리거 | 환경 | 결과 |
| --- | --- | --- |
| `main` 머지 | Production | 운영 도메인 `manuhub-develop.vercel.app` |
| `develop` 머지 | Preview | 고정 도메인 `manuhub-preview.vercel.app` |
| `main`·`develop` 대상 PR | Preview | PR별 URL을 PR 댓글로 남긴다 (같은 댓글 갱신) |

- 순서: `vercel pull` → `vercel build` → `vercel deploy --prebuilt`
- `main`·`develop`은 ruleset으로 직접 push를 막아 두었으므로, 워크플로의 `push` 트리거는 PR 머지 때만 실행된다. 머지된 PR은 이미 CI를 통과했으므로 CI를 다시 돌리지 않는다.
- 같은 PR의 이전 배포는 취소한다. `main`·`develop` 배포는 취소하지 않고 순서대로 실행한다.
- 포크 PR은 시크릿이 없어 배포하지 않는다.
- 배포 환경변수는 Vercel 대시보드에서 관리한다. → [env](../architecture/env.md)

### GitHub Secrets

| 키 | 값 |
| --- | --- |
| `VERCEL_TOKEN` | Vercel Account Settings → Tokens |
| `VERCEL_ORG_ID` | `.vercel/project.json`의 `orgId` (`vercel link` 후) |
| `VERCEL_PROJECT_ID` | `.vercel/project.json`의 `projectId` |

## Discord 알림

| 이벤트 | 내용 |
| --- | --- |
| CI 실패 | 실패한 잡 이름 + 링크 |
| Production 배포 결과 | `main` 배포 성공/실패 |
| Sentry 에러 | 운영 에러 발생 (Sentry 알림 연동) → [analytics](../architecture/analytics.md) |
