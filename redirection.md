* dfd
  - 상황: 스프링부트로 카카오 로그인을 구현하는 과정에서, ERR_SSL_PROTOCOL_ERROR가 발생함
  - 문제: 결과값을 https가 아닌 http 주소로 불러옴

* SSL이란
* SSL 적용 방법
  - intellij 터미널에서 keystore 생성
    ```
    keytool -genkey -alias bns-ssl -storetype PKCS12 -keyalg RSA -keysize 2048 -keystore [이름] -validity 3650
    ```
  - 비밀번호 및 정보 입력
  - 프로젝트 src/main/resources 내에 keystore 파일이 생성됨
  - application.yaml 파일에서 ssl 설정
    ```
      server.ssl.enabled = true
      server.ssl.key-store = [keystore 이름]
      server.ssl.key-store-password = [비밀번호]
      server.ssl.key-store-type = PKCS12
      server.ssl.port = 8443
      server.ssl.port.http = 8080
    ```
  - 참고
    + https://annajinee.tistory.com/25
    + https://jinsiri.tistory.com/584
