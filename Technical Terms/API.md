#

---

### API?

API 라는 말을 개발공부를 하다보면 자주 접하게되는데 사실 이에 대한 명확한 이해를 하지 못하고 공부를 하였던거 같아서 이제는 용어에 대해 정리 해보려고한다.

"**[\*API](https://ko.wikipedia.org/wiki/API)**(Application Programming Interface 애플리케이션 프로그래밍 인터페이스)는 응용 프로그램에서 사용할 수 있도록, 운영체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터 페이스를 뜻한다.\*" 주로 파일 제어, 창 제어, 화상 처리, 문자 제어 등을 위한 인터페이스를 제공한다.

> 위키백과 - API

API를 알기전에 UI(User Interface)를 먼저 짚어보자면, 우리가 실생활 에서 자주 사용하는 스마트 폰을 예를 들어보자. 스마트 폰의 홈버튼을 예를들어본다면

![tyler-nix](https://user-images.githubusercontent.com/66991380/112324370-12315b00-8cf6-11eb-8707-3fa810ca88b4.jpg)

Photo by <a href="[https://unsplash.com/@jtylernix?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText](https://unsplash.com/@jtylernix?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)">Tyler Nix</a> on <a href="/s/photos/iphone?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>

이 홈버튼(UI, 사용자 환경)은 사용자가 홈화면으로 돌아가게끔 해주는 방법이며 수단이다. 즉, 스마트폰과 사용자를 이어주는 매개체 이다.

API도 같은 맥락으로 UI가 사용자와 사용자가 다룰 대상(하드웨어 혹은 소프트웨어)를 연결한다면 API는 프로그램과 또 다른 프로그램을 연결해주는 일종의 다리라고 볼 수 있다.

예를들어, 나의 포트폴리오를 만들고자할때 아래의 3가지의 큰 주제로 만들어보려고한다.

- 일기예보 - 일기 예보 정보 자신이 만든 웹페이지에 띄우려면?
- 지도 - 지도를 이용한 웹서비스를 제작하려면?
- 결제 - 사용자들로부터 결제를 통해 나의 앱을 사용하게끔 하려면?

보통 일반 사람들은 이러한 큰 데이터들을 가지고 있지 않을뿐더러 관련 프로그램도 가지고 있지 않다.

하지만, 인터넷상에서 제공되는 API를 이용한다면 충분히 가능하게된다.

"**[\*API](https://ko.wikipedia.org/wiki/API)**(Application Programming Interface 애플리케이션 프로그래밍 인터페이스)는 응용 프로그램에서 사용할 수 있도록, 운영체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터 페이스를 뜻한다.\*" 주로 파일 제어, 창 제어, 화상 처리, 문자 제어 등을 위한 인터페이스를 제공한다.

- 응용프로그램 ⇒ 나의 포트폴리오
- 운영체제나 프로그래밍 언어가 제공하는 기능 ⇒ 날씨정보, 지도정보, 카카오페이 등등..

결론 : API란 간단히 하자면 내가 만든 프로그램이 개인 개발자, 기업 기관이 제공하는 기능, 프로그램 등을 활용할 수 있게끔 도와주는 중간 매개체 라는 것이며, 공공 API 유용한 무료 API들이 존재한다.

### API의 역할?

1. 서버와 데이터베이스에 대한 출입구 역할을 한다.
   - 데이터베이스에 존재하는 중요한 데이터들을 보안하기위해 허용된 사용자에게만 접근하게끔함
2. 애플리케이션과 기기가 원할하게 통신 할 수 있도록한다.
   - 스마트폰 어플이나 프로그램이 기기와 데이터를 원할이 주고받게끔함
3. 모든 접속을 표준화 한다.
   - 기계 / 운영체제와 관련없이 동일한 액세스를 얻을수 있다. (액세스 - 기억 장치의 특정 장소나 데이터 및 프로그램 따위에 사용자나 사용자 그룹이 접근하거나 수행할 수 있는 권리의 범위.)

### API의 유형?

1. private API - 회사 내부 API로 자체 제품서비스를 개선하기위해 내부적으로 발행
2. public API - 공공 API로 누구나 제한없이 사용가능
3. partner API - 기업이 동의하는 특정인들만 사용이 가능

참고

- [api란?](https://dydrlaks.medium.com/api-%EB%9E%80-c0fd6222d34c)
- [API란? 비개발자가 알기 쉽게 설명해드립니다!](http://blog.wishket.com/api%EB%9E%80-%EC%89%BD%EA%B2%8C-%EC%84%A4%EB%AA%85-%EA%B7%B8%EB%A6%B0%ED%81%B4%EB%9D%BC%EC%9D%B4%EC%96%B8%ED%8A%B8/)
