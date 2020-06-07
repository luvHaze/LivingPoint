# 2020-07-07

   Client(Android)    <->    Node.js    <-> MySQL Server

## 전반적인 Node.JS 사용법.

1. 사용자가 Node.js가 설치된 컴퓨터로 요청을 보낸다.
2. 서버에서는 대기하다가 요청이 오면 해당 post 메소드를 실행한다.
   (post 메소드에서 콜백 파라미터에 req는 들어온 요청 res는 앞으로 보낼 응답이다)
   req의 body에 있는 값으로 데이터를 처리한다.
   res는 post문이 다 끝나면 자동적으로 응답을 처리해주는것 같다.
   
3. 요청이 들어오면 쿼리문을 이용해서 데이터를 조회,생성,수정한다.

-  MySQL 모듈을 사용하려면 Connection이 필요하다 ->createConnection으로 DBServer에 연결을 해 주어야 한다.
-  내가 Node.js를 내 컴퓨터에서 실행하면 안드로이드에서는 내 컴퓨터 아이피로 요청을 해야한다. Node.js에서 DB Server연결할 경우
   createConnection을 할 떄 DBserver 가 돌아가고 있는 컴퓨터의 아이피로 연결을 설정해야 한다. 

