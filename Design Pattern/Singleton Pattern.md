---
sticker: emoji//1f471
---
## What is Singleton Pattern
![[Pasted image 20231104221301.png]]
싱글톤 패턴은 하나의 클래스가 애플리케이션 전반에 걸쳐 하나의 인스턴스만 갖는 패턴입니다.
## Why we need Singleton Pattern
Singleton Pattern은 하나의 인스턴스를 전역적으로 공유할 수 있게 도와주며, 다음을 가능하게 합니다.
1. 애플리케이션에서 전역적으로 한가지 상태를 공유할 수 있습니다.
2. 인스턴스 생성에 많은 자원이 소비되는 경우 자원 절약이 될 수 있습니다.

### Disadvantage of Singleton Pattern
싱글톤 패턴은 전역적으로 하나의 인스턴스를 공유하기 때문에 테스트 코드를 만들기 어렵다는 단점이 있습니다. 각 테스트는 독립적으로 이뤄져야하는 반면 하나의 인스턴스를 공유하는 순간 각 테스트의 순서에 따라 테스트가 깨질 수 있기 때문입니다. 

## 7 Ways of How to make Singleton Pattern
Java를 사용하는 경우 싱글톤 패턴을 구현하는 방법이 여러가지입니다. 이를 하나씩 배우면서 멀티 스레드 환경에서 싱글톤을 활용시 주의사항에 대해 알아봅시다. 

##### 1. 단순한 메서드 호출
싱글톤 인스턴스를 생성하는 가장 기본적인 방법입니다. 싱글톤 인스턴스가 존재여부를 확인하고 싱글톤이 없다면 인스턴스를 생성하고 반환합니다.

```java
public class Singleton {  
	private static Singleton instance;

	private Singleton() { }

	public static Singleton getInstance() { 
		if (instance == null) {
			instance = new Singleton(); 
		}

		return instance; 
	}
}
```

자바스크립트였다면 이 방법이 괜찮을지 모르지만 자바의 멀티스레드 환경에서는 원자성이 결여된 방법이기 때문에 사용시 주의가 필요합니다. 

다음은 위 코드를 타입스크립트로 작성하면 다음과 같이 작성할 수 있습니다. 
```typescript
class Singleton {
    private static instance: Singleton;

    public static getInstance(): Singleton {
        if (!Singleton.instance) {
            Singleton.instance = new Singleton();
        }

        return Singleton.instance;
    }
}
```

##### 2. Synchronized
메서드 호출 방식을 멀티 스레드 환경에서 사용할때 발생하는 문제는 Synchronized 키워드로 해결할 수 있습니다. 
```java
public class Singleton {  
	private static Singleton instance;

	private Singleton() { }

	public static synchronized Singleton getInstance() { 
		if (instance == null) {
			instance = new Singleton(); 
		}

		return instance; 
	}
}
```
메서드를 반환하는 `getInstance` 메서드에 `synchronized`를 적용함으로써 최초로 메서드에 접근하는 스레드가 스레드가 접근하지 못하도록 잠금을 걸어줍니다. 
이 방법은 멀티스레드 환경에서 원자성을 보장할 수 있지만 메서드가 Lock되는 순간 다른 메서드의 대기 시간이 발생하므로 추천되는 방식은 아닙니다. 

##### 3. 정적 멤버
런타임이 아닌 최초 JVM이 클래스를 로딩하는 시점에 인스턴스를 생성하는 방법입니다. 
이 방법은 앞서 이야기했던 2가지 방법의 단점을 모두 해소할 수 있지만 싱글톤 인스턴스가 필요없는 상황에도 인스턴스를 생성하기 때문에 자원 낭비라는 단점을 갖고 있습니다.
```java
public class Singleton {  
	private final static Singleton instance = new Singleton(); 
	private Singleton() { }

	public static Singleton getInstance() { 
		return instance;
	} 
}
```

##### 4. 정적 블록
정적 멤버와 비슷하게 정적 블록을 활용하여 인스턴스를 사전에 생성할 수 있습니다. 
```java
public class Singleton {

	private static Singleton instance = null;
	
	static {  
		instance = new Singleton();
	
	}  
	private Singleton() { }
	
	public static Singleton getInstance() { 
		return instance;
	}
}
```
##### 5. 정적 멤버와 Lazy Holder(중첩 클래스)
클래스 내부에 클래스를 둠으로서 싱글톤 클래스가 최초 로드시 초기화 되지 않도록 방지하고, `getInstance`메서드가 호출되는 순간에 클래스가 인스턴스가 생성될 수 있도록 합니다. 
```java
class Singleton {  
	private static class singleInstanceHolder {
		private static final Singleton INSTANCE = new Singleton(); 
	}

	public static Singleton getInstance() { 
		return singleInstanceHolder.INSTANCE;
	} 
}
```
이 방법은 Java에서 가장 많이 사용되고 있다고 알려져 있습니다. 
##### 6. 이중 확인 잠금
volatile 키워드를 통해 캐시를 공유함과 동시에 인스턴스 생성 여부를 2중으로 체크하면 메서드 실행 잠금에 따른 병목 현상을 해결할 수 있습니다.
```java
public class Singleton {  
	private volatile Singleton instance; 
	private Singleton() { }

	public Singleton getInstance() { 
		if (instance == null) { // 최초 1번만 잠금
			synchronized (Singleton.class) {
				if (instance == null) {
					instance = new Singleton();
				} 
			}
		}

		return instance; 
	}
}
```

##### 7. Enum
enum의 인스턴스는 기본적으로 스레드 세이프한 점이 보장되기 때문에 이를 통해 인스턴스를 생성할 수 있습니다. 
```java
public enum SingletonEnum {
	INSTANCE;

	public void oortCloud() { }

}
```
이펙티브 자바를 저술한 조슈아 블로크가 이 방법을 사용하는 것이 가장 좋다고 말하던데...