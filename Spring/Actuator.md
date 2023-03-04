## Spring Actuator
  - 스프링 프레임워크에서 제공하는 라이브러리로 어플리케이션 상태를 모니터링하고 관리를 위한 기능 제공
  - 운영환경에서 서비스를 운영할 때 이러한 기능들을 프로덕션 준비기능이라고 한다.(프로덕션을 배포하기 전 준비하는 비 기능적 요소)
  - 어플리케이션(서버)이 살아있는지, 로그가 정상작동하는지, 커넥션풀이 충분한지, CPU 사용정도가 높은지 등등..
  - 프로메테우스, 마이크로미터, 그라파나 등 모니터링 시스템과 쉽게 연동하여 사용 가능
  - 각각의 엔드포인트는 /actuator/{엔드포인트 명} 으로 조회 가능
#  
## 기본 설정
### Build.gradle 의존성 추가
```
  // actuator
  implementation 'org.springframework.boot:spring-boot-starter-actuator'
```
### application.yml 설정 -> Spring Actuator 기능 전체 조회 (localhost:8080/actuator 조회 시)
```
# Actuator 관련 스크립트
management:
  endpoints:
    web:
      exposure:
        include: "*"
```
### Actuator 기능을 통한 서버 상태 파악
  - url/actuator 
  - <img width="569" alt="스크린샷 2023-03-04 오후 9 30 57" src="https://user-images.githubusercontent.com/81909140/222901180-67024659-9f0f-4f88-979f-e06c6f9a0c1f.png">
  - url/actuator/health -> 현재 서버가 잘 작동하는지 헬스 정보
  - <img width="193" alt="스크린샷 2023-03-04 오후 9 32 33" src="https://user-images.githubusercontent.com/81909140/222901259-34563c50-2256-4bc7-b3fc-3f918d9113d3.png">
#  
# 
#  
## 자주사용하는 Actuator의 엔드포인트들
#### <<<<health, info, logger, httpexchanges, metrics,>>>> beans, configprops, mapping, env, threaddump, shutdown
#### 'beans'
  - 스프링 컨테이너에 등록된 빈 조회
```
"beans": {
            "href": "http://localhost:8080/actuator/beans",
            "templated": false
        },
        
  ->
"beans": {
                "spring.jpa-org.springframework.boot.autoconfigure.orm.jpa.JpaProperties": {
                    "aliases": [],
                    "scope": "singleton",
                    "type": "org.springframework.boot.autoconfigure.orm.jpa.JpaProperties",
                    "resource": null,
                    "dependencies": []
                },
                "endpointCachingOperationInvokerAdvisor": {
                    "aliases": [],
                    "scope": "singleton",
                    "type": "org.springframework.boot.actuate.endpoint.invoker.cache.CachingOperationInvokerAdvisor",
                    "resource": "class path resource [org/springframework/boot/actuate/autoconfigure/endpoint/EndpointAutoConfiguration.class]",
                    "dependencies": [
                        "org.springframework.boot.actuate.autoconfigure.endpoint.EndpointAutoConfiguration",
                        "environment"
                    ]
                },
               ...
```
#### 'configprops'
  - @ConfigurationProperties 값들 조회
  - spring dataSource 관련
```
"beans": {
            "href": "http://localhost:8080/actuator/configprops",
            "templated": false
        },
        
  ->
contexts": {
    "application": {
      "beans": {
        "spring.jpa-org.springframework.boot.autoconfigure.orm.jpa.JpaProperties": {
          "prefix": "spring.jpa",
          "properties": {
            "mappingResources": [
              
            ],
            "showSql": false,
            "generateDdl": false,
            "properties": {
              "hibernate.format_sql": "true",
              "hibernate.show_sql": "true"
            },
            "databasePlatform": "org.hibernate.dialect.H2Dialect"
          },
               ...
```
#### 'env'
  - 스프링 환경변수에 관한 값들
```
"beans": {
            "href": "http://localhost:8080/actuator/env",
            "templated": false
        },
        
  ->
{
  "activeProfiles": [
    
  ],
  "propertySources": [
    {
      "name": "server.ports",
      "properties": {
        "local.server.port": {
          "value": 8080
        }
      }
    },
               ...
```
#### 'mappings'
  - 어플리케이션 http 메소드 사용 확인
```
"handler": "com.example.pro.controller.ArticleController#articlePost()",
              "predicate": "{POST [/article/post]}",
              "details": {
                "handlerMethod": {
                  "className": "com.example.pro.controller.ArticleController",
                  "name": "articlePost",
                  "descriptor": "()Ljava/lang/String;"
                },
                "requestMappingConditions": {
                  "consumes": [
                    
                  ],
                  "headers": [
                    
                  ],
                  "methods": [
                    "POST"
                  ],
                  "params": [
                    
                  ],
                  "patterns": [
                    "/article/post"
                  ],
               ...
```





