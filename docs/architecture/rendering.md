# 렌더링

> Next.js API는 `node_modules/next/dist/docs/`를 기준으로 확인한다.

## Server / Client 경계

- 기본은 Server Component다.
- `"use client"`는 아래 트리거에 해당할 때만 붙이고, 컴포넌트 트리의 가능한 한 말단에 둔다.

### "use client" 허용 트리거

| 트리거 | 예 |
| --- | --- |
| React 상태·생명주기 훅 | `useState`, `useEffect` |
| 이벤트 핸들러 | `onClick`, `onChange` |
| 브라우저 전용 API | `window`, `IntersectionObserver` |
| 클라이언트 전용 훅·라이브러리 | TanStack Query 훅, `motion`, overlay-kit |

## 캐시: Cache Components

- `next.config.ts`에 `cacheComponents: true`를 켠다.
- 데이터 조회는 기본 동적이며, 캐시할 곳에만 `"use cache"`를 명시한다.
- 수명은 `cacheLife`, 태그는 `cacheTag`로 지정한다.

### 도메인별 캐시 수명

| 도메인 | 갱신 특성 | `cacheLife` |
| --- | --- | --- |
| match | 경기 종료 후 결과 반영, 일정 변경 시에만 바뀜 (진행 중 경기는 추후 중계 페이지에서 처리) | `"hours"` |
| news | | `"days"` |
| rank | | `"hours"` |
| player | | `"days"` |
| team | | `"days"` |
| season | | `"days"` |

## 서버 데이터 + TanStack Query

페이지네이션·더보기가 있는 목록(뉴스, 선수)은 서버 prefetch 후 클라이언트로 넘긴다.

```
page.tsx: prefetchQuery → dehydrate → <HydrationBoundary>
  └─ b_pages / 하위 Client Component: useQuery / useInfiniteQuery
```

- 첫 페이지는 서버에서 렌더링되어 검색엔진에 노출된다.
- 이후 페이지는 클라이언트에서 불러온다.

## 로딩 · 에러

| 범위 | 처리 |
| --- | --- |
| 컴포넌트 단위 로딩·에러 | suspensive (`Suspense`, `ErrorBoundary`) |
| 라우트 전체 실패 | `error.tsx` |
| 존재하지 않는 리소스 | `not-found.tsx` |
