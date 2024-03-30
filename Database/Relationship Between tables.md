### How to express relationships between tables
- 테이블들의 관계를 효과적으로 표시하기위한 방법으로 [Crow Foor](https://en.wikipedia.org/wiki/Crow_foot)이 있습니다. 
![[Screenshot 2023-12-03 at 4.40.39 PM.png]]

#### Table's Keys
- 키는 테이블간의 관계를 명확하게 하고 테이블 자체의 인덱싱을 위해 설정된 장치입니다. 
	- 유일성 : 하나의 키값으로 튜플을 유일하게 식별할 수 있는 성질
	- 최소성 : 키를 구성하는 속성들 중 꼭 필요한 최소한의 속성들로만 키를 구성하는 성질
![[Pasted image 20231203172803.png]]
##### Primary Key
- 유일성과 최소성을 만족하는 키
##### Natural Key
- 중복되는 것을 제외하고 자연스럽게 뽑아 결정하는 기본키, 
- 시간에 흐름에 따라 변경될 수 있음
##### Artficial Key
- MySQL의 auto imcrement등 인조적으로 유일성을 확보하는 키입니다. 
- 기본키는 보통 인조키로 설정되는 경우가 많습니다. 
##### Foreign Key
- 다른 테이블의 기본키를 그대로 참조하는 키
- 외래키로 인해 테이블의 데이터를 간단하게 변경할 수 있습니다. 
##### Candidate Key
- 기본키가 될 수 있는 후보들이며 유일성과 최소성을 만족하는 키입니다. 
##### Alternate Key
- 후보키가 두개 이상인 경우 기본키로 지정되지 못하는 후보키를 의미합니다.
##### Super Key
- 각 레코드를 유일하게 식별할 수 있는 유일성을 갖춘 키
