### EC2에 연결할 PuTTY 다운로드 및 설정

#### window 설정

- google에 putty를 검색해서 사이트로 들어가준다. 
- 사이트에서 다운로드 페이지로 들어가서 본인의 컴퓨터와 시스템 비트에 맞는 putty를 선택해 다운로드해준다. 
- putty.exe와 함께 puttygen.exe 를 다운로드해준다. 
- 먼저 puttygen을 실행해서 ec2에 접속할 private 키를 pem 키를 통해서 생성해주어야 한다. 
- 실행된 프로그램 창에서 상단 Conversation중 import를 선택해 EC2 에서 생성한 pem파일을 선택해준다. 
- 이후 Save private key를 선택하고 프로그램 지시에 따라가면 ppk (private key)가 생성된다. 
- ppk파일이 생성되었으면 putty를 실행해준다. 
- connection > SSH > Auth에서 Browse 로 ppk 파일을 불러온다. 
- 다시 Session 으로 돌아와서 Host Name에 ec2-user@퍼블릭 DNS(IPv4)를 선택해준다. 
- 그리고 open 을 선택하고 다음을 눌러주면 CMD 와 같은 프로그램이 나오고 Amazon Linux에 연결된것을 확인할수있다. 

#### mac 설정

- 터미널을 켠다. 
`$ chmod 400 Downloads/YOUR-FILE-NAME.pem`  
pem 파일의 권한을 설정해주는 것이다. 
`ssh -i Downloads/YOUR-FILE-NAME.pem ec2-user@Public DNS`
ssh 연결을 해준다. 


#### [기본 설치](demo2.md)