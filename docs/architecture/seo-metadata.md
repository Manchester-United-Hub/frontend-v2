# SEO · 메타데이터

## title

- 형식: `페이지 | ManUHub` (예: `경기 일정 | ManUHub`)
- 루트 `layout.tsx`의 `title.template`으로 일괄 적용한다.
- 페이지 메타데이터는 `page.tsx`에서 정의한다. → [folder-structure § app/](folder-structure.md#app-nextjs-라우트)

## OG 이미지

| 범위 | 방식 |
| --- | --- |
| 전체 페이지 공통 | 기본 이미지 1장 |
| 선수 상세 (`/players/[playerId]`) | `opengraph-image.tsx`로 선수별 동적 생성 |

## sitemap · robots

- `app/sitemap.ts`, `app/robots.ts`를 둔다.
- sitemap에는 정적 페이지만 넣는다. (선수 상세 등 동적 페이지 제외)
- 페이지 목록은 [routing § 페이지 목록](routing.md#페이지-목록)을 따른다.

## 도메인

- 운영 도메인은 미정이다. 확정 전까지 Vercel 기본 도메인을 쓴다.
- `metadataBase`는 하드코딩하지 않고 환경변수로 주입한다. → [env](env.md)
