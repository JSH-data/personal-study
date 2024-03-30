---
sticker: lucide//arrow-down-right-from-circle
---
## What is Flux Pattern
- Flux Pattern은 페이스북 컨퍼런스에서 발표된 아키텍쳐입니다. 
![[Pasted image 20231119170631.png]]
- 사용자 기반의 **Action**이 **Dispatcher**, **Store**, **Model**을 거쳐 View로 전달되는 단방향 흐름을 갖는 아키텍쳐 패턴입니다. 
	- Action: 사용자의 이벤트에 관한 객체입니다. 
	- Dispatcher: Action 객체 정보를 기반으로 어떤 행위를 할 것인지 결정하고 수행된 결과물을 Store에 전달합니다. 
	- Store: 애플리케이션의 상태를 관리하고 저장하는 계층입니다. 
	- View: 데이터 기반으로 표출되는 사용자 인터페이스입니다. 

## Why we need this?
- View와 Model의 강한 의존성 문제 해결
	- 애플리케이션의 크기가 비대해지는 경우 MVC 패턴의 문제점이 드러나게 됩니다. 연쇄적인 비동기 작업으로 인해 Model이 계속해서 업데이트 된다면 이에 따라 View가 새롭게 업데이트 됩니다. 이때 **의도치않게 View가 업데이트 되는 경우가 있을 수 있습니다.** 
	- Flux Pattern은 모든 요청이 단일 지점으로 향하고 View를 업데이트하기 때문에 View가 잘못된 업데이트를 하는 것을 방지할 수있습니다. 
![[Pasted image 20231119165712.png]]

## Disadvantage
- 불필요한 코드 작성의 증가
	- 데이터의 단방향 흐름 때문에 작성해야할 코드가 많습니다. (Action Creator, Dispatcher 등..)

## Process
1. 이벤트에 따라 Action객체를 생성합니다. 
2. Action 객체가 Dispatcher에 전달되어 Action 타입에 맞는 로직을 실행합니다. 
3. 결과물을 Store에 전달합니다. 
4. Store는 전달받은 결과를 토대로 상태를 업데이트합니다. 
5. 업데이트된 상태로 View가 업데이트 됩니다. 

## Example of Flux Pattern
- flux 아키텍쳐를 적용한 대표적인 사례로 Redux가 있습니다. 
![[Pasted image 20231119172405.png]]


## References
https://ggodong.tistory.com/263
https://ninefloor.tistory.com/105

## Links
- [[React]]
- [[What is Design Pattern]]

