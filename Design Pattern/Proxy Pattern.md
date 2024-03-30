---
sticker: emoji//1f96a
---
## What is Proxy Pattern
- 객체에 접근하는 요청을 가로채서 접근에 대해 작업 처리를 진행함으로서 로직의 흐름을 제어하는 구조 패턴입니다.
![[design-proxy01.gif]]
## Why we need this
1. **보안 향상**
	올바른 접근인지 확인하고 아닌경우 접근을 제한할 수 있습니다.

2. **캐싱**
	프록시 내부 캐시를 통해 작업의 효율을 높일 수 있습니다. 

3. **로깅**
	접근에 대한 기록을 남겨 이슈를 트래킹 할 수 있도록 도울 수 있습니다. 

## Disadvantage
1. **별도의 작업량이 많아진다.**
	별도의 프록시 서버를 구축하거나 각 애플리케이션에 서로 다른 프록시가 필요한 경우 작업량이 많아질 수 있습니다. 

2. **프록시로 인해 병목현상이 발생할 수 있습니다.** 
	요청을 처리하는 과정에서 프록시에 자원이 쏠리면 서비스 응답시간이 지연될 수 있습니다. 

## JS의 프록시 패턴
- JS는 프록시 패턴이 적용된 [Proxy](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Proxy) 객체를 제공합니다. 이를 통해 객체에 접근하는 동작을 가로채 별도의 로직을 실행할 수 있습니다.  
```javascript
const target = {
  message1: "hello",
  message2: "everyone",
};

const handler = {
  get(target, prop, receiver) {
    if (prop === "message2") {
      return "world";
    }
    
    return Reflect.get(...arguments);
  },
};

const proxy = new Proxy(target, handler);

console.log(proxy.message1); // hello
console.log(proxy.message2); // world
```