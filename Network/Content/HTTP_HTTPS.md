- [HTTP](#HTTP란)
- [HTTPS](#HTTPS란)
- [HTTP vs. HTTPS](#HTTP와-HTTPS)

# HTTP란

> 데이터를 주고 받기 위한 프로토콜이다.

## 특징

### 1. OSI 7 계층 중, Application 계층의 프로토콜로 주로 TCP/IP 위에서 작동한다.

### 2. 서버/클라이언트 모델이다.

- Request Response 구조
- HTTP는 클라이언트가 서버에 요청을 하고, 서버는 그에 응답하는 단방향 모델이다.
- 클라이언트의 요청에 대한 서버의 응답은 요청 처리 결과에 따라 각기 다른 응답코드로 나뉜다.

![Untitled](https://user-images.githubusercontent.com/101804857/200470496-883de39f-0be2-408d-866c-01475e2dde66.png)

### 3. 전송되는 데이터들을 암/복호화 하지 않기 때문에 보안이 취약하다

- 제 3자가 데이터를 엿볼 가능성이 있다. 이를 보안하기 위한 것이 HTTPS이다.

### 4. 간단하다

- 초반 HTTP/1의 경우, 사람이 읽어도 이해가 가능할 정도로 간단하게 고안되었다. HTTP/2에서 binary 코드가 더해짐에 따라 더 복잡해지기는 했지만, 캡슐화를 통해 간결함을 유지하였다.

### 5. 확장 가능하다

- 클라이언트와 서버가 새로운 시멘틱에 대하여 합의만 한다면, 얼마든지 새로운 기능을 추가하여 확장하는 것이 어렵지 않다.

### 6. 비연결성

- 클라이언트와 서버가 한 번 연결을 맺은 후, 클라이언트 요청에 대해 서버가 응답을 마치면 맺었던 연결을 끊어 버리는 성질을 말한다
- 장점
  - HTTP는 인터넷 상에서 불특정 다수의 통신 환경을 기반으로 설계되었는데, 만약 서버에서 다수의 클라이언트와 계속 연결을 유지해야 한다면, 이에 따른 많은 리소스가 발생하게 된다. 따라서 연결을 유지하기 위한 리소스를 줄이면 더 많은 연결을 할 수 있다. ⇒ **접속 유지를 최소한으로 하되, 더 많은 유저의 요청을 처리할 수 있다**
- 단점
  - 서버는 클라이언트를 기억하지 못하므로 동일한 클라이언트의 모든 요청에 대해 매번 새로운 연결 시도/해제의 과정을 거쳐야 한다
    ⇒ **연결/해제에 대한 오버헤드(어떤 처리를 하기 위해 들어가는 간접적인 처리시간/메모리)가 발생**

![Untitled (1)](https://user-images.githubusercontent.com/101804857/200470610-47ed2d5f-5981-430c-a945-ff6227279dee.png)

### 7. 무상태성

> HTTP에서 서버가 클라이언트의 상태를 보존하지 않는 무상태 프로토콜이다. 간단한 예시를 들자면 클라이언트가 서버에게 ‘저녁에 치킨먹자’고 말했고 서버가 ‘그래’라고 답했다. 저녁이 되어 클라이언트는 서버에게 ‘먹으로 가자’고 말했고 서버는 대답했다. ‘뭘?’

- 비연결성으로 인해 파생된 특징. **연결이 끊어짐에 따라 서버는 클라이언트를 식별하지 못한다**.
- 서버는 클라이언트의 **상태를 저장하지 않는다**. → 클라이언트가 이전에 했던 요청과 그 다음 요청은 아무런 연관이 없다. 즉, **서버의 응답은 연속된 요청에 대해 각각 독립적으로 반응**한다.
- 장점
  - **서버 확장에 대한 부담이 적다** → 서버가 많아질수록 서버 간에 정보를 공유하기 위한 비용이 비싸지기에 무상태성을 사용하게 되면 정보 공유를 위한 비용등을 절약할 수 있다.
  - 어느 서버다 요청을 받아도 응답이 빠르게 가능하다
- 단점
  - HTTP 요청을 보낼 때마다 해당 요청을 처리하기 위한 **모든 데이터를 매번 보내야** 한다. → 이를 해결하기 위해 쿠키, 세션, JWT, OAuth를 활용하여 데이터를 처리한다.

![Untitled (2)](https://user-images.githubusercontent.com/101804857/200470709-d94361ac-3528-4b00-918f-db4d9f42e018.png)

# HTTPS란

> Hyper Text Transfer Protocol Secure의 약자이며 인터넷에서 통신할 때 사용되는 기본 HTTP 프로토콜의 보안 암호화 버전이다.

![Untitled](https://user-images.githubusercontent.com/101804857/200460734-b6e6cc98-7b62-4f38-b6c6-436b6329e2e3.png)

HTTPS는 사용자와 웹사이트 간에 전송될 때 민가만 데이터를 비공개로 유지하는 Hypertext Prootocol Secure의 약자이며 암호화 기술을 통해 승인된 당사자만 볼 수 있도록 한다.

HTTPS는 두 당사자 간에 데이터를 안전하고 비공개로 전송하는 방법이다.

## HTTP의 단점

HTTP는 웹을 지탱하는 심플한 기술이지만 단점이 있다. 브라우저와 웹 서버가 통신함에 있어서 주고 받는 **데이터가 암호화 되지 않고 그대로 전송** 되어진다.

![Untitled (1)](https://user-images.githubusercontent.com/101804857/200460882-5c4551b5-e604-4dc7-9f68-97bf431fc99b.png)

이러한 도청을 스니핑(sniffing)이라고 한다.

HTTP는 인터넷이라는 통로를 이용해 웹 서버와 브라우저가 서로 통신하게 해주므로, 해커가 그 중간 통로를 도청하게 된다면 중요한 정보들을 탈취할 수 있다.

## HTTPS 등장

HTTPS는 `SSL(Secure Socket Layer)` or `TLS(Transport Layer Security)`와 같은 프로토콜을 사용하여 공개키/개인키 기반으로 데이터를 암호화하고 있다. 데이터는 암호화되어 전송되기 때문에 임의의 사용자가 데이터를 조회하여도 원본의 데이터를 보는 것은 불가능하다.

- **SSL** (Secure Sockey Layer)
  - SSL은 보안 소켓 계층
  - 데이터를 안전하게 전송하기 위한 인터넷 암호화 통신 프로토콜
  - 전자상거래 등의 보안을 위해 넷스케이프에서 처음 만들었다
- **TSL** (Transport Layer Security)
  - SSL 이후에 이것을 표준화하여 만들어진 것이다
  - SSL/TSL로 함께 묶여 분류 된다

![Untitled (2)](https://user-images.githubusercontent.com/101804857/200461066-2e6649a5-b5e5-4a3a-b518-df645dacc67c.png)

HTTPS는 HTTP 통신을 함에 있어 데이터를 암호화 하여 통신한다. 따라서 중간에 통신을 도청 할지라도 내용을 알아볼 수 없다. 그러면 웹 서버에서는 브라우저에서 보내는 데이터 정보를 어떻게 알까 ?

## 암호화, 암호화 키(Key)

데이터 암호화에는 `키(Key)`가 필요하다. A와 B가 어떤 데이터에 대해서 똑같은 암호화 알고리즘을 사용한다면 같은 결과가 나올것이기에 어떤 암호화 알고리즘을 사용하는지만 알아낸다면 암호화된 데이터일지라도 쉽게 답을 유추할 수 있다. 그러나 암호화 키라는 변수를 두면 암호화 결과를 달라지도록 할 수 있어 데이터를 예측 할 수 없게 된다.

![Untitled (3)](https://user-images.githubusercontent.com/101804857/200461158-b319d169-3c2c-44dc-8a58-2def1e08675b.png)

암호화시 사용하는 암호화 키는 매우 중요하며 해커에게 노출되어서는 안된다. 그런데 중요한 점은 암호화된 데이처를 원래 데이터로 복호화 하는 과정에서도 키가 필요하다.

![Untitled (4)](https://user-images.githubusercontent.com/101804857/200461249-da17a89f-5cbc-4ae3-a8a5-25d99480f8b8.png)

따라서 암호화된 데이터를 주고 받기 이전에 통신할 대상과 키를 분배하여 공유해야 한다. 그런데 키를 공유하게 되면 키를 주고 받는 과정에서 해커에게 노출될 수 있다. 해커가 키를 가로챈다면 데이터를 암호화 하여 통신한다고 하여도 데이터를 마음대로 복호화하여 들어다 볼 수 있다. 그러면 그 키를 또 암호화해야 할까 ? 그러면 또 그 그에 대한 암호화 키가 필요하게 될 것이고 점점 복잡해질 뿐 해결책이 되지는 못한다. 그래서 SSL이라는 것이 등장한다.

## HTTPS 통신 과정

![Untitled (5)](https://user-images.githubusercontent.com/101804857/200461330-9ae48d8a-ff1d-4b17-8f0a-e79bd7251874.png)

HTTPS 통신 과정

1. 클라이언트에서 서버로 연결을 시도하는 패킷을 전송한다. Client가 사용가능한 Cipher suite 목록이 포함되어있다. 어떤 프로토콜(TLS/SSL)을 사용할지, 인증서 검증 또는 데이터를 어떤 방식으로 암호화할지 등이 표시된다.
2. 클라이언트에게서 받은 패킷에 대해 서버가 응답을 한다. 여기에는 클라이언트에게서 받은 Cipher suite 중 하나를 보낸다.
3. 2번 패킷 외에도 인증서에 대한 패킷을 보낸다. 인증서는 서버가 발급받은 SSL인증서를 말한다.
4. SSL 인증서에 서버의 공개키가 없는 경우 서버가 직접 공개키를 전달한다. 인증서에 공개키가 있는 경우 생략된다.
5. 인증서 확인
6. 서버가 행동을 마무리 했다고 응답을 보낸다.
7. 1, 2 단계에서 생성한 난수를 조합하여 pre-master-secret을 생성하고, 인증서 안에 들어있는 공개키를 이용하여 pre-master-secret 값을 암호화하여 서버로 전송한다.
8. 클라이언트로부터 전송받은 pre-master-secret를 서버는 자신의 비공개 키로 정상적으로 복호화 master-key(대칭키)로 승격 후 보안 파라미터를 적용하거나 변경될 때 보낸다.

위 과정을 통해서 대칭키와 암호화 방식으로 데이터를 송, 수신하게된다.

# HTTP와 HTTPS

![Untitled](https://user-images.githubusercontent.com/101804857/200467735-75ba5d0d-6f3d-4f84-8eee-caa82f0eba79.png)

두 프로토콜 사이에 가장 커다란 차이점은 SSL 인증서이다.

### HTTP의 문제점

- HTTP는 평문 통신이기 때문에 **도청이 가능**하다
- 통신 상대를 확인하지 않기 때문에 **위장이 가능**하다
- 완전성을 증명할 수 없기 때문에 **변조가 가능**하다

위 세가지는 다른 암호화하지 않은 프로토콜에도 공통되는 문제점들이다.

### TCP/IP는 도청 가능한 네트워크이다.

TCP/IP 구조의 통신은 전부 통신 경로 상에서 엿볼 수 있다. 패킷을 수집하는 것만으로 도청할 수 있다. 평문으로 통신을 할 경우 메시지의 의미를 파악할 수 있기 때문에 암호화하여 통신해야 한다.

**보안 방법**

1. 통신 자체를 암호화 `SSL(Secure Socket Layer)` or `TSL(Trans Layer Security)` 라는 다른 프로토콜을 조합합으로써 HTTP의 통신 내용을 암호화할 수 있다. SSL을 조합한 HTTP를 `HTTPS(HTTP Secure)` or `HTTP over SSL`이라고 부른다.
2. 콘텐츠를 암호화 말 그래도 HTTP를 사용해서 운반하는 내용인, HTTP 메시지에 포함되는 콘텐츠만 암호화하는 것이다. 암호화해서 전송하면 받은 측에서는 그 암호를 해독하여 출력하는 처리가 필요하다.

### 통신 상대를 확인하지 않기 때문에 위장이 가능하다.

HTTP에 의한 통신에는 상대가 누구인지 확인하는 처리는 없기 때문에 누구든지 request를 보낼 수 있다. IP 주소나 포트 등에서 그 웹 서버에 액세스 제한이 없는 경우 reauest가 오면 상대가 누구든지 무언가의 response를 반환한다. 이러한 특징은 여러 문제점을 유발한다.

1. request를 보낸 곳의 웹 서버가 원래 의도한 response를 보내야 하는 웹 서버인지를 확인할 수 없다.
2. response를 반환한 곳의 클라이언트가 원래 의도한 request를 보낸 클라이언트인지를 확인할 수 없다.
3. 통신하고 있는 상대가 접근이 허가된 상대인지를 확인할 수 없다.
4. 어디에서 누가 request 했는지 확인할 수 없다.
5. 의미없는 request도 수신한다. → DoS 공격을 방지할 수 없다.

**보안방법**

위 암호화 방법으로 언급된 `SSL`로 상대를 확인할 수 있다. SSL은 상대를 확인하는 수단으로 **증명서**를 제공한다. 증명서는 신뢰할 수 있는 **제 3자 기관에 의해** 발행되는 것이기 때문에 서버나 클라언트가 실재하는 사실을 증명한다. 이 증명서를 이용함으로써 통신 상대가 내가 통신하고자 하는 서버임을 나타내고 이용자는 개인 정보 누설 등의 위험성이 줄어들게 된다. 한 가지 이점을 꼽자면 클라이언트는 이 증명서로 본인 확인을 하고 웹 사이트 인증에서도 이용할 수 있다.

### 완전성을 증명할 수 없기 때문에 변조가 가능하다.

여기서 완전성이란 **정보의 정확성**을 의미한다. 서버 또는 클라이언트에서 수신한 내용이 송신측에서 보낸 내용과 일치한다라는 것을 보장할 수 없는 것이다. request나 response가 발신된 후에 상대가 수신하는 사이에 누군가에 이해 변조되더라도 이 사실을 알 수 없다. 이와 같이 공격자가 도중에 request나 reaponse를 빼앗아 변조하는 공격을 중간자 공격(Main-in-Middle)이라고 부른다.

**보안 방법**

`MDS`, `SHA-1` 등의 해시 값을 확인하는 방법과 파일의 디지털 서명을 확인하는 방법이 존재하지만 확실히 확인할 수 있는 것은 아니다. 확실히 방지하기에 `HTTPS`를 사용해야 한다. SSL에는 인증이나 암호화 그리고 다이제스트 기능을 제공하고 있다.

- 다이제스트 기능
  - 일반적으로 사용자가 입력한 비밀번호는 암호화 해시 함수를 거쳐 다이제스트(Digest)의 형태로 저장된다. 여기서 다이제스트란, 해시 함수라는 수학적인 연산을 통해 생성된 암호화된 메세지를 의미한다.

### 키워드

1. **인증서와 CA(Certificate authority)**

SSL을 적용하기 위해서는 인증서라는 것이 필요하다.

인증서의 내용은 크게 2가지로 구분할 수 있다.

- 서비스의 정보 (CA, 도메인,,,)
- 서버 측의 공개키 (공개키의 내용, 공개키의 암호화 방식)

![Untitled](https://user-images.githubusercontent.com/101804857/201476218-b17e0ddc-c731-4638-8102-3f539a360e70.png)

이 인증서를 발급해주는 기업을 CA라고 한다. 인증서가 보안에 관련된 것인 만큼 CA는 영향력이 있고 신뢰할 수 있는 기업에서만 가능하다.

2. [대칭키와 공개키](https://github.com/timobyjin02/Computer-Science/blob/main/Network/Content/%EB%8C%80%EC%B9%AD%ED%82%A4%EC%99%80%EA%B3%B5%EA%B0%9C%ED%82%A4.md)
