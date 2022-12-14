# Primary index vs. Secondary index

기본 인덱스와 보조 인덱스의 주요 차이점은 **중복 항목을 포함하지 않는 필드 집합의 인덱스**인 반면 보조 인덱스는 **기본 인덱스가 아니면 중복 항목을 포함할 수 있는 인덱스**라는 점이다.

인덱싱은 데이터베이스 성능을 최적화 하는 데 도움이 되는 프로세스이다. 쿼리를 처리하기 위한 디스크 액세스 수를 줄인다. 인덱스는 데이터ㅔ이스의 테이블에서 사용 가능한 데이터를 더 빠르게 찾고 액세스하는 데 사용되는 데이터 구조이다. 일반적으로 인덱스에는 검색 키와 데이터 참조의 두 섹션이 있다. 검색 키에는 테이블의 기본 키 또는 후보 키의 복사본이 포함된다. 정렬된 방식으로 저장되므로 데이터에 쉽게 엑세스할 수 있다. 데이터 참조에는 포이너가 포함되어 있다. 해당키에 해당하는 디스크 블록의 주소르 저장한다.또한 다양한 유형의 인덱싱 방법이 있는데 그 중 두 가지는 기본 및 보조 인덱스이다.

## 기본 인덱스

인덱스가 기본 키를 기반으로 하는 경우 이를 기본 인덱스라고 한다. 이러한 키는 각 레코드에 대해 고유하다. 또한 레코드 간의 1:1 관계를 포함한다. 기본 인덱스를 사용하여 데이터를 검색하는 것은 정렬된 순서로 데이터를 저장하기 때문에 효율적이다.

## 보조 인덱스

보조 인덱스는 다른 수준의 인덱싱을 도입하여 매핑 크기를 줄이는 데 도움이 되는 인덱스 유형이다. 초기 단계에서 열의 범위를 선택한다. 따라서 첫 번째 수준의 매핑 크기가 작아진다. 그런 다음 이 인덱스 방법은 각 범위를 더 작은 범위로 줄인다. 일반적으로 기본 메모리는 주소를 더 빨리 가져오기 위해 첫 번째 수준 매핑을 저장한다. 또한 보조메모리는 두 번째 수준의 매핑과 실제 데이터를 저장한다.

## 기본 인덱스와 보조 인덱스의 차이점

### 정의

기본 인덱스는 고유한 기본 키를 포함하고 중복을 포함하지 않도록 보장되는 일련의 필드에 대한 인덱스이다. 이에 반해 보조 인덱스는 기본 인덱스가 아닌 중복이 있을 수 있는 인덱스이다.

### 주문하다

기본 인덱스는 데이터 블록의 행이 인덱스 키에서 정렬되어야 하는 반면 보조 인덱스는 데이터 블록에서 행이 실제로 구성되는 방식에 영향을 미치지 않는다.

### 인덱스 수

또한 기본 인덱스는 하나만 있고 보조 인덱스는 여러 개 있을 수 있다.

### 중복

기본 인덱스에는 중복이 없지만 보조 인덱스에는 중복이 있을 수 있다.

## 결론

기본 인덱스와 보조 인덱스의 주요 차이점은 **기본 인덱스는 필드의 기본 키를 포함하고 중복 항목을 포함하지 않는 필드 집합의 인덱스**인 반면 **보조 인덱스는 기본 인덱스가 아닌 인덱스이며 중복을 포함할 수 있다**.
