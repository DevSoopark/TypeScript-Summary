## Chapter 4. Single Page Application

전통적인 웹 방식은 새로운 페이지 요청 시마다 정적 리소스가 다운로드되고 전체 페이지를 다시 렌더링하는 방식을 사용하므로 새로고침이 발생되어 사용성이 좋지 않았다. 그리고 변경이 필요없는 부분를 포함하여 전체 페이지를 갱신하므로 비효율적이었다.

이후에 등장한 `싱글 페이지 애플리케이션(single page application, SPA)`은 서버로부터 완전한 새로운 페이지를 불러오지 않고, 현재의 페이지를 동적으로 다시 작성하는 웹 애플리케이션이다.

웹 애플리케이션에 필요한 모든 정적 리소스를 최초에 한번 다운로드한다. 이후 새로운 페이지 요청 시, 페이지 갱신에 필요한 데이터만을 전달받아 페이지를 갱신하므로 서버에 불필요한 코드가 계속 요청되는 일이 없고, rendering 도 client 상에서 일어나기 때문에 전체적인 트래픽도 감소할 수 있고, 전체 페이지를 다시 렌더링하지 않고 변경되는 부분만을 갱신하므로 새로고침이 발생하지 않아 네이티브 앱과 유사한 사용자 경험을 제공할 수 있다.

<img src="img/ssr.PNG" width="600" height="360">

### 클라이언트 사이드 렌더링(Client Side Rendering)의 문제점

- 초기 구동 속도

SPA는 웹 애플리케이션에 필요한 모든 정적 리소스를 최초에 한번 읽어들이고, 자바스크립트가 화면을 그리는 시간까지 모두 마쳐야 콘텐츠가 보여지기 때문에 초기 구동 속도가 상대적으로 느리다. 하지만 SPA는 웹페이지보다는 애플리케이션에 적합한 기술이므로 트래픽의 감소와 속도, 사용성, 반응성의 향상 등의 장점을 생각한다면 결정적인 단점이라고 할 수는 없다.

- 검색엔진 최적화(Search Engine Optimization, SEO) 문제

SPA는 서버 렌더링 방식이 아닌 자바스크립트 기반 비동기 모델(클라이언트 렌더링 방식)이고, 대부분의 웹 크롤러, 봇들이 자바스크립트 파일을 실행시키지 못하기 때문에, HTML에서만 콘텐츠를 수집하게 되고 클라이언트 사이드 렌더링되는 페이지를 빈 페이지로 인식하게 된다.
(구글은 자바스크립트로 렌더링해서 크롤링하므로 되는 경우가 많음. good!)

추가적으로 보안문제도 발생한다. 기존의 서버 사이드 렌더링에서는 사용자에 대한 정보를 서버 측에서 사용할 수 있는 세션으로 관리를 했다. 그러나, 클라이언트 측에서는 쿠키 말고는 사용자에 대한 정보를 저장할 공간이 마땅치 않다.