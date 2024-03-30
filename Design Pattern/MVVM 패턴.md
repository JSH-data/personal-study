---
sticker: emoji//1f195
---
## What is MVVM Pattern
![[Pasted image 20231119155409.png]]
- MVC의 C가 **ViewModel**으로 변경된 패턴입니다. 
	- ViewModel: View를 추상화한 계층으로 View의 이벤트를 통해 모델을 조작하고 전달하는 역할을 담당하고 있습니다. 

## Why we need this?
- 낮은 의존성
	- View와 VM은 의존관계가 1: n입니다. **데이터 바인딩**을 활용하면 이 둘의 의존관계를 상당히 줄일 수 있습니다.
		- 데이터 바인딩: 화면에 보이는 데이터와 브라우저 상의 메모리 데이터를 일치시키는 방법

## Disadvantage
- 구현이 어렵습니다. 
	- 데이터 바인딩, Observavle의 개념을 이해하고 VM을 직접 개발하는 것은 쉽지 않습니다. 

## Process
1. 사용자의 Action들은 View를 통해 들어옵니다.
2. View에 Action이 들어오면 ViewModel에 Action을 전달합니다.
3. ViewModel은 Model에게 데이터를 요청합니다.
4. Model은 ViewModel에게 요청받은 데이터를 응답합니다.
5. ViewModel은 응답 받은 데이터를 가공하여 저장합니다.
6. View는 Data Binding을 이용해 UI를 갱신시킵니다.

## Examples of MVVM Pattern
- Vue가 MVVM 패턴에 영감을 받아 개발된 가장 널리 알려진 웹 프레임워크입니다. 
![[Pasted image 20231119163736.png]]

- Vue는 위 그림과 같은 형식으로 디자인 되어있습니다. 일반 객체를 통해 모델을 등록하고 ViewModel을 두어 양방향 바인딩이 가능하도록 지원합니다. 