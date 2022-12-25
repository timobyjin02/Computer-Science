## 해시

> **단방향 암호화 기법으로 해시함수를 이용하여 고정된 길이의 비트열로 변경한다.**
>
> - 단방향 암호화 기법 : 암호화는 수행하지만 복호화는 불가능한 알고리즘
>
> **_해시 함수_**
>
> **어떤 길이의 데이터를 입력해도 정해진 길이의 결과를 주는 함수**
>
> 이때 매핑 전 원래 데이터의 값을 키, 매핑 후 데이터의 값을 해쉬값, 매핑하는 과정을 해싱, 해시값 + 데이터색인 주소를 해시테이블이라고 한다.

## 해시함수 특징

1. 해시 함수는 동일한 입력값에 대한 동일한 출력값을 갖는다.
   1. 즉, 입력값이 바뀌지 않으면 출력값도 바뀌지 않는다.
2. 입력값이 아주 살짝 변경되어도 출력값은 어마어마하게 바뀐다. [눈사태 효과]
3. 항상 같은 방향, 일반향으로만 움직인다.
4. 복잡하지 않은 알고리즘으로 구현되기 때문에 상대적으로 CPU, 메모리 같은 시스템 자원을 덜 소모한다.

## 해시함수의 문제점

해시 함수의 특징 중 자원소모가 적어 처리속도가 빠르다고 했지만, 이건 장점이자 단점이다. 무차별 대입 공격을 받을 수 있기 때문이다

- 레인보우 테이블
  ⇒ 해시값을 입력값이랑 연결해놓은 테이블
  - 일반적으로 해시값을 보면 암호화가 되어서 비번을 알 수 없지만 해시값을 “레인보우 테이블” 에서 찾아보면 해쉬값을 알 수 있다.
    → 입력값이 바뀌지 않고 고정이기 때문에 해시값으로 입력값을 알 수 있다.4

### **해시 함수 문제점 해결**

그래서 “Salt” 즉, 랜덤 텍스트가 생겼다. 나중에 유저가 패스워드를 입력할 때 패스워드를 salt와 함께 해시하고 이는 랜덤한 값으로 이어지고 그걸 저장한다.

→ 해킹 불가~~~

## 해시 테이블

Key, Value로 데이터를 저장하는 자료구조 중 하나로 빠르게 데이터를 검색할 수 있는 자료구조이다. 해시 테이블이 빠른 검색속도를 제공하는 이유는 내부적으로 배열(버킷)을 사요아여 데이터를 저장하기 때문이다. 해시 테이블은 각각의 Key값에 해시함수를 적용해 배열의 고유한 index를 생성하고, 이 index를 활용해 값을 저장하거나 검색하게 된다. 여기서 실제 값이 저장되는 장고를 버킷 또는 슬롯이라고 한다.

![Untitled](https://user-images.githubusercontent.com/101804857/209458285-7408812a-8607-4628-b27c-b07c19dc0f10.png)

예를 들어 우리가 (Key, Value)가 (”John Smith”, “521-1234”)인 데이터를 크기가 16인 해시 테이블에 저장한다고 하자. 그러면 index = hash_function(”John Smith”) % 16 연산을 통해 index 값을 계산한다. 그리고 array[index] = “521-1234” 로 전화번호를 저장하게 된다.

이러한 해싱 구조로 데이터를 저장하면 Key값으로 데이터를 찾을 때 해시 함수를 1번만 수행하면되므로 매우 빠르게 데이터를 저장, 삭제, 조회할 수 있다.

그러나 데이터가 많아지면, 다른 데이터가 같은 해시 값으로 충돌나는 현상이 발생한다.

**“collision” 현상**

### **_그래도 해시 테이블을 쓰는 이유는?_**

적은 자원으로 많은 데이터를 효율적으로 관리하기 위해 하드디스크나, 클라우드에 존재하는 무한한 데이터들을 유한한 개수의 해시값으로 매핑하면 작은 메모리로도 프로세스 관리가 가능해진다.

- 언제나 동일한 해시값 리턴, index를 알면 빠른 데이터 검색이 가능해짐
- 해시테이블의 시간복잡도 O(1) - (이진탐색트리는 O(logN)

## 해시 충돌

“John Smith”를 해시 함수를 돌려 나온 값과 “Mang Kyu”를 해시 함수를 돌려 나온 값이 동일하다면 어떻게 해야 할까?

해시 테이블에서는 충돌에 의한 문제를 **분리 연결법(Separate Chaining)과 개방 주소법(Open Adressing)** 크게 2가지로 해결하고 있다.

### 분리 연결법

![Untitled (1)](https://user-images.githubusercontent.com/101804857/209458307-f0a488b0-a1e6-4846-94e6-78e466c8599f.png)

Separate Chaning이란 동일한 버킷의 데이터에 대해 자료구조를 활용해 추가 메모리를 사용하여 다음 데이터의 주소를 저장하는 것이다. 위의 그림과 같이 동일한 버킷으로 접근을 한다면 데이터들을 연결을 해서 관리해주고 있다.

이러한 Chaning 방식은 해시 테이블의 확장이 필요없고 간단하게 구현이 가능하며, 손쉽게 삭제 할 수 있다는 장점이 있다. 하지만 데이터의 수가 많아지면 동일한 버킷에 chaning되는 데이터가 많아지며 그에 따라 캐시의 효율성의 감소한다는 단점이 있다.

### 개장 주소법

Open Addressing이란 추가적인 메모리를 사용하는 Chaining 방식과 다르게 비어있는 해시 테이블의 공간을 활용하는 방법이다. Open Addressing을 구현하기 위한 대표적인 방법으로는 3가지 방식이 존재한다.

1. Linear Probing
   1. 현재의 버킷 index로부터 고정폭 만큼씩 이동하여 차례대로 검색해 비어 있는 버킷에 데이터를 저장한다.
2. Quadratic Probing
   1. 해시의 저장순서 폭을 제곱으로 저장하는 방식이다. 예를 들어 처음 충돌이 발생한 경우에는 1만큼 이동하고 그 다음 계속 충돌이 발생하면 2^2^, 3^2 칸씩 옮기는 방식이다.
3. Double Hashing Probing
   1. 해시된 값을 한번 더 해싱하여 해시의 규칙성을 없애버리는 방식이다. 해시된 값을한번 더 해싱하여 새로운 주소를 할당하기 때문에 다른 방법을보다 많은 연산을 하게 된다.

![Untitled (2)](https://user-images.githubusercontent.com/101804857/209458321-54f284c2-2898-4dbd-845d-10ef1e95a82c.png)

Open Addressing에서 데이터를 삭제하면 삭제된 공간은 Dummy Space로 활용되는데, 그렇기 때문에 Hash Table을 재정리 해주는 작업이 필요하다.