#SQL DATABASE

##데이터베이스 만들기

``` CREATE DATABASE databasename; ```.  


##데이터베이스 삭제

```DROP DATABASE databasename;```.  


##데이터베이스 테이블 만들기

```
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
   ....
);
```

datatype 매개 변수는 열에서 보유 할 수있는 데이터 유형 (예 : varchar, 정수, 날짜 등)을 지정

<a href="https://www.w3schools.com/sql/sql_datatypes.asp">SQL종류별 데이터 유형</a>


##테이블 삭제
``` DROP TABLE table_name;```


##테이블의 열을 추가하거나 삭제하기

ALTER TABLE - 열 추가

	```
	ALTER TABLE table_name
	ADD column_name datatype;
	```

ALTER TABLE - DROP COLUMN
테이블의 열을 삭제하려면 다음 구문을 사용합니다 (일부 데이터베이스 시스템에서는 열 삭제가 허용되지 않음).

	```
	ALTER TABLE table_name
	DROP COLUMN column_name;
	```


## SQL 제약 조건 만들기
CREATE TABLE.으로 테이블이 작성 될 때 또는 ALTER TABLE.으로 테이블이 작성된 후에 제한 조건을 지정할 수 있습니다.

	```
	CREATE TABLE table_name (
	    column1 datatype constraint,
	    column2 datatype constraint,
	    column3 datatype constraint,
    	....
	);
	```

[일반적인 제약조건]

* NOT NULL - 열이 NULL 값을 가질 수 없음을 보장합니다.
* UNIQUE - 열의 모든 값이 서로 다른지 확인합니다.
* PRIMARY KEY - NOT NULL과 UNIQUE의 조합. 테이블의 각 행을 고유하게 식별합니다.
* 외래 키 - 다른 테이블의 행 / 레코드를 고유하게 식별합니다.
* CHECK - 열의 모든 값이 특정 조건을 충족하는지 확인합니다.
* DEFAULT - 값이 지정되지 않은 경우 열의 기본값을 설정합니다.
* INDEX - 데이터베이스에서 매우 신속하게 데이터를 생성하고 검색하는 데 사용합니다.	

## PRIMARY KEY
PRIMARY KEY 제약 조건은 데이터베이스 테이블의 **각 레코드를 고유하게 식별**합니다.
기본 키는 UNIQUE 값을 포함해야하며 NULL 값을 포함 할 수 없습니다.
테이블에는 기본 키가 하나만있을 수 있습니다. 기본 키는 하나 또는 여러 개의 필드로 구성 될 수 있습니다.

	```
	CREATE TABLE Persons (
	    ID int NOT NULL,
	    LastName varchar(255) NOT NULL,
	    FirstName varchar(255),
	    Age int,
	    PRIMARY KEY (ID)
	);
	```
	
이미 만들어진 테이블에 프라이머리 키 추가하기

	```
	ALTER TABLE Persons
	ADD PRIMARY KEY (ID);
	```

프라이머리 키 삭제

	```
	ALTER TABLE Persons
	DROP PRIMARY KEY;
	```

## FOREIGN KEY
foreign KEY 는 두 테이블을 서로 연결하는 데 사용되는 키입니다.
Foreign Key는 다른 테이블의 PRIMARY KEY를 참조하는 테이블의 필드 (또는 필드 모음)입니다.
Foreign Key가 들어있는 테이블을 하위 테이블이라고하고 후보 키가 들어있는 테이블을 참조 된 테이블 또는 상위 테이블이라고합니다.

	```
	CREATE TABLE Orders (
	    OrderID int NOT NULL,
	    OrderNumber int NOT NULL,
	    PersonID int,
	    PRIMARY KEY (OrderID),
	    FOREIGN KEY (PersonID) REFERENCES Persons(PersonID)
	);
	```

이미 만들어진 테이블에 포린 키 추가하기

	```
	ALTER TABLE Orders
	ADD FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);
	```

포린 키 삭제하기

	```
	ALTER TABLE Orders
	DROP FOREIGN KEY FK_PersonOrder;
	```

## 단일 colum의 제약조건 각각 달기
다음 SQL은 "Person"테이블이 작성되면 "Age"C 럼에 CHECK 제한 조건을 작성합니다. CHECK 제약 조건은 18 세 미만의 사람을 가질 수 없도록 보장합니다.

	```
	CREATE TABLE Persons (
	    ID int NOT NULL,
	    LastName varchar(255) NOT NULL,
	    FirstName varchar(255),
	    Age int,
	    CHECK (Age>=18)
	);
	```


이미 있는 테이블 안의 컬럼에 제약조건 추가하기

	```
	ALTER TABLE Persons
	ADD CHECK (Age>=18);
	```
	
컬럼 제약조건 삭제하기

	```
	ALTER TABLE Persons
	DROP CONSTRAINT CHK_PersonAge;
	```
	
##기본값 넣기

	```
	CREATE TABLE Persons (
	    ID int NOT NULL,
	    LastName varchar(255) NOT NULL,
	    FirstName varchar(255),
	    Age int,
	    City varchar(255) DEFAULT 'Sandnes'
	);
	```

이미 있는 테이블 안의 데이터 기본값 추가하기

	```
	ALTER TABLE Persons
	ALTER City SET DEFAULT 'Sandnes';
	```

##테이블 인덱스

	```
	CREATE INDEX index_name
	ON table_name (column1, column2, ...);
	```













	