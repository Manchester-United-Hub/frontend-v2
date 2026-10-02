<!-- BEGIN:nextjs-agent-rules -->

# This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` (resolved from this file's directory; in monorepos the `next` package may not be visible from the repo root) before writing any code. Heed deprecation notices.

This block is written and re-added by `next dev` — verify at `node_modules/next/dist/server/lib/generate-agent-files.js`. Removing it from a diff only re-creates the uncommitted change; committing it with your work keeps the tree clean.

<!-- END:nextjs-agent-rules -->

# ManUHub frontend-v2

맨체스터 유나이티드 팬 정보 사이트 (경기 일정, 뉴스, 구단, 선수). → [overview](docs/architecture/overview.md)

이 파일은 인덱스다. 규칙은 `docs/`에 있다. 작업 전 아래 표에서 필요한 문서만 읽는다. 전체 목록은 [docs/README.md](docs/README.md).

## 작업별 문서

| 작업 | 읽을 문서 |
| --- | --- |
| 파일·폴더 위치 결정 | [folder-structure](docs/architecture/folder-structure.md), [naming](docs/convention/naming.md) |
| 컴포넌트 작성 | [rendering](docs/architecture/rendering.md), [ui-component](docs/convention/ui-component.md), [style](docs/convention/style.md), [accessibility](docs/convention/accessibility.md) |
| 타입 작성 | [typescript](docs/convention/typescript.md) |
| API 연동 | [data-flow](docs/architecture/data-flow.md), [query](docs/convention/query.md) |
| 상태 추가 | [state-management](docs/architecture/state-management.md) |
| 페이지 추가 | [routing](docs/architecture/routing.md), [seo-metadata](docs/architecture/seo-metadata.md) |
| 환경변수 추가 | [env](docs/architecture/env.md) |
| 라이브러리 추가 | [tech-stack](docs/architecture/tech-stack.md) |
| 테스트 작성 | [test](docs/convention/test.md) |
| 주석 | [comment](docs/convention/comment.md) |
| 커밋 | [commit](docs/collaboration/commit.md) |
| 브랜치·PR | [branch-strategy](docs/collaboration/branch-strategy.md), [pr-flow](docs/collaboration/pr-flow.md) |
| 리뷰 | [code-review](docs/collaboration/code-review.md) |
| CI·배포 | [ci](docs/collaboration/ci.md) |
| 페이지 기능 작업 | [feature/README](docs/feature/README.md) → `docs/feature/[page]/`의 최신 날짜 문서 |

## 문서 운영

[docs/README § 문서 운영 규칙](docs/README.md#문서-운영-규칙)을 따른다. 문서에 없는 규칙은 임의로 만들지 않는다.
