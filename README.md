# NolaeJui

위치 기반 음원 수집 서비스

## 개발 환경

- Springboot, Spring JPA, Spring Security, Spring Cloud
- Kotlin
- Protobuf, RabbitMQ
- Eureka
- Mysql, MongoDB, Redis, Elasticsearch, Logstash
- AWS S3
- Discord Bot

## 시스템 아키텍쳐
<img src="https://github.com/Kan9hee/NolaeJui/blob/main/NolaeJui_Architecture.png" width="800"/>

## Repositories
- https://github.com/Project-NolaeJui/Microservice-Playlist
- https://github.com/Project-NolaeJui/Microservice-Location
- https://github.com/Project-NolaeJui/Microservice-Auth
- https://github.com/Project-NolaeJui/Microservice-Management
- https://github.com/Project-NolaeJui/Gateway
- https://github.com/Project-NolaeJui/Config
- https://github.com/Project-NolaeJui/Eureka

## 주요 기능

### Grpc 기반 마이크로서비스
- 각 마이크로 서비스는 .proto 파일을 정의한 상태
- 메시지 브로커 RabbitMQ를 통해 비동기 메시징 기반 gRPC 통신 구축

### 액세스/리프레시 토큰 관리
|Screen #1|
|:---:|
|<img src="https://github.com/Kan9hee/NolaeJui/blob/main/NolaeJui_LogIn.PNG" width="800"/>|

|Screen #2|
|:---:|
|<img src="https://github.com/Kan9hee/NolaeJui/blob/main/NolaeJui_Redis.PNG" width="800"/>|
- 액세스 토큰은 클라이언트가 직접 보관
- 액세스 토큰 만료시 리프레시 토큰으로 재발급 요청
- Redis에 리프레시 토큰 저장 및 블랙리스트 관리
- 로그아웃 또는 재발급 시 기존 토큰은 블랙리스트에 추가되어 무효화
- 관리자는 특정 유저의 모든 세션을 종료 가능

### 음원 등록 및 검색
|Screen #3|
|:---:|
|<img src="https://github.com/Kan9hee/NolaeJui/blob/main/NolaeJui_SearchResult.PNG" width="800"/>|

|Screen #4|
|:---:|
|<img src="https://github.com/Kan9hee/NolaeJui/blob/main/NolaeJui_Logstash.PNG" width="800"/>|
- MP3 파일/타 서비스 URL 기반 음원 재생
- 미리 서명된 URL을 통한 MP3 음원 파일 저장
- Elasticsearch 기반 멀티 옵션 음원 검색
    - Logstash를 통해 일정 주기마다 Mysql의 데이터를 Elasticsearch에 등록

### 위치 기반 음원 재생 로그
 - 재생한 음원과 재생 위치 정보를 MongoDB에 저장
 - 사용자는 일정 주기마다 현재 위치 주변의 로그를 수집
 - 수집한 로그에서 음원 정보를 추출, 플레이리스트에 저장

### 음원 신고 기능
|Screen #5|
|:---:|
|<img src="https://github.com/Kan9hee/NolaeJui/blob/main/NolaeJui_Report.PNG" width="600"/>|
 - 부정 음원 및 정보 오류를 관리자에게 신고
 - 디스코드 봇을 통한 신고 접수 및 전달

## 참고자료
- https://sjh9708.tistory.com/119
- https://velog.io/@mbsik6082/Spring-Boot-gRPC-Server-%EC%8B%A4%ED%96%89%EC%8B%9C%EC%9E%91-%EC%95%88-%EB%90%98%EB%8A%94-%EC%98%A4%EB%A5%98-gRPC-server-not-start-error-when-using-spring-boot#spring-boot-%EB%B2%84%EC%A0%84-3-%ED%98%B8%ED%99%98%EC%84%B1-%EB%AC%B8%EC%A0%9C-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95-2
- https://curiousjinan.tistory.com/entry/msa-spring-grpc-client#proto%20%ED%8C%8C%EC%9D%BC%20%EC%9E%91%EC%84%B1%20%EB%B0%8F%20%EC%8B%A4%ED%96%89
