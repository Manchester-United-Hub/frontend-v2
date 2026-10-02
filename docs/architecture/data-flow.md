# 데이터 흐름

## 백엔드 응답 형태

- API 문서: https://www.manuhub.kro.kr/swagger-ui/index.html
- 성공: 공통 래퍼(`{ data: ... }` 등) 없이 엔드포인트별 형태로 반환한다.
  - 예: `GET /api/news/recent` → `[{ id, title, link }]`, `GET /api/news` → `{ newsList: [...] }`
- 실패: HTTP 상태코드 + `{ code, message }` (예: 404 → `{ "code": "NOT_FOUND_ERROR", "message": "..." }`)

## 흐름

```
f_shared/api (fetch 래퍼)
  → e_entities/[domain]/api     호출
  → e_entities/[domain]/schema  zod로 서버 응답 검증 (DTO)
  → e_entities/[domain]/model   DTO → 화면용 타입 변환
  → ui
```

## Fetcher

- `f_shared/api`의 네이티브 `fetch` 래퍼 하나만 사용한다. 외부 HTTP 라이브러리를 쓰지 않는다.
- 도메인 코드에서 `fetch`를 직접 호출하지 않는다.

## 검증 · 변환

- `schema/`는 서버 응답을 **그대로** 검증한다. 검증에 실패하면 에러를 던진다.
- `model/`의 변환 함수가 DTO를 화면용 타입으로 바꾼다.
- 화면(`ui/`)은 변환된 타입만 사용한다.

## 에러 처리

| 상황 | 처리 |
| --- | --- |
| 404 (`NOT_FOUND_ERROR`) | `notFound()` → `not-found.tsx` |
| 그 외 API 에러 | ErrorBoundary 폴백 (재시도 버튼) |
| zod 검증 실패 | 에러로 처리 (위와 동일) |

- 화면 문구는 서버 `message`가 아닌 `code`를 기준으로 프론트에서 정한다.
