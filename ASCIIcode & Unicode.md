# 📕 아스키 코드(ASCIIcode)와 유니코드(Unicode)

## 📗 아스키코드란?

컴퓨터는 모든 데이터를 0과 1로 바꿔서 저장고 인식합니다!
그렇다면 알파벳이나 다른 문자들은 어떻게 컴퓨터에 저장될까요?

예를들어 a 라는 알파벳을 0 과 1로 나타내려면 규칙이 필요하겠죠?
그렇기에 **미국정보교환표준부호** 또는,**아스키**(ASCII,American Standard Code for Information Interchange)라는 규칙을 만들어냅니다.

아스키 코드를 다시한번 살펴보면,
알파벳(대,소문자)숫자, 특수문자 만을 사용했고 이를 저장하기위해서 **1byte = 8bit**면 충분했다고 합니다. 즉, 각각의 문자를 나타내기 위해 8자리의 2진수로 각 문자를 나타낸다는 뜻입니다.

몇가지 예시로 표를 한번 확인해 봅시다.

![아스키코드 예시](https://user-images.githubusercontent.com/66991380/91523280-45199900-e937-11ea-9487-416dee02ae7e.jpg)

자 여기서 이상한 점이 있습니다.

8자리의 이진수를 사용한다고 했는데 표의 이진수는 일곱자리입니다!

나머지 한자리는 어디있냐면 바로 **패리티 비트**(parity bit)라고 불리우는데 **데이터의 에러를 탐지**하기위해 사용합니다!

이 일곱자리의 이진수에서 1이 홀수개 라면 끝에 1을 덧붙이고 짝수게라면 0을 덧붙입니다.
그렇게되면 아주 정밀하지는 않지만 패리티 비트를 이용해 어느정도의 에러를 탐지할수 있게됩니다.

패리티 비트를 제외하면 <u>총 7자리의 이진수로 문자를 나타낼수 있기 때문에</u> 총 2^7개의(2의 7승) **128개의 문자**를 나타낼수 있게 됩니다.

그 128개에 대한 표는 아래와 같습니다.

![아스키코드표](https://user-images.githubusercontent.com/66991380/91523424-ae99a780-e937-11ea-8f1f-a45b57f139a9.jpg)

---

## 📘 유니코드란?

기존에는 **ASCIIcode**를 사용하면서 문제없이 사용하고있었습니다.
하지만 컴퓨터가 발전함에따라 미국이 아닌 다른 국가사람들이 자국어로 글들을 작성하고 싶어집니다.
그래서, 자국어로 작성을 하면서 사용을 하고있었는데, 네트워크가 발전함에 따라 다른사람 홈페이지에 들어갔는데 글씨가 와장창 깨지는 현상을 발견하게 됩니다!
그리하여 국제적으로 전세계 언어를 모두 표시할 수 있는 표준코드를 만들기로한 것이 **유니코드**입니다.

추가적으로 현재 한국에서 사용되는 인코딩 방식으로는 크게 **euc-kr** 방식과 **UTF-8** 방식이 있습니다.

euc-kr 방식은 원래 영어만을 고려한 1byte 길이의 ASCII 라는 인코딩 방식을 확장하여 한글을 사용할 수 있도록 만든 2byte 길이의 국가 언어 코드입니다.
국가 언어코드. 즉 우리나라에서만 쓸 수 있도록 만든 코드이며 세계 어디에서나 공통으로 사용되는 인코딩 방식이 아니기 때문에, 다른 언어를 사용하는 환경(외국 등)에서는 한글 페이지를 제대로 볼 수 없는 문제가 발생합니다.

**그렇기에 유니코드의 필요성을 알수 있습니다!**

유니코드에는 두가지 매핑 방식이 있는데

- 유니코드 변환 형식 인코딩(Unicode Transformation Format, UTF)과
- 국제 문자 세트 인코딩(Universal Coded Character Set, UCS) 이 있다.
  여기서 문자 세트(Character set)란 여러언어가 사용할수 있는 문자 집합을 뜻합니다.

그중에 **UTF-8**을 보면 우리가 HTML을 공부하면서 볼수 있었던 부분이 나옵니다.
UTF-8은 charset안에 들어가있었는데, 이는 UTF-8이 문자 **인코딩 방식**을 뜻한다는것을 알 수 있습니다.

여기서 **인코딩**이란 컴퓨터가 이해할수 있는 형태로 바꿔주는것을 뜻합니다.
아래코드 표를 참고합시다.

![문자 인코딩 방식](https://user-images.githubusercontent.com/66991380/91524403-1224d480-e93a-11ea-9455-e7505503fd41.jpg)

🎈 <u>유니코드</u>는 **국제 표준 문자표**를 뜻하고, <u>UTF-8</u>은 **인코딩 방식**을 말하니 꼭 구분지어 기억할수 있도록합시다!

<참조사이트>
[https://miaow-miaow.tistory.com/37#]: https://miaow-miaow.tistory.com/37#  
[https://ofcourse.kr/html-course/%EC%9D%B8%EC%BD%94%EB%94%A9]: https://ofcourse.kr/html-course/%EC%9D%B8%EC%BD%94%EB%94%A9  
[https://m.blog.naver.com/PostView.nhn?blogId=jamduino&logNo=220833819592&proxyReferer=https:%2F%2Fwww.google.co.kr%2F]: https://m.blog.naver.com/PostView.nhn?blogId=jamduino&logNo=220833819592&proxyReferer=https:%2F%2Fwww.google.co.kr%2F  
[https://medium.com/@jeongdowon/unicode%EC%99%80-utf-8-%EA%B0%84%EB%8B%A8%ED%9E%88-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-b6aa3f7edf96]: https://medium.com/@jeongdowon/unicode%EC%99%80-utf-8-%EA%B0%84%EB%8B%A8%ED%9E%88-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-b6aa3f7edf96  
[https://ko.wikipedia.org/wiki/ASCII]: https://ko.wikipedia.org/wiki/ASCII

[https://ko.wikipedia.org/wiki/%ec%9c%a0%eb%8b%88%ec%bd%94%eb%93%9c]: https://ko.wikipedia.org/wiki/%EC%9C%A0%EB%8B%88%EC%BD%94%EB%93%9C
