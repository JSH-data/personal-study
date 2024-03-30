---
sticker: lucide//repeat-1
---
## What is MVP Pattern?
![[Pasted image 20231119153819.png]]
- MVC 패턴의 Controller가 **Presenter**로 변경된 패턴입니다. 
	- Presenter: Presenter는 View를 통해 사용자 액션을 전달받고 Model의 도움을 받아 처리된 결과를 다시 View로 전달합니다. 

## Why we need this?
- 단위 테스트가 용이합니다. 
	- VIew와 Presenter 사이의 의존 관계가 1:1로 설정되어 있기 의존 관계가 복잡한 MVC보다 테스트하기 용이합니다. 

## Disadvantage
- View와 Presenter의 너무 강한 의존성
	- 1:1로 View와 Presenter가 연결되기 때문에 서로 의존성이 강하게 연결되어 있습니다. 

## Process
1. 사용자의 Action은 View를 통해 들어오게 됩니다.
2. View는 데이터를 Presenter에 요청합니다.
3. Presenter는 Model에게 데이터를 요청합니다.
4. Model은 Presenter에게 요청받은 데이터를 응답합니다.
5. Presenter가 데이터를 가공하고 다시 View에게 응답합니다.
6. View는 Presenter로 부터 데이터를 응답받고 UI 데이터를 갱신합니다.