---
sticker: emoji//1f52c
---
## What is Observer Pattern
- 특정 객체의 상태 변화를 구독하고 있는 옵저버들에게 객체의 상태 변화가 발생할 때마다 알려주는 디자인 패턴입니다. ![[design-observer01.gif]]

## Why we need this
1. **상태 변경에 따라 다른 객체의 동작을 트리거 할 수 있습니다.** 
	객체간 의존성을 주입하지 않고도 이벤트를 주고 받을 수 있습니다. 

2. **객체간 느슨한 결합을 유지할 수 있습니다.**
	이벤트 전달 과정을 제외하고 서로 어떤 객체인지 알필요가 없습니다. 따라서 유지보수가 매우 용이합니다. 

## Disadvantage
1. **알람의 순서를 보장하기 어렵습니다.** 
	알림을 받는 옵저버들의 후속 조치 로직의 순서를 보장하기 어렵습니다.

2. **코드의 가독성이 낮아집니다.** 
	너무 다수의 관계가 설정되는경우 코드의 복잡도가 상승할 수 있습니다. 

3. **메모리 누수가 발생할 수 있습니다.** 
	구독을 해제하지 않는 경우 예기치 못한 메모리 누수가 발생할 수 있습니다. 

## Example
```typescript
interface Subject {  
  register(obj: Observer): void;  
  unregister(obj: Observer): void;  
  notifyObservers(): void;  
  getUpdate(obj: Observer): string;  
}  
  
interface Observer {  
  update(): void;  
}  
  
class Topic implements Subject {  
  observers: Observer[];  
  message: string;  
  
  constructor() {  
    this.observers = [];  
    this.message = "";  
  }  
  
  register(obj: Observer) {  
    if (!this.observers.includes(obj)) this.observers.push(obj);  
  }  
  
  unregister(obj: Observer) {  
    this.observers = this.observers.filter((observer) => obj !== observer);  
  }  
  
  notifyObservers() {  
    this.observers.forEach((observer) => observer.update());  
  }  
  
  getUpdate(obj: Observer): string {  
    return this.message;  
  }  
  
  postMessage(msg: string) {  
    console.log("Message sended to Topic: " + msg);  
    this.message = msg;  
    this.notifyObservers();  
  }  
}  
  
class TopicSubscriber implements Observer {  
  name: string;  
  topic: Subject;  
  
  constructor(name: string, topic: Subject) {  
    this.name = name;  
    this.topic = topic;  
  }  
  
  update() {  
    const msg = this.topic.getUpdate(this);  
    console.log(this.name + ":: got message >> " + msg);  
  }  
}  
  
class HelloWorld {  
  public static main() {  
    const topic = new Topic();  
    
    const a = new TopicSubscriber("a", topic);  
    const b = new TopicSubscriber("b", topic);  
    const c = new TopicSubscriber("c", topic);  
    
    topic.register(a);  
    topic.register(b);  
    topic.register(c);  
  
    topic.postMessage("amumu is op champion!!");  
  }  
}  
  
HelloWorld.main();  
  
/*  
Message sended to Topic: amumu is op champion!!  
a:: got message >> amumu is op champion!!  
b:: got message >> amumu is op champion!!  
c:: got message >> amumu is op champion!!  
*/
```