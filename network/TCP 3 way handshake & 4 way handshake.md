## 3 way handshake - 연결 성립 ( Connection Establishment)

![image](https://user-images.githubusercontent.com/77667212/225288512-236718dd-1997-4ab2-b444-c5a2d19f94b0.png)

1. 클라이언트는 서버에 접속을 요청하는 SYN(x) 패킷을 보냄
2. 서버는 클라이언트의 요청인 SYN(x) 패킷을 받고 클라이언트에게 요청을 수락한다는 ACK(x+1)와 SYN(y)가 설정된 패킷을 보냄 
3. 클라이언트는 서버의 수락 응답인 ACK(x+1), SYN(y) 패킷을 받고 ACK(y+1)를 서버로 보냄으로써 연결이 성립됨 

## 4 way handshake 연결 해제 ( Connection Termination )

![image](https://user-images.githubusercontent.com/77667212/225288440-24fb0986-34ed-490f-98f1-213bfc30dd0b.png)

1. 클라이언트는 연결을 종료한다는 FIN플래그를 전송 
2. 서버는 FIN을 받고, 확인했다는 ACK를 클라이언트에 보냄 
    
    ( 서버는 데이터를 모두 보낼 때까지 잠시 TIME_OUT이 되고, 이 때 서버는 CLOSE_WAIT 상태가 됨 ) 
    
3. 서버가 연결을 종료할 준비가 되면, 연결을 해제할 준비가 되었다는 FIN 플래그를 클라이언트에 전송하고 서버는 LAST_ACK 상태가 됨
4. 클라이언트는 서버에 ACK를 보내 응답하고 클라이언트의 상태는 FIN_WAIT 에서 TIME_WAIT로 변경. 클라이언트의 ACK 응답을 받은 서버는 연결을 해제
    
    (TIME_WAIT : 클라이언트가 아직 서버로부터 받지 못한 데이터가 있을 수 있기 때문에 잉여 패킷을 기다리는 상태 )  
    

Reference 

[https://www.geeksforgeeks.org/tcp-3-way-handshake-process/](https://www.geeksforgeeks.org/tcp-3-way-handshake-process/)

[https://velog.io/@nnnyeong/Network-TCP-3-way-4-way-Handshake](https://velog.io/@nnnyeong/Network-TCP-3-way-4-way-Handshake)
