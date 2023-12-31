# CORS

### 목차

* CORS 란
  * 동일 출처 정책
  * JSONP
  * `Access-Control-Allow-Origin`
* `@CrossOrigin`

### 강의 정리

실제 REST API 사용 경험!\
많은 문제가 생기는데 대표적인 CORS(Cross Origin Resource Sharing) 에러에 대해 살펴보자\
Same-Origin Policy(동일 출처 정책)\
동일 오리진 정책 웹 브라우저가 처리하는 보안 정책으로 얻으려는 리소스의 출처가 현재 요청하려는 페이지와 서버가 다르면 에러가 난다.(포트포함)\


\=> 해결 방법 : 서버의 REST API Response 헤더에 Access-Control-Allow-Origin Header를 추가한다. B/E에서 여기(F/E의 주소)에서 요청한 것은 괜찮아요! 라고 설명해주는것\


JSONP (JSON with Padding): CORS 이전에 동일 출처 정책 문제를 해결하기 위해 사용되던 방식입니다.\
웹 페이지가 다른 도메인의 데이터를 읽을 수 있게 하는 데 사용되는 패턴입니다.\
JSONP는 스크립트 태그를 통해 데이터를 요청하며, 응답은 콜백 함수를 실행하는 JavaScript 코드 형식으로 옵니다.\
하지만 JSONP는 보안 문제와 제한된 요청 방식(GET만 가능) 때문에 현대의 웹 개발에서는 잘 사용되지 않는다.\


Access-Control-Allow-Origin\
CORS를 구현할 때 사용되는 HTTP 응답 헤더 중 하나입니다. 이 헤더는 특정 원본(출처)이 리소스에 접근하도록 허용하는지를 나타냅니다. 예를 들어, 헤더에 \* 값이 설정되면 모든 원본이 리소스에 접근할 수 있습니다. 특정 도메인을 지정하면 해당 도메인만 접근이 허용됩니다.\


@CrossOrigin:\
이 어노테이션을 사용하면 Spring 기반의 웹 서비스에서 CORS 설정을 쉽게 할 수 있습니다. 예를 들어, @CrossOrigin(origins = "http://example.com")과 같이 설정하면 해당 도메인만 리소스에 접근이 가능하게 됩니다. CORS (Cross-Origin Resource Sharing):

### 궁금한 점?

1.개발자도구에서 referer 헤더? referer는 웹 브라우저가 리소스에 접근할 때 해당 리소스나 페이지로 연결을 제공한 이전 웹 페이지의 주소를 나타내는 HTTP 헤더입니다. 이 헤더는 특정 웹 페이지가 어디서 접근되었는지 추적하거나 웹 트래픽의 출처를 파악하는 데 도움을 줍니다. 그러나, 보안 문제로 인해 이 헤더의 사용이 제한될 수 있으며, 때로는 Referer-Policy 헤더를 사용하여 referer 정보의 전송 범위나 상세 정보를 제한할 수 있다.

2.cors 우회 proxy 이용? 클라이언트는 원하는 리소스를 직접 요청하는 대신 CORS proxy 서버에 요청합니다.\
CORS proxy 서버는 해당 리소스를 가져와 클라이언트에게 반환합니다. 이 때, CORS proxy 서버는 CORS 헤더(Access-Control-Allow-Origin, 등)를 응답에 추가하여 클라이언트가 리소스에 접근할 수 있게 합니다.\
장점: 빠르고 쉽게 CORS 문제를 해결할 수 있습니다.\
서드 파티 서비스나 API가 CORS를 직접 지원하지 않을 때 유용합니다.\
단점 :

1. 데이터의 민감성: CORS proxy를 사용하면, 해당 프록시 서버가 전달되는 모든 데이터를 볼 수 있게 됩니다. 민감한 데이터가 이를 통해 전송될 경우, 프록시 서버는 해당 데이터를 가로채거나 조작할 수 있습니다.
2. 서버 부하: 프록시 서버를 직접 운영하는 경우, 많은 요청이 프록시 서버를 통해 갈 경우 서버에 부하가 발생할 수 있습니다.
3. 비효율성: 간단한 요청도 프록시 서버를 거쳐가야 하므로, 이는 추가적인 지연 시간을 초래할 수 있습니다.\


결론적으로, CORS proxy는 개발 과정에서 빠르게 문제를 해결하기 위한 임시 방편으로 사용될 수 있지만, 프로덕션 환경에서는 이러한 방식이 가져올 수 있는 위험성을 충분히 고려해야 합니다. 가능하다면, 백엔드 서버에서 직접 CORS 헤더를 설정하는 것이 더 안전하고 권장되는 방법입니다.

3. 프록시 서버 사용의 장점?

* 컨텐츠 필터링: 프록시 서버를 사용하여 특정 웹사이트나 웹 컨텐츠에 대한 접근을 차단하거나 허용할 수 있습니다. 이를 통해 조직 내의 네트워크 사용을 제한하거나 원치 않는 컨텐츠를 필터링하는 데 사용될 수 있습니다.
* 캐싱: 프록시 서버는 자주 요청되는 웹 리소스나 데이터를 로컬에 캐시하여 저장할 수 있습니다. 이를 통해 반복적인 요청에 대한 응답 시간을 줄일 수 있으며, 외부 트래픽을 감소시킬 수 있습니다.
* 보안 및 익명성: 프록시를 사용하면 사용자의 실제 IP 주소를 숨기고, 프록시 서버의 IP 주소로 웹 요청을 전송할 수 있습니다. 이를 통해 사용자의 실제 위치나 신원 정보를 숨길 수 있습니다. 프록시 서버를 통해 네트워크 트래픽을 감사하고, 악의적인 트래픽을 차단하는 추가적인 보안 계층을 제공할 수 있습니다.
* 로드 밸런싱: 여러 서버에 대한 트래픽을 분산시키기 위해 로드 밸런서로서의 프록시를 사용한다.
