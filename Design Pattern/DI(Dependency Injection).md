---
sticker: emoji//1f489
---
## What is Dependency?
- 프로그래밍에서 의존관계란 다음을 의미합니다. 

>	*A가 B에 의존하는 경우 B가 변하면 A도 영향을 받는다.*

#### Example
- 다음은 메인 클래스 `Project`가 하위 프로젝트인 `Backend` , `Frontend`의 의존관계를 갖고 있는 예제입니다. 
```typescript
class Backend {  
  writeJava() {  
    console.log("Writing Java");  
  }  
}  
  
class Frontend {  
  writeJavascript() {  
    console.log("Writing Javascript");  
  }  
}  
  
class Project {  
  backend: Backend;  
  frontend: Frontend;  
  
  constructor(be: Backend, fe: Frontend) {  
    this.backend = be;  
    this.frontend = fe;  
  }  
  
  implement() {  
    this.backend.writeJava();  
    this.frontend.writeJavascript();  
  }  
}  
  
const project = new Project(new Backend(), new Frontend());  
  
project.implement();

// Writing Java
// Writing Javascript
```
## What is DI?
- 메인 모듈이 직접 다른 하위 모듈에 대한 의존성을 갖지 않고 외부의 의존성 주입자를 통해 의존관계를 결정하고 주입받는 것을 의미합니다. 
![[Screenshot 2023-11-11 at 8.26.19 PM.png]]
## Why we need this?
1. **유연한 구조를 가질 수 있습니다.**
	Dependecy Injector를 통해 의존관계를 주입 받기 때문에 메인 모듈과 하위 모듈의 결합도가 낮아지고 이를 통해 유지보수, 모듈 교체 등이 더 쉬워집니다. 

2. **더 쉬운 단위 테스팅이 가능합니다.** 

3. **코드 가독성 향상됩니다.** 

## Disadvantage
**1. 더 많은 코드를 작성해야합니다.**

**2. 디버깅의 난이도 상승합니다.**
	종속성이 실제로 주입되는 상황은 런타임 환경입니다. 컴파일 단계에서 사전에 에러를 차단하지 못하면 디버깅의 난이도가 올라갈 수 있습니다. 

### Example
- 위에서 보여준 의존관계를 DI를 통해 의존성을 해결한 예제입니다. 
```typescript
abstract class Developer {  
  abstract develop(): void;  
}  
  
class Backend extends Developer {  
  develop() {  
    this.writeJava();  
  }  
  
  writeJava() {  
    console.log("Writing Java");  
  }  
}  
  
class Frontend extends Developer {  
  develop() {  
    this.writeJavascript();  
  }  
  writeJavascript() {  
    console.log("Writing Javascript");  
  }  
}  
  
class Project {  
  developers: Developer[];  
  
  constructor(developers: Developer[]) {  
    this.developers = developers;  
  }  
  
  implement() {  
    this.developers.forEach((developer) => developer.develop());  
  }  
}  
  
const project = new Project([new Backend(), new Frontend()]);  
  
project.implement();
```

## What is DIP(Dependency Inversion principle)?
- **Robert Martin**에 의해 소개된 [[SOLID]] 원칙 중 한가지로 하위 레벨 묘듈의 변경이 상위 레벨 모듈까지 전파되는 구조적 문제에서 발생하는 위계 관계를 끊기 위한 원칙입니다. 의존성이 주입되는 경우 DIP가 적용되게 됩니다. 

- DIP에서는 다음 2가지 규칙을 지킵니다. 
	1. 상위 모듈은 하위 모듈에 종속되지 않고 추상화에 의존합니다.
	2. 추상화는 세부사항에 의존하지 않으며, 세부사항은 추상화에 의존합니다.

- React
https://fe-developers.kakaoent.com/2023/230330-frontend-solid/

