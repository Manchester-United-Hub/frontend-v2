# 라우팅

## 페이지 목록

| 페이지 | URL | 상태 |
| --- | --- | --- |
| 홈 | `/` | 구현 예정 |
| 경기 일정 | `/matches` | 구현 예정 |
| 뉴스 목록 | `/news` | 구현 예정 |
| 구단 정보 | `/club` | 구현 예정 |
| 선수 목록 | `/players` | 구현 예정 |
| 선수 상세 | `/players/[playerId]` | 구현 예정 |
| 시즌 (순위·득점·도움) | `/season` | 구현 예정 |
| 하이라이트 | `/highlights` | 추후 (YouTube 맨유 경기 하이라이트, 구현 계획 없음) |
| 404 | — | 구현 예정 (`not-found.tsx`) |

## ROUTE_PATHS

- 경로 문자열은 `ROUTE_PATHS` 한 곳에서만 정의한다. `href`, `router.push`, `redirect`에 문자열을 직접 쓰지 않는다.
- 내비게이션 메뉴 정보도 `ROUTE_PATHS`와 함께 한 곳에서 관리한다. 메뉴 컴포넌트에 링크를 하드코딩하지 않는다.
- 새 페이지를 만들면 같은 PR에서 `ROUTE_PATHS`에 추가한다.

위치: `f_shared/config/routes.ts` — 경로(`ROUTE_PATHS`)와 메뉴 배열(`NAVIGATION_ITEMS`)을 같은 파일에 둔다.

```ts
export const ROUTE_PATHS = {
  HOME: "/",
  MATCHES: "/matches",
  PLAYER_DETAIL: (playerId: string) => `/players/${playerId}`,
} as const;

export const NAVIGATION_ITEMS = [
  { label: "경기 일정", href: ROUTE_PATHS.MATCHES },
  { label: "뉴스", href: ROUTE_PATHS.NEWS },
];
```

- 동적 세그먼트가 있는 경로는 함수로 정의한다.
- 메뉴 순서는 `NAVIGATION_ITEMS` 배열 순서를 따른다.
