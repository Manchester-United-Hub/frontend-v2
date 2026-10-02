# 개요

## 서비스

맨체스터 유나이티드 팬을 위한 정보 사이트.
경기 일정 조회를 중심으로 뉴스, 구단 정보, 선수 정보를 제공한다.
로그인/쓰기 기능 없이 공개 데이터를 조회만 한다.

## v2를 만드는 이유

개발 워크플로우를 바꾼다.

- v1: 하네스(전문 에이전트·스킬)를 구성해 맡기는 바이브코딩 형태
- v2: `docs/`에 결정 사항을 정리하고, 하네스 없이 문서를 기준으로 작성

따라서 v2에서는 **문서에 없는 규칙을 임의로 만들지 않는다.** 필요한 결정이 문서에 없으면 먼저 문서에 합의된 내용을 추가한다.

## 시스템 구성

```
[브라우저] → [Next.js 16 / Vercel] → [Spring Boot API / AWS]
```

- API 문서: https://www.manuhub.kro.kr/swagger-ui/index.html
- 모든 API는 GET이며 인증이 없다.
- 프론트는 Vercel에 배포한다. 트래픽이 커지면 호스팅 이전을 검토한다 (현재는 사이드 프로젝트 규모).

## 도메인

API 도메인을 그대로 문서·코드의 도메인 단위로 쓴다.

| 도메인 | 설명 | API |
| --- | --- | --- |
| match | 경기 일정·결과 | `GET /api/matches`, `GET /api/matches/{matchId}` |
| news | 뉴스 | `GET /api/news`, `GET /api/news/recent` |
| team | 구단 정보·전적 | `GET /api/teams/{teamId}`, `GET /api/team/statistics` |
| player | 선수 목록·상세·기록 | `GET /api/players`, `GET /api/players/{playerId}`, `GET /api/player-details/{playerId}` |
| rank | 리그 순위·득점·도움 순위 | `GET /api/rank/premier-league`, `.../topscorers`, `.../topassists` |
| season | 현재 시즌 | `GET /api/seasons/current` |

## 페이지

[routing § 페이지 목록](routing.md#페이지-목록) 참고.
