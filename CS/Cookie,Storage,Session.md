# 쿠키와 세션 그리고 웹 스토리지

---

## 쿠키발급 및 사용과정

![cookie jpg](https://user-images.githubusercontent.com/66991380/110486099-a95fb580-812f-11eb-8a0a-fba260abfb14.jpg)

1. 서버요청
2. 서버에서 만든 쿠키를 사용자(브라우저)에게 전달
3. 쿠키를 다시 서버에전달
4. 변경사항을 확인하고 다시 서버에서 사용자(브라우저)에게 전달

## HTTP의 특징과 쿠키와 세션을 사용하는 이유

### HTTP 프로토콜의 특징

- **connectionless (비연결 지향)**

HTTP는 사용자(브라우저)가 서버에 요청을 보내면, 서버는 사용자(브라우저)에 요청에 맞는 response를 보내고 접속을 끊는 특성이 있습니다.

- **stateless (상태 비보존)**

사용자와 서버가 통신이 끝나면 상태를 유지하지 않는 특징을 가집니다.

**이 두가지 특징을 해결하기 위해 쿠키와 세션, 스토리지를 사용하며 만약 이를 사용하지 않는다면, 페이지를 이동할떄마다 매번 다시 재로그인 해야하는 상황이 발생하게 됩니다.**

## 쿠키 (Cookie)

### 쿠키란?

쿠키는 크게 두가지 유형이 있습니다.

**persistent cookies(잔류성 쿠키)와 session cookies(세션 쿠키)입니다.**

session cookies(세션 쿠키)는 만료일을 포함하지 않아서 브라우저나 탭이 열려있을동안만 저장됩니다. 브라우저가 닫히게되면, 영구적으로 삭제됩니다.

persistent cookies(잔류성 쿠키)는 만료일을 가집니다. 이 cookie는 만료일까지 유저의 디스크에 저장되며 유저가 방문하는 페이지의 행동을 기록하는등 여러가지 활동들에 사용됩니다.

또한, 클라이언트 로컬에 저장되는 작은 데이터파일이며 개당 4KB~ 5KB로 브라우저별로 다르며 클라이언트에 최대 300개 까지 쿠키가 저장 가능하며, 하나의 도메인에 20개의 값만 가질수 있습니다.

### 쿠키의 동작방식

1. 클라이언트가 페이지를 요청
2. 서버에서 쿠키를 생성
3. HTTP 헤더에 쿠키를 포함시켜 응답
4. 브라우저가 종료되어도 쿠키 만료 기간이 있다면 클라이언트에서 보관하고있다.
5. 같은 요청을 할 경우 HTTP 헤더에 쿠키를 보내서 서버에서 쿠키를 읽어 이전상태 정보를 업데이트후, HTTP 헤더에 포함시켜 응답

즉, 쿠키는 HTTP 헤더에 포함되어서 사용자와 서버를 오갑니다.

## 세션

### 세션이란?

세션은 쿠키를 기반하고 있지만 사용자 정보파일을 브라우저에 저장하는 쿠키와 달리, 세션은 서버측에서 관리하게됩니다. 서버에서는 클라이언트를 구분하기 위해 각각의 세션 별로 ID를 부여하며 서버에 접속해서 브라우저를 종료할때 까지 인증상태를 유지합니다.

사용자에 대한 정보를 서버에 두기에 쿠키보다 보안에 좋지만, 사용자가 많아진다면 메모리를 많이 차지 하게됩니다. 즉, 동접자수가 많은 웹사이트라면 서버에 과부화를 주게되며 성능저하의 요인이 될수있습니다.

클라이언트가 Request를 보내면 해당 서버엔진에서 클라이언트에게 유일한 ID를 부여하는데 이것이 세션 ID입니다.

### 세션의 동작 방식

1. 클라이언트가 서버에 접속시 세션 ID를 발급받는다.
2. 세션 ID에 대해 쿠키를 사용해서 저장하고 가직
3. 클라이언트는 서버에 요청하게될때, 이 쿠키의 세션 ID를 이용해 서버로 전달해 사용합니다.
4. 서버는 세션 ID를 전달받고 그에따른 클라이언트 정보를 가져옵니다.
5. 클라이언트 정보를 가지고 그에 맞는 요청을 응답합니다.

### 세션의 특징

각 클라이언트에게 고유 ID를 부여 하며, 쿠키에 저장된 세션 ID로 클라이언트를 구분하여 그에맞는 응답을 제공, 보안면에서 쿠키보다 우수하며 사용자가 많아진다면 서버 메모리를 차지하게된다.

## 쿠키와 세션의 차이

세션도 결국 쿠키를 사용합니다. 하지만 다른점은 정보가 저장되는 위치입니다. 쿠키는 서버의 자원을 사용하지 않으며, 세션은 서버의 자원을 사용합니다.

보안면에서 세션이 우수하지만, 요청속도는 쿠키가 세션보다 빠른데 이유는 세션은 클라이언트별로 나누어진 고유 ID를 찾아 그에따른 응답을 하기 때문입니다.

보안부분에서는 쿠키는 클라이언트에 저장되기에 요청에서 스니핑(해킹)을 당할 우려가 있어 보안에 취약하다. 세션은 쿠키를 이용해 session ID 만을 저장해 그것으로 구분해서 서버에서 관리하기에 보안부분에서 비교적 좋습니다.

## 웹 스토리지

웹 스토리지는 저장된 데이터가 클라이언트에 존재할뿐 서버로의 전송은 이루어 지지않습니다.

Web Storage는 데이터의 지속성과 관련해 두가지 용도의 저장소를 제공합니다.

기본적으로 Web Storage는 쿠키와 마찬가지로 사이트의 도메인 단위로 접근이 제한되며 A 도메인에서 저장한 데이터는 B 도메인에서 조회할수없습니다.

- 도메인? : 숫자로 이루어진 인터넷상의 컴퓨터 주소를 알기 쉬운 영문으로 표현한 것을 말한다.
  (www.google.com)

### 웹 스토리지와 쿠키와의 비교

- 쿠키는 매번 서버로 전송된다. 하지만 웹 스토리지는 서버로의 전송은 이루어 지지않는다.

웹사이트에서 쿠키를 설정하게되면 이후 모든 웹 요청은 쿠키정보를 포함하여 서버로 전송된다. (따로 설정하지 않아도 자동으로 서버에 전송)

### LocalStorage(영구저장소)

저장한 데이터를 명시적으로 지우지 않는다면 영구적으로 보관이가능하다.

각각의 도메인 별로 로컬스토리지가 생성되며 Window 전역객체의 LocalStorage라는 컬렉션을 통해 저장과 조회가 이루어진다.

HTML5 이후부터 cookie보다 더 많은 장점을 가진 LocalStorage로 대체되었다. 대표적으로 HTTP 요청에서 데이터를 주고 받지 않아도 된다. 그에따라 클라이언트와 서버와의 트래픽을 줄일수있다. 또한 로컬스토리지는 쿠키와는 달리 5MB 라는 정보를 저장할수 있는데 이것을 통해 좀더 다양한것들을 할수있게되었다.

LocalStorage(영구저장소)는 persistent cookies(잔류성 쿠키)처럼 동작한다. Javascript 코드를 삭제하지 않으면 데이터는 자동적으로 삭제 하지 않으며 오랜시간 저장해야하는 큰 데이터에 유용하다. 또한 문자열 뿐만아니라 원시값과 객체도 저장가능하다.

### SessionStorage(임시저장소)

데이터의 지속정과 엑세스범위에 특수한 제한이 존재하며 SessionStorage는 Window 전역객체의 sessionStorage라는 컬렉션을 통해 저장과 조회가 이루어진다.

SessionStorage는 데이터가 지속적으로 보관되지 않는다. 현재 브라우징 되고있는 브라우저 컨텍스트 내에서만 데이터가 유지된다. 즉, 브라우저가 종료되면SessionStorage도 삭제된다.

텝브라우징이나 브라우저를 하나더 실행해 같은 페이지를 실행했을때 이두페이지의 SessionStorage는 별개의 영역으로 서로 침범 하지 못하며 이는 도메인만 같다면 전역적으로 공유가능한 LocalStorage와 구분되는 특징이다.

#### 참고자료

- [https://interconnection.tistory.com/74](https://interconnection.tistory.com/74)

- [https://erwinousy.medium.com/쿠키-vs-로컬스토리지-차이점은-무엇일까-28b8db2ca7b2](https://erwinousy.medium.com/%EC%BF%A0%ED%82%A4-vs-%EB%A1%9C%EC%BB%AC%EC%8A%A4%ED%86%A0%EB%A6%AC%EC%A7%80-%EC%B0%A8%EC%9D%B4%EC%A0%90%EC%9D%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C-28b8db2ca7b2)

- [https://velog.io/@ejchaid/localstorage-sessionstorage-cookie의-차이점](https://velog.io/@ejchaid/localstorage-sessionstorage-cookie%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)
