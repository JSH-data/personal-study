---
sticker: emoji//1f3ed
---
## What is Factory Method Pattern
![[Pasted image 20231111160606.png]]
- 팩토리 메서드 패턴은 객체 생성을 팩토리 클래스로 캡슐화 처리하여 대신 생성하게 하는 생성 디자인 패턴입니다. 사용자는 팩토리 클래스의 하위 클래스 생성 메서드를 통해 여러가지의 클래스 인스턴스를 생성할 수 있게 됩니다. 

## Why we need this?
- 팩토리 메서드 패턴을 사용하는 경우 다음과 같은 이점을 얻을 수 있습니다. 

1. **유연성이 증대됩니다.**
	상위 팩토리 클래스는 하위 클래스의 상세한 로직을 알필요가 없습니다. 따라서 어떤 클래스든 팩토리 클래스를 통해 생성할 수 있습니다. 

2. **유지보수가 용이해집니다.** 
	상위 클래스와 하위 클래스 사이의 결합도가 매우 낮기 때문에 각 로직의 수정이 비교적 자유롭습니다. 

3. **객체 생성 로직에 대한 공통 로직 추가가능**
	서로 관련이 없는 하위 클래스의 생성 시점에 동일한 로직을 추가시킬 수 있습니다. 

## What is Disadvantage
- 각 하위 클래스를 구현하기 때문에 구현해야하는 **서브 클래스가 늘어나면 관리가 어렵다**는 단점이 있을 수 있습니다. 

## Example
- 다음은 사용자가 원하는 타입의 커피를 생성할 수 있도록 팩토리 메서드를 활용하는 예시입니다. 
``` typescript
type ClassType = "LatteFactory" | "EspressoFactory";  
  
class CoffeeFactory {  
  static createCoffee(type: ClassType) {  
    const factory = factoryList[type];  
  
    return factory.createCoffee();  
  }  
}  

class Latte {  
  name: string;  
  
  constructor() {  
    this.name = "latte";  
  }  
}  

class Espresso {  
  name: string;  
  
  constructor() {  
    this.name = "Espresso";  
  }  
}  
  
class LatteFactory extends CoffeeFactory {  
  static createCoffee() {  
    return new Latte();  
  }  
}  

class EspressoFactory extends CoffeeFactory {  
  static createCoffee() {  
    return new Espresso();  
  }  
}  
  
const factoryList = {  
  LatteFactory,  
  EspressoFactory,  
};  
  
const main = () => {  
  const coffee = CoffeeFactory.createCoffee("LatteFactory");  
  
  console.log("coffee", coffee.name);  
  // coffee, latte
};  
  
main();
```

### Reference
[팩토리 메서드(Factory Method) 패턴 - 완벽 마스터하기](https://inpa.tistory.com/entry/GOF-%F0%9F%92%A0-%ED%8C%A9%ED%86%A0%EB%A6%AC-%EB%A9%94%EC%84%9C%EB%93%9CFactory-Method-%ED%8C%A8%ED%84%B4-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EB%B0%B0%EC%9B%8C%EB%B3%B4%EC%9E%90#%ED%8C%A8%ED%84%B4_%EB%8B%A8%EC%A0%90)
[팩토리 메서드 패턴](https://refactoring.guru/ko/design-patterns/factory-method)
