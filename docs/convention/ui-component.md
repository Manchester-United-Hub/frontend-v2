# UI 컴포넌트

## shadcn/ui

- 원자 컴포넌트(버튼, 다이얼로그 등)는 shadcn CLI로 추가한다. 위치: `f_shared/ui/shadcn/` → [folder-structure](../architecture/folder-structure.md#f_sharedui)
- `f_shared/ui/shadcn/`의 파일은 수정하지 않는다.
- 디자인 변형이 필요하면 `f_shared/ui/`에 감싼 컴포넌트를 만들어 확장한다.

## props · export

- 네이티브 요소를 감싸는 컴포넌트는 해당 요소의 props를 확장한다: `interface ButtonProps extends ComponentProps<"button">`
- `className`을 받아 `cn()`으로 병합한다.
- named export만 쓴다. `export default`는 Next.js 특수 파일(`page.tsx` 등)에서만 쓴다.
- export하는 컴포넌트는 파일당 1개다.
- props 타입 이름은 `컴포넌트명Props`로 하고, 다른 파일에서 쓸 때만 export한다.
- `ref`는 일반 prop으로 받는다. `forwardRef`를 쓰지 않는다. (React 19)
- `useMemo`, `useCallback`을 수동으로 쓰지 않는다. (React Compiler가 처리)
- 상태를 어디에 둘지(`useState`, URL, Zustand 등)는 [state-management](../architecture/state-management.md)를 따른다.
- props 타입은 `interface`로 쓴다. 상태에 따라 props가 달라지는 union만 `type`으로 쓴다. → [typescript](typescript.md#type--interface)

### props 작성 예시

```tsx
import type { ComponentProps, ReactNode } from "react";
import type { VariantProps } from "class-variance-authority";

interface PlayerCardProps {
  player: Player;
  onPlayerSelect?: (playerId: string) => void;
}

interface BadgeProps extends ComponentProps<"span">, VariantProps<typeof badgeVariants> {}

interface SectionProps {
  title: string;
  children: ReactNode;
}

interface NavLinkProps extends Omit<ComponentProps<"a">, "href"> {
  href: string;
  isActive: boolean;
}

type ScoreBoardProps =
  | { status: "scheduled"; kickOffAt: string }
  | { status: "finished"; homeScore: number; awayScore: number };
```

- React 타입은 `React.` 네임스페이스 대신 `import type { ... } from "react"`로 가져온다.

## 오버레이: overlay-kit

관심사(modal, toast 등)별로 파일을 나누고, 컴포넌트는 관심사별 함수만 호출한다.

```
f_shared/lib/overlay/
├── modal.tsx    # openModal(), openConfirm() — shadcn Dialog 기반
└── toast.tsx    # showToast()
```

```tsx
const isConfirmed = await openConfirm({ title: "..." });
showToast({ message: "...", variant: "error" });
```

- 컴포넌트에서 `overlay.open`을 직접 호출하지 않는다.
- 위치·중복·닫힘 규칙은 관심사별 파일에서 관리한다.
- toast도 overlay-kit로 구현한다. (오버레이 방식 통일)
- 새 오버레이(bottom sheet 등)는 같은 폴더에 파일을 추가한다.

## 로딩 · 에러 경계: suspensive

- 데이터를 불러오는 블록 단위로 `ErrorBoundary` + `Suspense`를 감싼다. 한 블록이 실패해도 나머지는 보인다.
- 로딩 폴백은 블록 모양의 스켈레톤으로 만든다.
- 라우트 단위 처리는 [rendering § 로딩 · 에러](../architecture/rendering.md#로딩--에러) 참고.

## variant: cva + cn

- variant가 2개 이상인 컴포넌트는 `cva`로 정의한다.
- 클래스 병합은 항상 `cn()`을 쓴다. 문자열 템플릿으로 클래스를 합치지 않는다.
- boolean props 여러 개로 모양을 바꾸지 않는다: `isPrimary`, `isLarge` ✗ → `variant`, `size`

## 조건부 렌더링: ts-pattern

| 조건 | 방식 |
| --- | --- |
| 단순 참/거짓 | `&&`, 삼항 연산자 |
| 분기 3개 이상 또는 union 타입 | `match(...).with(...).exhaustive()` |

예시 (상태 값은 실제 스키마를 따른다):

```tsx
match(status)
  .with("scheduled", () => <KickOffTime />)
  .with("live", () => <LiveLink />)
  .with("finished", () => <Score />)
  .exhaustive();
```

## 애니메이션: motion

- 필요하다고 판단되면 자유롭게 쓴다.
- import는 `motion/react`에서 한다.
