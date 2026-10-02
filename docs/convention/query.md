# TanStack Query

서버 prefetch → HydrationBoundary 흐름은 [rendering § 서버 데이터 + TanStack Query](../architecture/rendering.md#서버-데이터--tanstack-query) 참고.

## QueryClient 기본값

- `staleTime: 60 * 1000` (60초). SSR prefetch 직후 클라이언트가 바로 다시 요청하지 않게 한다.

## queryOptions 팩토리

- 도메인별로 `e_entities/[domain]/model/[domain]Queries.ts`에 `queryKey`와 `queryFn`을 함께 정의한다.
- 서버 prefetch와 클라이언트 훅이 같은 팩토리를 쓴다.
- 호출부에서 `queryKey`, `queryFn`을 따로 조립하지 않는다.
- 키의 첫 요소는 도메인 이름이다: `["news", ...]`

## 목록 페이지네이션

| 목록 | API 방식 | UI | 훅 |
| --- | --- | --- | --- |
| 뉴스 | 커서 (`cursorAt`, `cursorId`, `size`) | 더보기 버튼 | `useInfiniteQuery` |
| 선수 | 페이지 번호 (`page`, `size`) | 페이지 번호 버튼 | `useQuery` |

### 뉴스: 커서 + 더보기

다음 커서는 응답의 `nextCursorAt`, `nextCursorId`를 쓴다.

```ts
export const newsQueries = {
  all: () => ["news"] as const,
  list: (size: number) =>
    infiniteQueryOptions({
      queryKey: [...newsQueries.all(), "list", size],
      queryFn: ({ pageParam }) => getNews({ ...pageParam, size }),
      initialPageParam: null,
      getNextPageParam: (last) =>
        last.nextCursorId ? { cursorAt: last.nextCursorAt, cursorId: last.nextCursorId } : undefined,
    }),
};
```

```tsx
await queryClient.prefetchInfiniteQuery(newsQueries.list(10));
const { data, fetchNextPage, hasNextPage } = useInfiniteQuery(newsQueries.list(10));
```

### 선수: 페이지 번호 + 필터

- `page`와 필터(`season`, `position`, `name`)의 위치는 [state-management](../architecture/state-management.md)를 따른다: `/players?position=Midfielder&page=2`
- 필터 값은 query key에 포함한다: `["player", "list", { season, position, name, page }]`
- 다음 페이지 여부는 응답의 `hasNext`, `totalPages`를 쓴다.
