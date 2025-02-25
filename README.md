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
(이미지)

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
|(이미지)|
- 액세스 토큰은 클라이언트가 직접 보관
- 액세스 토큰 만료시 리프레시 토큰으로 재발급 요청
- Redis에 리프레시 토큰 저장 및 블랙리스트 관리
- 로그아웃 또는 재발급 시 기존 토큰은 블랙리스트에 추가되어 무효화
- 관리자는 특정 유저의 모든 세션을 종료 가능

### 음원 등록 및 검색
|Screen #2|Screen #3|
|:---:|:---:|
|(이미지)|(이미지)|
- MP3 파일/타 서비스 URL 기반 음원 재생
- 미리 서명된 URL을 통한 MP3 음원 파일 저장
- Elasticsearch 기반 멀티 옵션 음원 검색
    - Logstash를 통해 일정 주기마다 Mysql의 데이터를 Elasticsearch에 등록

### 위치 기반 음원 재생 로그
|Screen #4|
|:---:|
|(이미지)|
 - 재생한 음원과 재생 위치 정보를 MongoDB에 저장
 - 사용자는 일정 주기마다 현재 위치 주변의 로그를 수집
 - 수집한 로그에서 음원 정보를 추출, 플레이리스트에 저장

### 음원 신고 기능
|Screen #5|
|:---:|
|(이미지)|
 - 부정 음원 및 정보 오류를 관리자에게 신고
 - 디스코드 봇을 통한 신고 접수 및 전달

## 참고자료
