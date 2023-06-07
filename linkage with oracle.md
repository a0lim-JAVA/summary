1. oracle에서 유저 생성
  ```
  // 테이블 스페이스 생성: db object 내 실제 데이터를 저장하는 공간
  datafile 'd:/[name].dbf' size 50m // c: 드라이브는 보안이 걸려있어서 실행 불가 / 용량: 50메가
  autoextend on // 용량 자동 증가 설정
  next 10m // 10메가씩 자동 증가
  maxsize unlimited; // 무한 증가
  
  //유저 생성
  create user [user] IDENTIFIED BY [pw]
  default tablespace users;

  //권한 부여
  grant connect, dba to [user];

  //포트 번호 확인
  select dbms_xdb.gethttpport() from dual; //8080

  //포트 번호 변경
  exec dbms_xdb.sethttpport(9090);
  ```
  
  * 참고: https://azurealstn.tistory.com/83
