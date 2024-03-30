템플릿 리터럴 타입은 JS의 템플릿 리터럴 문자열을 사용하여 문자열 리터럴 타입을 선언할 수 있는 문법입니다. 

##### 예시

```typescript
type Stage = 
	| "init"
	| "select"
	| "edit"

type StageName = `${Stage}-stage`
// "init-stage" | "select-stage" | "edit-stage"
```