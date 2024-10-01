# HTTP에 대한 필수 지식 

작성자 : 프람

## 서론

최근 프로젝트를 진행하다 보니,광범위한  HTTP 프로토콜에 대한 낮은 이해도와 서로 다른 의견에 따른 마찰이 자주 생김을 느꼈다.
그래서 보다 나은 HTTP API 명세법과 자주 발생할 수 있는 문제들을에 대해 자세하게 알아보도록 한다. 

이 글은 HTTP에 대한 깊은 학습보다는 웹 애플리케이션을 개발하면서 필수적인 기반 지식과 초보자가 접할 수 있는 오류들에 대해 집중적으로 다룬다.

### 1.1 HTTP 란?
HTTP란 HyperText Transfer protocol의 약자로, HyperText를 전송하는 통신규약을 말한다.
HyperText는 문서 내에서 특정 단어가 다른 문서나 시스템으로 연결 되어 있는 것이라보면 된다. 
즉, ‘링크가 걸린 문서의 전송 규칙'에 대해 알아보는 것이 목표이다.

### 1.2 초기 HTTP의 역사
HTTP는 1991년 HTTP 버전 0.9를 시작으로 현재는 3.0까지 여러 버전을 거치면서 발전을 해왔다.
초기 HTTP발전 양상을 보면  자연스럽게 당시 시대상이 이해될 것이다.

HTTP의 첫은 등장은 W3에서 문서 전송을 위해서이다.
1989년 유럽 입자 물리학 연구소에서 구성원 간의 문서 공유에 어려움을 느끼고 효율적인 문서 공유를 위해 논의 되었고 팀 버너스 리가 발명하였다. 
첫 HTTP는 W3에서 효율적인 하이퍼 텍스트의 전송의 목적으로 나왔다. 따라서 당시 팀 버너리스는 기본적인 URL 구문과 기초적인 HTML의 형식을 만들었다.

