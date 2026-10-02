# 성능

## 목표: Core Web Vitals "Good"

| 지표 | 의미 | 기준 |
| --- | --- | --- |
| LCP | 가장 큰 요소가 보이기까지 시간 | ≤ 2.5s |
| INP | 사용자 입력에 화면이 반응하기까지 시간 | ≤ 200ms |
| CLS | 로딩 중 레이아웃 밀림 정도 | ≤ 0.1 |

- 실사용자 수치는 Vercel Speed Insights로 측정한다. → [analytics](analytics.md)

## 규칙

| 규칙 | 내용 |
| --- | --- |
| 이미지 | `next/image`를 쓴다. 외부 이미지 도메인은 `next.config.ts`의 `images.remotePatterns`에 등록한다 |
| 폰트 | `next/font`를 쓴다. 외부 CDN 폰트 링크를 쓰지 않는다 |
| 동적 import | 첫 화면에 보이지 않는 무거운 클라이언트 컴포넌트(모달 내부 등)는 `next/dynamic`으로 불러온다 |

## 번들 분석

상시 규칙이 아니라 성능이 나빠졌을 때 쓰는 도구다. 도입 시 실행 방법을 이 섹션에 추가한다.
