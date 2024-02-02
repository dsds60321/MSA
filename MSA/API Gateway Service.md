# API Gateway Service
## API Gateway란?
* 사용자가 설정한 라우팅 설정에 따른 각 엔드포인트로 클라이언트 대신 요청과 응답을 받아 클라이언트에게 다시 전달해주는 프록시 역활을 하고 있습니다.
* **정점**으로는 시스템 내부 구조를 숨기고 외부의 요청에 적절한 형태로 가공할수 있는 점이 있다.
![apigateway_1.png](img%2FAPIGATEWAY%2Fapigateway_1.png)
* 기존 마이크로 서비스에 추가 혹은 변경이 이루어져도 자체적으로 빌드, 배포가 되므로 변경후에도 문제가 없지만 클라이언트 사이드에 엔드포인트가 달라질수 있으므로
<br>같이 수정 및 배포가 되어야 되는일이 생기므로 일괄적으로 처리 할수 있는 모듈이 필요하다. 단일 진입점 형태로 개발할수 있는 API-게이트웨이가 위에 문제를 해결해준다.
### API Gateway Service 기능
1. 인증 및 권한
2. 서비스 검색 통합
3. 응답 캐싱
4. 정책, 회로 차단 및 Qos 다시시도
5. 속도 제한
6. 부하 분산
7. 로깅, 추적, 상관 관계
8. 헤더, 쿼리 문자열 및 청구 변환
9. IP 허용 목록에 추가
### Netflix Ribbon
* Spring Cloud에서 서비스를 호출하기 위해 사용되는 방법
1. RestTemplate
   * 서버 주소 와 포트번호를 입력 HTTP 메소드를 통해 외부 서비스 연동
~~~java
RestTemplate restTemplate = new RestTemplate();
restTemplate.getForObject("http://localhost:8080/", User.class, 200);
~~~
2. Feign Client
   * @FeignClient 라는 어노테이션을 통해 API 호출 가능합니다. 특정한 인터페이스를 만들고 인터페이스에서 웹으로 따로 호출하며 마이크로 서비스 이름을 등록합니다. 
~~~java
@FeignClient("stores")
public interface StoreClient {
    @RequestMapping(method = RequestMethod.GET, value="/stores")
    List<Store>getStores();
}
~~~