1991년 HTTP의 첫 문서화 버전인 [HTTP 0.9](https://www.w3.org/Protocols/HTTP/AsImplemented.html)가 등장하였다.
HTTP의  등장 배경에서 알 수있듯 0.9버전 문서 전달을 주 목적으로 GET를 통한 문서 조회 기능만을 제공했다.  

1996년 W3의 큰 수요으로 인해 팀 버너리스 리는[HTTP 1.0](https://datatracker.ietf.org/doc/html/rfc1945)를 발표하게된다. 
이 때는 POST, HEAD 메서드의 추가 지원과 상태 코드 및 해더가 등이 등장한다.
이를 통해 HTTP는 당시 급격하게 늘어나는 W3의 수요에 대응하듯 범용적인 사용을 가능하도록 기능들을 확장해나갔다.

1997년 [HTTP 1.1](https://datatracker.ietf.org/doc/html/rfc2616)이 다시 발표되는 된다.
HTTP 1.0에서는 대용량 트래픽에 대한 캐싱 전력과 비효율적인 HTTP연결 과정에 대한 문제가 대두 된다.
이를 해결하기 위해 HTTP 1.1에서는 더욱 세분화된 캐싱 전략 지원, 지속연결과 파이프-라이닝 매커니즘을 도입하였다. 

문서 공유의 어려움을 인한 HTTP의 첫 발명, 그리고 W3의 큰 발전으로 인한 대용량 트래픽을 처리하기 하기 위한 HTTP1.1까지 1990년대의 W3의 등장과 고속성장을  엿볼 수 있다.

HTTP 2.0 과 HTTP3.0에 대해서는 언급하지 않겠지만, 이도 비슷하게 시대의 요구에 맞게 발전되어가고 있다.

### 1.3  HTTP에 대한 기본 이해

HTTP에 대한 본격적인 내용을 다루기전 HTTP의 기본이 되는 2가지 틀에 대해 알아본다. 

첫 째 ,HTTP는 서버-클라이언트 모델이다.
앞서 설명했듯이, HTTP는 효율적인 문서 관리를 위해 등장하였다.
누군가는 문서를 요청하고 서버는 요청된 문서를 응답하는 식이다.
즉, 누군가 요청을 하면 누군가는 응답하는 형식이다. 
요청을 보내는 쪽을 클라이언트라하고 요청을 받고 응답을 주는 곳을 서버라 한다.


둘 째, HTTP는 상태를 가지지 않는다.
HTTP의 무상태 특징은 클라이언트에 대한 정보에 해당한다. 
서버는 클라이언트에 대한 정보를 저장하지 않는다. 서버가 여러 클라이언트에 대한 요청을 처리할 때, 
모든 클라이언트의 요청 기록이나 정보들을 저장하게 된다면 엄청난 부하가 올것이다. 
이를 방지하고 구조의 단순화를 위해 HTTP는 Stateless하게 설계되었다.


## HTTP의 주요 구성 개념
### 2.1 URI 와 URL
결론부터 말하자면, URI와 URL는 개념적으로 유의미한 차이는 없다. 
URI는 HTTP의 자원 식별자에 해당한다. URL 역시 HTTP에서 자원을 식별하기 위한 식별자이다.
단 URL는 식별하는 방법에서 자원의 위치를 명시한다는 것이다. URL은 URI의 부분집합이라 보면된다.

URL은 웹 브라우저가 특정 웹 페이지나 파일에 접근할 수 있도록 해준다.
URL의 구조는 다음과 같은 요소로 구성된다. 



Scheme: 스키마는 통신할 프로토콜에 해당한다.
Domain Name: 우리가 통신할 서버의 이름에 해당한다. 
Port: HTTP는 기본적으로 80번 포트로 통신을 한다. 생략해도 묵시적으로 80번으로 통신한다.
Path to file: URL로 가져올 웹 서버의 리소스의 추상적 위치에 해당한다.
Parameters: 웹 서버의 리소스 형식의 범위를 제한하기 위해 사용된다.

### 2.2 메서드
 
메서드에 대한 이해가 부족하여 서로 다른 메서드로 팀 일관성이 깨지는 경우가 꽤 많았다.
이를 해결하기 위해 우리는 각 메서드에 대한 내용을 정확하게 파헤쳐본다. 

**[GET]**

GET요청은 URL로 식별되는 자원을 요청할 때 사용된다. 
GET 요청 사용 시 주의 점은 GET요청 시 자원을 생산하는 프로세스가 참조 될 경우에는 생성 과정을 반환하는 것이 아닌 생성된 리소스를 반환해야 한다.  

예를 들어 GET http://localhost:80/user 의 요청 시 서버에서 데이터 베이스로 사용자 생성 SQL이 쿼리 된다 가정해본다. 
이런 상황에서 응답으로 SQL insert 쿼리와 같이 중간 단계 과정을 응답으로 하지 말라는 것이다.

기본적인 GET 요청 이외에도 조건부 GET 과 부분적 GET 요청에 대해 짧게 짚고 넘어 가겠다.

**조건부  GET** 
HTTP 1.1에서는 더욱 세분화된 캐시 제어를 위해 If-Modified-Since, If-Unmodified-Since, If-Match, If-None-Match 그리고 If-Range header 값에 따라 GET 요청이 조건부로 작동한다.  
 
예를 들어 http://localhost:80/user 요청에 if-Modified-Since: Wed, 21 Oct 2015 07:28:00 GMT header가 추가 되면, 2015년 10 21일 7시 28분 이후로 자료가 바뀌었다면 리소스를 반환하는 식이다. 

**부분적 GET**
부분적 GET 의 경우에는 Range header의 값에 따라 응답 받을 리소스의 범위를 제한하여 받겠다는 것이다. 

예를 들어 http://localhost:80/user 와 Header Range: bytes=0-499 를 추가하게 되면 응답을 첫 500 바이트까지만 받는다.


**[POST]**

 POST 메서드는 요청의 정보를 서버의 새로운 리소스로 수락하도록 요청하는 데 사용된다. 요청 URL에 의해 식별된 리소스의 하위 리소스가 된다.
말이 많이 어렵지만 그냥 서버에 새로운 리소스를 등록하기 위한 요청이다.

**[HEAD]**

HEAD 메서드는 GET 요청을 보냈을 때  Body를 제외한 정확히 같은 응답을 해야한다.
HEAD는 API 유효성과 Header 정보를 통한 정보를 얻기 위해 사용한다.

**[PUT]**

PUT 요청도 POST요청과 같이 특정 URL에 리소스를 추가하는 작업이다. 
두 메서드간 큰 차이는 요청하는 URL이 직접 해당 리소스를 가르키냐는 것이다.  

예를 들어 
```
POST /api/posts HTTP/1.1
Host: example.com
Content-Type: application/json
Content-Length: 82

{
    "title": "My First Post",
    "content": "This is the content of my first blog post."
}
```
이 요청을 한다 했을 때 서버에는 post가 하나더 추가 되겠지만 /api/posts 자체가 그 추가된 리소스를 뜻하지 않는다, 

반면 PUT의 경우에는
```
PUT /api/posts/1 HTTP/1.1
Host: example.com
Content-Type: application/json
Content-Length: 82

{
    "title": "My Updated Post",
    "content": "This is the updated content of my blog post."
}

```
/api/posts/1로 요청 URL이 생성될 리소스 그 자체를 의미한다는 점에서 큰 차이가 있다.



**[DELETE]**

DELETE는 URL로 식별되는 리소스를 삭제한다.
하지만 이 요청이 무조건 되는 성공되는 것을 보장하지 않는다.
서버에서 삭제를 할 것인지 아닌지 판단하고 리소스 조건에 맞으면 삭제한다. 

즉, 클라이언트에서 200번대 상태 코드 응답으로 삭제 여부를 확인할 수 있다.

**[TRACE]**

잘 사용하지 않는 메서드 중 하나라 생소하다.
[RFC2616](https://datatracker.ietf.org/doc/html/rfc2616#section-9.7) 네트워크 진단과 디버깅 용도 쓰인다는 데 어떤 원리인지  한눈에 이해가 힘들다,

그래서 아래 예시를 통해 알아보자.

클라이언트 TRACE 요청과 Max-Forward 해더로 몇 번 프록시(중계 서버) 나 게이트 웨이를 거쳐 갈 것인지를 저징할 수 있다.  

요청
```
TRACE / HTTP/1.1
Host: www.example.com
Max-Forwards: 5
```

응답은 아래와 같이 요청에 정보를 그대로 반환해주기 때문에 민감한 정보를 응답할 수 있다.
그래서 보안 상의 이유로 권장하지 않는다. 

응답
HTTP/1.1 200 OK
Content-Type: message/http

TRACE / HTTP/1.1
Host: www.example.com
Max-Forwards: 5

**[CONNECT]**

터널 전환용 메서드로 SSL 전환하기 위한 용도 쓰인다.


### 2.3 세션(Session)과 쿠키(Cookie)

HTTP의 세션은 HTTP의 무상태성 특성으로 인해 처음에는 이해가 어려운 수 있다.
세션에 대해 이해가 위해선 쿠키에 대한 이해가 먼저 필요하다.

**쿠키(Cookie)**
쿠키는 클라이언트 측에서 저장되는 작은 데이터 파일로, 
서버가 사용자의 상태를 유지하거나 특정 정보를 기억하기 위해 사용한다.
웹 브라우저는 서버로부터 받은 쿠키를 로컬에 저장하고, 이후 동일한 서버로 요청을 보낼 때 해당 쿠키를 자동으로 포함한다. 
쿠키는 주로 다음과 같은 목적으로 사용된다.

세션 관리: 로그인 정보나 장바구니 상태 등을 유지
+ 개인화: 사용자 선호 설정이나 테마를 기억
+ 트래킹: 사용자의 웹사이트 방문 기록이나 행동을 추적
+ 쿠키의 구조는 이름, 값, 유효 기간, 도메인, 경로, 보안 설정 등의 요소로 이루어진다.

  
쿠키의 주요 속성
+ Expires: 쿠키의 만료 시간을 지정한다. 지정된 시간이 지나면 쿠키는 자동으로 삭제된다.
+ Secure: 이 플래그가 설정되면 HTTPS를 통해서만 쿠키가 전송된다.
+ HttpOnly: 이 플래그가 설정되면 자바스크립트에서 쿠키에 접근할 수 없도록 하여 보안을 강화한다.
+ 
쿠키는 클라이언트 쪽에 저장되기 때문에 비교적 쉽게 조작될 수 있다.
따라서 중요한 정보는 쿠키에 직접 저장하지 않고, 대신 세션을 사용하거나 암호화된 값을 저장하는 것이 일반적이다.

**세션(Session)**
세션은 서버 측에서 유지되는 상태 정보이다.
사용자가 웹 애플리케이션에 로그인하거나 중요한 정보를 교환할 때, 서버는 세션을 생성하고 그 세션에 관련된 데이터를 관리한다.
각 클라이언트는 세션 ID라는 고유한 식별자를 가지며, 이를 통해 서버는 여러 사용자의 상태를 구분한다. 
세션 ID는 주로 쿠키에 저장되지만, 경우에 따라 URL 파라미터나 HTTP 헤더를 통해 전송될 수도 있다.

세션의 주요 특징

+ 서버 측에서 관리: 세션 정보는 서버의 메모리나 데이터베이스에 저장되므로, 클라이언트가 이를 임의로 수정할 수 없다.
+ 짧은 수명: 세션은 일반적으로 짧은 시간 동안 유지되며, 일정 시간이 지나면 만료된다. 사용자가 웹 브라우저를 닫으면 세션이 종료되는 경우도 많다.
+ 보안: 쿠키보다 보안성이 높다. 세션 데이터는 서버에서만 유지되고 관리되므로 민감한 정보를 다룰 때 더 안전하다.

  
  세션은 보통 로그인한 사용자 정보나 특정 작업을 수행 중인 사용자의 상태를 유지하는 데 유용하다.
   예를 들어, 사용자가 장바구니에 물건을 담거나 특정 페이지에서 작업을 수행하고 있을 때 그 상태를 서버에서 기억하게 된다.
  
**쿠키와 세션의 차이점**
저장 위치: 쿠키는 클라이언트 측에 저장되고, 세션은 서버 측에 저장된다.
+ 보안성: 쿠키는 클라이언트에 저장되므로 비교적 보안에 취약하며, 세션은 서버에서 관리되어 더 안전하다.
+ 수명: 쿠키는 만료 시간을 설정할 수 있지만, 세션은 일반적으로 사용자가 웹 브라우저를 닫거나 일정 시간이 지나면 만료된다.
+ 데이터 저장 용량: 쿠키는 각 쿠키 당 약 4KB 정도의 용량 제한이 있지만, 세션은 서버에서 관리되므로 더 큰 데이터를 처리할 수 있다.
결론적으로, 쿠키는 클라이언트 측에 데이터를 저장하여 상태를 유지하는 반면,
 세션은 서버에서 데이터를 관리하여 더 높은 보안성을 제공한다.
둘은 웹 애플리케이션에서 서로 보완적으로 사용되며, 상황에 따라 적절히 선택하여 사용할 필요가 있다.

HTTP는 무상태성이지만, 세션을 통한 클라언트 식별 기능을 제공한다 정도로 이해하고 넘어가자.


## 멱등성
멱등성은 HTTP 다루다 보면 꼭 한번씩 듣게 되는 단어이다. 한글인데도 이해하기 어려운 멱등성에 대해 제대로 이해해보기로 하자. 

### 3.1 안전한 메소드(Safe methods)
GET과 HEAD는 리소스에 대한 조회가 주 목적인 메서드이기 때문에, 관례적으로 안전한 메서드로 굳혀졌다. 따라서 서버 개발자라면 반드시  GET 과 HEAD는 조회 목적만을 하도록 구성해야한다.

### 3.2 멱등 메소드(Idempotent Methods)
멱등 메서드란 같은 요청을 여러 번 보내도 최종 결과가 같다는 것을 의미한다. 
즉, N번 동일한 요청을 보내더라도 그 결과는 한 번 요청한 것과 같다. 
이 특성은 웹 애플리케이션의 안정성을 높이는 데 중요한 역할을 한다.
멱등성을 가진 메서드는 주로 GET, HEAD, PUT, DELETE가 있다. 
이 메소드들은 여러 번 호출해도 서버의 상태가 최종적으로 동일하게 유지된다.
GET: 정보를 가져오는 데 사용되며, 여러 번 요청해도 서버의 내용은 변하지 않는다.
항상 같은 데이터를 반환하니까 멱등성을 가지고 있다 볼 수 있다.
HEAD: GET과 유사하게 동작하지만, 응답 본문 없이 헤더만 반환한다.
GET과 마찬가지로 여러 번 호출해도 서버의 상태는 그대로 유지된다.
PUT: 자원을 생성하거나 업데이트하는 데 사용된다.
동일한 자원에 대해 여러 번 PUT 요청을 보내도 최종 결과는 같다
. 즉, 같은 데이터를 여러 번 보내도 자원이 중복 생성되지 않아서 멱등성을 갖는다.
DELETE: 자원을 삭제하는 메서드다.
동일한 자원을 여러 번 삭제하려고 요청해도, 처음 한 번 삭제한 후에는 더 이상 삭제할 자원이 없으니까 멱등성을 유지한다.
결론적으로, 멱등성은 여러 번 요청해도 결과가 같다는 특징이 있다. 
이 특성 덕분에 웹 애플리케이션의 안정성과 예측 가능성을 높일 수 있다. 
멱등성은 사용자에게 일관된 경험을 제공하는 데 중요한 요소이다.
당연한 이야기 이지만, 멱등 메서드는 해당 메서드를 사용한다고 조건이 만족되는 것이 아닌,
해당 메서드를 사용하고 설계하는 서버 개발자가 만족시켜야할 사항이다. 

## CORS(교차 출처 리소스 공유)
CORS(교차 출처 리소스 공유)는 웹 브라우저가 한 출처(origin)에서 로드된 웹 페이지가 다른 출처의 자원에 접근할 수 있도록 허용하는 메커니즘이다.
 이는 웹 보안을 유지하면서도 다양한 출처 간의 리소스를 공유할 수 있게 해준다. 주로 AJAX 요청이나 웹 폰트와 같은 자원에 대해 사용된다.

### 4.1 CORS의 필요성

웹 브라우저는 기본적으로 보안상의 이유로 Same-Origin Policy(SOP)를 따른다. 
이 정책은 하나의 출처에서 로드된 웹 페이지가 다른 출처의 자원에 접근하는 것을 제한한다. 
예를 들어, `http://example.com`에서 로드된 페이지는 `http://api.example.com`의 자원에 접근할 수 없다. 
CORS는 이러한 제한을 완화하여, 서버에서 허용한 특정 출처에 대해서만 교차 출처 요청을 허용한다.

### 4.2 CORS 작동 원리

CORS는 HTTP 헤더를 사용하여 작동한다. 클라이언트가 다른 출처에 요청을 보낼 때, 서버는 요청에 대한 응답으로 CORS 관련 헤더를 포함해야 한다. 주요 헤더는 다음과 같다:

- Access-Control-Allow-Origin: 이 헤더는 클라이언트가 요청하는 출처를 허용하는지 여부를 나타낸다. `*`을 설정하면 모든 출처의 요청을 허용하게 된다.
- Access-Control-Allow-Methods: 서버가 클라이언트의 요청에 대해 허용하는 HTTP 메서드를 지정한다. 예를 들어, `GET, POST, OPTIONS`와 같이 설정할 수 있다.
- Access-Control-Allow-Headers: 클라이언트가 요청 시 사용할 수 있는 헤더를 지정한다.
- Access-Control-Allow-Credentials: 이 헤더가 `true`로 설정되면, 클라이언트가 인증 정보를 요청과 함께 전송할 수 있도록 허용한다.

- Access-Control-Max-Age: Preflight 요청의 결과를 캐시할 수 있는 시간을 초 단위로 지정한다.

### 4.3 CORS의 종류

CORS 요청은 크게 두 가지 유형으로 나뉜다:

1. Simple Requests: `GET`, `POST`, `HEAD` 메서드를 사용하며, CORS 헤더의 요구사항을 간단하게 충족하는 요청이다. 이 요청은 추가적인 Preflight 요청이 필요하지 않다.
2. Preflight Requests: `PUT`, `DELETE`와 같이 안전하지 않은 메서드를 사용할 때 발생하는 요청이다. 클라이언트는 먼저 `OPTIONS` 메서드로 서버에 Preflight 요청을 보내어 서버가 요청을 허용하는지 확인한다. 서버는 적절한 CORS 헤더를 포함하여 응답해야 한다.
예를 들어, 클라이언트가 `PUT` 요청을 보내기 전에 서버에 다음과 같은 Preflight 요청을 보낼 수 있다:
```
OPTIONS /api/resource HTTP/1.1
Origin: http://example.com
Access-Control-Request-Method: PUT
```

서버는 다음과 같이 응답해야 한다:

```
HTTP/1.1 204 No Content
Access-Control-Allow-Origin: http://example.com
Access-Control-Allow-Methods: PUT
```

### 4.4 CORS의 문제점과 고려사항
CORS를 사용할 때는 몇 가지 주의해야 할 사항이 있다. 스프링으로 서버를 개발하다 보면, Filter나 Interceptor에도 Preflight 요청이 들어오게 된다. 따라서 Filter와 Interceptor에서 Preflight 요청은  filter와 Interceptor 에서 제외해줘야한다. 

## 결론
HTTP는 웹 애플리케이션의 기본적인 통신 프로토콜로,
그 작동 방식과 설계 원리를 이해하는 것은 개발자에게 필수적이다.
이 글에서는 HTTP의 기본 개념, 메서드, 세션 및 쿠키, 멱등성, 그리고 CORS에 대해 다루었다.
이러한 기초 지식을 바탕으로 더욱 안정적이고 효율적인 웹 애플리케이션을 개발할 수 있기를 바란다.
프로젝트에서 발생하는 다양한 문제를 해결하기 위해서는 계속해서 HTTP와 관련된 기술을 학습하고 적용해 나가야 한다. 
다양한 상황에서의 HTTP 사용 경험은 개발자의 역량을 한층 높여줄 것이다.
