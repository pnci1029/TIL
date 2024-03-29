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
#  
#  
### health
  - 어플리케이션 요청 동작여부 확인
  - 데이터베이스 여부 확인
  - 디스크 사용량 문제 여부 확인
```
  ""yml에 health - detail 활성화 후 확인가능""

  "status": "UP",
  "components": {
    "db": {
      "status": "UP",
      "details": {
        "database": "H2",
        "validationQuery": "isValid()"
      }
    },
    "diskSpace": {
      "status": "UP",
      "details": {
        "total": 994662584320,
        "free": 869734965248,
        "threshold": 10485760,
        "exists": true
      }
    },
    "ping": {
      "status": "UP"
    },
    "redis": {
      "status": "UP",
      "details": {
        "version": "7.0.8"
      }
    }
  }
```
### info
  - java 버전 / OS 정보 노출 (yml 설정 추가 필요)
  - build (build.gradle 추가 필요) - 빌드정보(빌드 시간, 버전, 이름 ...)
  - git 정보 노출
  - 어플리케이션 기본정보 노출
```
{
  "app": {
    "name": "chhong",
    "projectName": "myPro"
  },
  "git": {
    "branch": "master",
    "commit": {
      "id": "asdasdsadas",
      "time": "2023-03-04T14:00:29Z"
    }
  },
  "build": {
    "artifact": "pro",
    "name": "pro",
    "time": "2023-03-05T03:16:07.616Z",
    "version": "0.0.1-SNAPSHOT",
    "group": "com.example"
  },
  "java": {
    "version": "11.0.17",
    "vendor": {
      "name": "asdasdasdsadsads",
      "version": "Corretto-11.0.17.8.1"
    },
```
### loggers
  - /actuator/loggers/com.example.pro.controller 를 통해 컨트롤러 로그 레벨 실시간 확인 / 변경 가능
  - yml에서 하위 로깅 경로를 지정해주어 로깅 레벨 설정
  - 로거 레벨을 설정하지 않을 시 기본으로 'info' 레벨로 스프링에서 지정
```
  method : get
  /actuator/loggers/com.example.pro.controller 요청 시 
{
  "configuredLevel": "DEBUG",
  "effectiveLevel": "DEBUG"
} 현재 로그 레벨 확인

  method : post
  /actuator/loggers/com.example.pro.controller 요청 시 
  body - json 
{
  "configuredLevel" : Trace 
} 요청 시 현재 로그 레벨 Debug -> Trace로 변환
```
### httpExchanges
  - 
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





