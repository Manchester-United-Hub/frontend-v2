# 환경변수

## 파일

| 파일 | 용도 | 커밋 |
| --- | --- | --- |
| `.env.template` | 필요한 키 목록과 설명 (값은 비움) | O |
| `.env.local` | 로컬 개발 값 | X |

- 배포 환경의 값은 Vercel 대시보드에서 관리한다.
- `.env*` 파일은 프로젝트 루트에 둔다.
- `.gitignore`에 `!.env.template`를 추가해 템플릿만 커밋한다.

## 키

| 키 | 노출 | 용도 |
| --- | --- | --- |
| `API_BASE_URL` | 서버 전용 | 백엔드 주소. 서버 fetch와 rewrites 대상 |
| `SITE_URL` | 서버 전용 | `metadataBase`, sitemap 기준 URL → [seo-metadata](seo-metadata.md) |

## 브라우저 → 백엔드 호출

- 브라우저는 백엔드를 직접 호출하지 않는다. 같은 출처의 `/api/...`로 호출하고, `next.config.ts`의 `rewrites`가 `API_BASE_URL`로 전달한다.
- 따라서 백엔드 주소를 `NEXT_PUBLIC_`으로 노출하지 않는다.

## 접근 방식

- `f_shared/config/env.ts`에서 zod로 검증한 뒤 export한다.
- 코드에서 `process.env`를 직접 읽지 않는다.

## 키 추가 절차

1. `.env.template`에 키와 설명 추가
2. `f_shared/config/env.ts` 스키마에 추가
3. Vercel 환경변수에 등록
