# 브랜치 전략

Git flow를 기반으로 한다. `release/*` 브랜치는 쓰지 않는다.

## 브랜치

| 브랜치 | 역할 | 분기 기준 | 머지 대상 |
| --- | --- | --- | --- |
| `main` | 운영 배포 | — | — |
| `develop` | 통합 | `main` | `main` |
| 작업 브랜치 | 기능·수정 등 일반 작업 | `develop` | `develop` |
| `hotfix/*` | 운영 긴급 수정 | `main` | `main` → 이후 `develop`에도 반영 |

- `main`, `develop`에 직접 push하지 않는다. 모든 변경은 PR로만 들어간다. (GitHub branch protection으로 강제, CI 통과 필수)

## 작업 브랜치 이름

형식: `접두사/설명-#이슈번호`

- 접두사는 커밋 타입과 같다: `feat`, `fix`, `style`, `refactor`, `test`, `chore` → [commit](commit.md)
- 설명은 영어 kebab-case로 쓴다.

```
feat/news-list-#12
fix/player-photo-broken-#31
hotfix/match-time-wrong-#40
```

## 머지 방식

| PR 방향 | 방식 |
| --- | --- |
| 작업 브랜치 → `develop` | Squash merge |
| `develop` → `main` | Merge commit |
| `hotfix/*` → `main`, `main` → `develop` | Merge commit |

- stacked PR의 squash 머지 후 처리는 [pr-flow](pr-flow.md)를 따른다.
