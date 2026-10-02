# 스타일

## 기본

- 스타일은 Tailwind CSS v4 유틸리티 클래스로 작성한다.
- Tailwind 설정은 `tailwind.config.*`가 아닌 `src/app/globals.css`의 `@theme`에서 한다.

## 디자인 토큰

- 색·폰트·간격 값은 `@theme` 토큰으로 정의하고, 클래스에서는 토큰만 쓴다.
- 임의값(`text-[#DA291C]`, `mt-[13px]`)을 쓰지 않는다. 필요한 값은 토큰으로 추가한다.
- 토큰 값은 디자인(`ds/*.css`)에서 가져온다.
- 토큰 이름은 색 이름이 아닌 역할 이름으로 짓는다: `--color-white` ✗ → `--color-background`, `--color-text-primary`

## 클래스 정렬

- `prettier-plugin-tailwindcss`로 자동 정렬한다. 손으로 정렬하지 않는다.
- `cn()`, `cva()` 안의 클래스도 정렬 대상이다.

## 반응형: mobile-first

- 접두사 없는 클래스 = 모바일. 큰 화면은 `md:`, `lg:` 등으로 덮어쓴다.
- breakpoint는 Tailwind 기본값을 쓴다.

| 이름 | 최소 너비 |
| --- | --- |
| `sm` | 640px |
| `md` | 768px |
| `lg` | 1024px |
| `xl` | 1280px |
| `2xl` | 1536px |

```tsx
<ul className="grid grid-cols-1 gap-4 md:grid-cols-2 lg:grid-cols-3" />
```

## 다크 모드

- 지금은 지원하지 않는다.
- 다크 시안이 생기면 시스템 설정(`prefers-color-scheme`) 방식부터 추가한다. 역할 이름 토큰에 다크 값 세트만 더하면 된다.
