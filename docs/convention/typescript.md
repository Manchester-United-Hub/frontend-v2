# TypeScript

## type / interface

| 대상 | 사용 |
| --- | --- |
| 컴포넌트 props | `interface` |
| props가 union이어야 할 때 | `type` (예외) |
| 그 외 (데이터, `z.infer`, union, 유틸 타입) | `type` |
| 라이브러리 타입 확장 (declaration merging) | `interface` |

- props 작성 예시는 [ui-component § props 작성 예시](ui-component.md#props-작성-예시) 참고.

## enum

- TS `enum`을 쓰지 않는다. `as const` 객체 + 타입 추출을 쓴다.
- zod 스키마에서는 `z.enum`을 쓴다.

예시 (값은 실제 스키마를 따른다):

```ts
export const MATCH_STATUS = {
  SCHEDULED: "scheduled",
  FINISHED: "finished",
} as const;

export type MatchStatus = (typeof MATCH_STATUS)[keyof typeof MATCH_STATUS];
```

## 타입 안전

| 금지 | 대안 |
| --- | --- |
| `any` | `unknown`으로 받고 타입 가드·zod로 좁힌다 |
| `as` 타입 단언 (`as const` 제외) | 타입 가드, zod, `satisfies` |
| non-null 단언 `value!` | 명시적으로 확인한다 (`if (!value) ...`) |

- `satisfies`로 객체가 형식을 지키는지 검사한다: `ROUTE_PATHS`, cva variant 객체 등
- 타입만 가져올 때는 `import type`을 쓴다. (ESLint `consistent-type-imports`로 강제)
- `tsconfig.json`에 `noUncheckedIndexedAccess: true`를 켠다. 배열·객체 인덱스 접근 결과가 `T | undefined`가 된다.

## 반환 타입

- export하는 함수는 반환 타입을 명시한다.
- 파일 내부 함수는 추론에 맡긴다.
