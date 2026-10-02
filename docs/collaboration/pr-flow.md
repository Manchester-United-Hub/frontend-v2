# PR 플로우

브랜치 종류·이름·머지 방식은 [branch-strategy](branch-strategy.md)를 따른다.

## 기본 플로우

```
이슈 생성 → 작업 브랜치 생성 → 작업·커밋 → PR → CI + AI 리뷰 통과 → 머지
```

1. 이슈를 먼저 만든다. 이슈 없이 작업 브랜치를 만들지 않는다.
2. `develop`에서 작업 브랜치를 만든다: `feat/news-list-#12`
3. 커밋은 [commit](commit.md) 규칙을 따른다.
4. PR을 만든다. 제목은 커밋 헤더 형식과 같다 (squash 머지 시 커밋 메시지가 되므로).
5. CI와 AI 리뷰를 통과하면 작성자가 직접 머지한다. (1인 개발, 승인자 없음) → [code-review](code-review.md), [ci](ci.md)

## 템플릿

| 종류 | 파일 |
| --- | --- |
| PR | [`.github/pull_request_template.md`](../../.github/pull_request_template.md) |
| 이슈 (작업) | [`.github/ISSUE_TEMPLATE/progress.md`](../../.github/ISSUE_TEMPLATE/progress.md) |
| 이슈 (버그) | [`.github/ISSUE_TEMPLATE/bug.md`](../../.github/ISSUE_TEMPLATE/bug.md) |

- PR 크기 제한은 두지 않는다.

## stacked PR (새 기능의 첫 구현)

새 기능을 처음 구현할 때만 4단계로 나눈다. 이후 수정·버그는 단일 PR로 한다.

| 단계 | 내용 | 제목 예 |
| --- | --- | --- |
| 1/4 | 설계 문서 (`docs/feature/`) | `chore: news list design doc [1/4] #12` |
| 2/4 | UI 구현 | `feat: news list ui [2/4] #12` |
| 3/4 | 기능 구현 | `feat: news list data fetching [3/4] #12` |
| 4/4 | 테스트 작성 | `test: news list tests [4/4] #12` |

- `[n/4]`는 설명 뒤, 이슈 번호 앞에 붙인다. squash 커밋이 커밋 규칙을 그대로 통과한다.
- 각 단계는 앞 단계 브랜치 위에 쌓는다.
- 커버리지 검사는 테스트 파일이 있는 단계(4/4)부터 적용된다. → [test § 커버리지](../convention/test.md#커버리지)

### Graphite CLI (`gt`)

squash 머지 후 위 단계 브랜치를 다시 쌓는 작업(restack)은 `gt`로 처리한다.

| 명령 | 용도 |
| --- | --- |
| `gt create` | 현재 브랜치 위에 새 단계 브랜치 생성 |
| `gt submit --stack` | 스택 전체 PR 생성·갱신 |
| `gt sync` | 머지된 브랜치 정리 + 남은 브랜치 restack |

## 긴급 수정 (hotfix)

1. 이슈를 만들고 `main`에서 `hotfix/설명-#이슈번호` 브랜치를 만든다.
2. 수정에 필요한 최소 변경만 포함한다.
3. `main`으로 PR → 머지 후, `main` → `develop` PR로 같은 수정을 반영한다.
