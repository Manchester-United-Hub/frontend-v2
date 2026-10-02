# 상태 관리

상태를 어디에 둘지에 대한 규칙은 이 문서에서만 정의한다. 다른 문서는 이 문서를 링크한다.

## 판단표

새 상태를 추가할 때 위에서부터 확인하고, 처음 해당하는 행을 따른다.

| 이 값은... | 둘 곳 | 작성법 |
| --- | --- | --- |
| 서버에서 온 데이터 | TanStack Query | [rendering](rendering.md#서버-데이터--tanstack-query), [query](../convention/query.md) |
| 공유·새로고침 시 유지돼야 함 (필터, 페이지) | URL `searchParams` | [query § 선수](../convention/query.md#선수-페이지-번호--필터) |
| 한 컴포넌트 안에서만 씀 | `useState` | — |
| props로 3단계 넘게 전달됨 | Zustand | 아래 "Zustand 스토어 위치" |

## Zustand 스토어 위치

- 스토어를 쓰는 슬라이스들의 가장 낮은 공통 슬라이스의 `model/`에 둔다.
- 여러 레이어에서 쓰면 `f_shared/model/`에 둔다.
