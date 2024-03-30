---
sticker: emoji//267b-fe0f
---
## What is Iterator Pattern?
- Iterator를 통해 동일한 하나의 인터페이스로 컨테이너의 요소 타입과와 관계 없이 컨테이너를 순회할 수 있도록 만드는 패턴입니다. 
![[Pasted image 20231114184231.png]]
## Why we need this?
1. 어떤 타입의 컬랙션도 순회	
	Iterator 패턴을 활용하면 컬랙션이 갖고 있는 자료형에 관계 없이 순회할 수 있다는 장점이 있습니다. 

## Example
- 자바스크립트의 경우 Iterator 패턴을 직접 구현할 수 있게 도와주는 [Generator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Generator) 개념이 있습니다. 

```javascript
function* generator() {
  yield 1;
  yield 2;
  yield 3;
}

const gen = generator(); // "Generator { }"

console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // 3
```

- 또한 `for ... of` 문법을 통해 다양한 컬랙션의 순회가 가능합니다. 
```typescript
const map = new Map(...);
const set = new Set(...);
const arr = [...];

for(let [key, value] of map) {
	// 순회 가능
}

for(let x of set) {
	// 순회 가능
}

for(let x of arr) {
	// 순회 가능
}
```
