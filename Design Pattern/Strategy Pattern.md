---
sticker: emoji//1f3b4
---
## What is Strategy Pattern?
- 전략 패턴은 런타임 환경에서 알고리즘 전략을 선택하여 객체 동작을 실시간으로 변경할 수 있게 만드는 패턴입니다. 
	- *전략이라는 단어의 의미는 알고리즘 혹은 특정 목표를 수행하기 위한 행동 계획을 캡슐화 시켜놓은 것입니다.*
![[Pasted image 20231114184938.png]]
## Why we need this
**1. 런타임 중 한 알고리즘을 전환할 수 있습니다.** 
	런타임 환경에서 알고리즘을 변경해야하는 일이 발생하는 경우 유연하게 변경할 수 있습니다. 

**2. 알고리즘 구현 정보를 고립시킬 수 있습니다.** 
	알고리즘의 세부 사항을 고립시켜 유지보수 및 테스트가 용이하도록 만들 수 있습니다. 또한 새로운 알고리즘의 추가가 용이합니다. 

## Disadvantage
**1. 불필요한 코드 생성**
	만약 알고리즘의 종류가 많지 않고 추가되는 상황이 없는 경우 많은 인터페이스와 클래스를 추가하는게 짐이 될 수 있습니다. 

**2. 함수형 프로그래밍으로 대체**
	함수형 프로그래밍을 지원하는 경우 일급함수를 통해 완벽히 대체할 수 있습니다. 
```javascript
const strategyA = () => {
	// 특정한 전략 A에 따른 실행 
}; 

const strategyB = () => { 
	// 특정한 전략 B에 따른 실행
}; // 컨텍스트 함수 

const context = (strategy) => { 
	return strategy(); 
}; // 사용 

context(strategyA); // 전략 A에 따른 실행 
context(strategyB); // 전략 B에 따른 실행
```

## Example

```typescript
interface PaymentStrategy {  
  pay(amount: number): void;  
}  
  
class KAKAOCardStrategy implements PaymentStrategy {  
  name: string;  
  cardNumber: string;  
  cvv: string;  
  dateOfExpiry: string;  
  
  constructor(nm: string, ccNum: string, cvv: string, expiryDate: string) {  
    this.name = nm;  
    this.cardNumber = ccNum;  
    this.cvv = cvv;  
    this.dateOfExpiry = expiryDate;  
  }  
  
  pay(amount: number) {  
    console.log(amount + " paid using KAKAOCard.");  
  }  
}  
  
class LUNACardStrategy implements PaymentStrategy {  
  emailId: string;  
  password: string;  
  
  constructor(email: string, pwd: string) {  
    this.emailId = email;  
    this.password = pwd;  
  }  
  
  pay(amount: number) {  
    console.log(amount + " paid using LUNACard.");  
  }  
}  
  
class Item {  
  name: string;  
  price: number;  
  
  constructor(name: string, cost: number) {  
    this.name = name;  
    this.price = cost;  
  }  
  
  getName(): string {  
    return this.name;  
  }  
  
  getPrice(): number {  
    return this.price;  
  }  
}  
  
class ShoppingCart {  
  items: Item[];  
  
  constructor() {  
    this.items = [];  
  }  
  
  addItem(item: Item): void {  
    this.items.push(item);  
  }  
  
  removeItem(item: Item): void {  
    this.items = this.items.filter((i) => i !== item);  
  }  
  
  calculateTotal(): number {  
    let sum = 0;  
    this.items.forEach((item) => {  
      sum += item.getPrice();  
    });  
  
    return sum;  
  }  
  
  pay(paymentMethod: PaymentStrategy) {  
    const amount = this.calculateTotal();
      
    paymentMethod.pay(amount);  
  }  
}  
  
class HelloWorld {  
  public static main() {  
    const cart = new ShoppingCart();  
  
    const A = new Item("kundolA", 100);  
    const B = new Item("kundolB", 300);  
  
    cart.addItem(A);  
    cart.addItem(B);  
  
    // pay by LUNACard  
    cart.pay(new LUNACardStrategy("kundol@example.com", "pukubababo"));  
    // pay by KAKAOBank  
    cart.pay(new KAKAOCardStrategy("Ju hongchul", "123456789", "123", "12/01"));  
  }  
}  
  
console.log(HelloWorld.main());  
  
/*  
400 paid using LUNACard.  
400 paid using KAKAOCard.  
*/
```
