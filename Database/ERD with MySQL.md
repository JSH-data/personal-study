## What is ERD?
- 객체-관계 모델 (Entity-Relationship Modeling, E-R Modeling)은 세상의 사물을 개체 (Entity)와 개체 간의 관계 (Relationship)로 표현하는 데이터 모델링 방식으로 개념적 데이터 모델링 단계에서 사용됩니다.

### SQL을 통해 ERD 만들기

![[Screenshot 2023-12-05 at 1.39.50 AM.png]]
```SQL
CREATE TABLE `customers` (  
`customerNumber` int(11) NOT NULL,  
`customerName` varchar(50) NOT NULL,  
`contactLastName` varchar(50) NOT NULL, `contactFirstName` varchar(50) NOT NULL, 
`phone` varchar(50) NOT NULL,  
`addressLine1` varchar(50) NOT NULL,  
`addressLine2` varchar(50) DEFAULT NULL,  
`city` varchar(50) NOT NULL,  
`state` varchar(50) DEFAULT NULL,  
`postalCode` varchar(15) DEFAULT NULL,  
`country` varchar(50) NOT NULL,  
`salesRepEmployeeNumber` int(11) DEFAULT NULL, `creditLimit` decimal(10,2) DEFAULT NULL,  
PRIMARY KEY (`customerNumber`),  
KEY `salesRepEmployeeNumber` (`salesRepEmployeeNumber`), CONSTRAINT `customers_ibfk_1` FOREIGN KEY
(`salesRepEmployeeNumber`) REFERENCES `employees`
(`employeeNumber`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;
```

#### SQL 명령어
##### decimal
- 소수부분을 포함한 실수의 총자리수 정의할 수 있는 명령어
- ex) decimal(10, 2) = 소수부분을 포함한 실수의 총자리수 10자리, 2개의 소수를 가지는 실수.

#### 복합키
- 특정 데이터를 식별하는게 의미가 없는 도메인인 경우 후보키를 합쳐서 복합키를 구성하기도 합니다. 
![[Screenshot 2023-12-05 at 1.44.04 AM.png]]