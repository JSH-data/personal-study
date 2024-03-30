---
sticker: lucide//clipboard-signature
---
### 데이터 베이스의 기본 개념 용어

데이터 베이스를 더 잘 이해하기 위해서는 데이터베이스를 구성하는 다양한 개념들을 이해해야합니다. 다음은 데이터베이스를 구성하는 개념들입니다. 

### What is Entity
- **Entity** 는 사람, 장소, 물건 사건 등 여러 개의 속성을 지닌 명사를 의미합니다. 

### What is Relation
- 데이터베이스에서 정보를 구분하여 저장하는 기본 단위입니다. 
- 논리적인 개념인 **Entity**를 데이터베이스에 적용하면 **Relation**이 됩니다. 
- 관계형 데이터베이스에서는 **테이블**이라고 부르며, NoSQL 데이터베이스에서는 **컬랙션**이라고 불립니다. 

### Difference Between Collection and Table
- RDBMS의 Table, NoSQL의 Collection은 데이터베이스에서 담당하는 역할 측면에서는 비슷한 의미를 갖지만 그것들을 구성하는 요소 측면에서 바라보면 다른 점이 많습니다. 

|  RDBMS   |   NoSQL    |
|:--------:|:----------:|
| Database |  Database  |
|  Table   | Collection |
|  Record  |  Document  |
|  Column  |   Field    |

- 위 테이블은 위에서 아래로 향하며 하위가 상위를 이루는 구성요소를 나타냅니다.

### What is Attribute
- Relation에서 관리하는 구채적이고 고유한 이름을 갖는 정보입니다. 
- Entity를 이루는 속성이며 비즈니스 요구사항을 기반으로 관리해야할 필요가 있는 것들입니다. 

#### What is Domain
- Relation에서 포함된 각각의 속성들이 가질 수 있는 값의 집합을 의미합니다. 

#### Links
[[Components of Database]]




