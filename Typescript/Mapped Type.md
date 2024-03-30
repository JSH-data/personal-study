Mapped Type은 다른 타입을 기반으로 한 타입을 선언할 때 사용하는 문법인데, 인덱스 시그니처 문법을 사용해서 반복적 타입 선언을 효과적으로 줄일 수 있다.

##### 기본 개념 예시

```typescript
type Example = {
	a: number;
	b: number;
	c: number;
}

type Subset<T> = {
	[key in key of T]: T[Key]
}

const aExample: Subset<Example> = { a: 1 }

type ReadOnlyTypes = {
	readonly a?: number;
	readonly b?: string;
};

type CreateMutable<T> = {
	-readonly [K in keyof T]-?: T[K]
}
```

##### 실전 예시

```typescript
const BottomSheetMap = {
	a: someType,
	b: someType,
	c: someType
}

type BOTTOM_SHEET_ID = keyof typeof BottomSheet

type BottomSheetStore = {
	[index in BOTTOM_SHEET_ID as `${index}_NEW_NAME`]: {
		resolver?: () => void;
		args?: () => any;
		isOpened: () => boolean;
	}
}
// a,b,c에 필요한 자료를 직접 지정해줄 수 있습니다. 
```