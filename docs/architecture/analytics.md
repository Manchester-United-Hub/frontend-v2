# 분석 · 모니터링

| 목적 | 도구 |
| --- | --- |
| 성능 (실사용자 Core Web Vitals) | Vercel Speed Insights → [performance](performance.md) |
| 사용자 행동 분석 | Google Analytics 4 |
| 에러 추적 | Sentry |

## Sentry

- 백엔드(Spring Boot)와 같은 Sentry 조직을 쓰고, 프로젝트는 frontend / backend로 나눈다.
- 분산 트레이싱으로 프론트 요청과 백엔드 처리를 연결한다. (`sentry-trace`, `baggage` 헤더가 rewrites 프록시를 거쳐 백엔드로 전달됨 → [env](env.md#브라우저--백엔드-호출))
- 무료 플랜의 에러 할당량을 두 프로젝트가 나눠 쓴다.
- zod 검증 실패도 Sentry에 기록된다. → [data-flow](data-flow.md#에러-처리)

## Google Analytics 4

- 페이지뷰 + 커스텀 이벤트(예: 더보기 클릭)를 수집한다.
- 수집할 커스텀 이벤트 목록은 미정이다.
