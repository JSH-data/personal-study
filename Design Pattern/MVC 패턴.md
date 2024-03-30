---
sticker: lucide//layout-template
---
## What is MVC Pattern?
![[Pasted image 20231119153059.png]]
- MVC는 사용자 인터페이스, 데이터 및 논리 제어를 구현하는데 널리 사용되는 디자인 패턴입니다.
	- Model: 데이터와 비즈니스 로직을 관리합니다. 
	- View: 레이아웃과 사용자가 보는 화면을 관리합니다. 
	- Controller: Model과 View를 연결을 담당하며 모델, 뷰의 변경 통지를 받아 해석하고 각 구성요소에 변경내용을 전파합니다. 

## Why we need this?
1. 관심사 분리를 통해 독립적인 개발이 용이합니다. 
	- 역할별로 구성요소를 3가지 분리시켜놓았기 때문에 개발시 한 가지에 집중하여 개발할 수 있습니다. 

2. 재사용성 및 확장성이 용이합니다. 

## Disadvantage
1. View와 Model의 의존성이 높아질 수 있습니다.
	- 애플리케이션의 크기가 커질수록 모델과 뷰의 관계가 복잡해지는 단점이 있습니다. 

## Process
1. 사용자의 요청이 **Controller**에 들어옵니다.
2. Controller는 요청에 맞게 Model을 업데이트합니다.
3. Controller에서 업데이트된 Model을 나타내줄 View를 선택합니다.
4. View는 업데이트된 Model을 사용자에게 보여주기 위해 UI 데이터를 업데이트 합니다.

## Examples of MVC Pattern
- Spring은 아래 형식의 아키텍쳐를 갖고 있습니다, 이 중에서 Web 모듈이 MVC 패턴으로 구성되어 있습니다
	- Web Module: 멀티 파트 파일  업로드와 같은 웹 기능을 제공합니다. 
![[Pasted image 20231119145903.png]]
- Spring Web MVC 패턴은 **Dispatcher Servlet**의 사용자 요청 처리과정을 통해 알 수 있습니다. 
	- Dispatcher Servelet: 서블릿 컨테이너 가장 앞단에서 HTTP 프로토콜로 들어오는 모든 요청을 먼저 받아 적합한 컨트롤러에 위임해주는 프론트 컨트롤러
![[Pasted image 20231119151742.png]]
1. 클라이언트의 요청을 Dispatcher Servelet이 받습니다. 
2. Handler Mapping을 통해 요청에 알맞은 컨트롤러를 찾아냅니다. 
3. Handler Adaper를 통해 컨트롤러의 메서드를 실행합니다. 이 메서드를 통해 비즈니스 로직이 수행됩니다. 
4. 처리된 결과물인 모델을 Dispatcher Servelet에 전달합니다. 
5. View를 생성하기 위한 View Resolver 참고합니다. 
6. 사용자에게 VIew를 전달합니다. 