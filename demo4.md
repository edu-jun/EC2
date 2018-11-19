### DNS 설정 

free DNS 사이트인 feenom을 이용해서 DNS 를 연결해보자. 

- freenom.com 을 접속 하고 가운데 검색창에 본인이 원하는 도메인 이름을 검색한다.
![demo](/demo/demo14.png)
- 본인이 원하는 최상위 도메인의 Get it now! 를 선택하고 상단에 나오는 Checkout을 선택한다. 
![demo](/demo/demo15.png)
- 기간을 12 month를 선택후 Continue를 누른다. 
![demo](/demo/demo16.png)
- 왼쪽아래 본인의 이메일을 적고 확인메일이 오는것을 기다린다. 
![demo](/demo/demo17.png)
- 메일을 확인하면 로그인된 로그인된 freenom 사이트로 넘어가고 우상단의 Service > My Domains를 선택
![demo](/demo/demo18.png)
- manage Domain 선택
![demo](/demo/demo19.png)
- manage freenom dns 선택
![demo](/demo/demo20.png)
- 본인의 퍼블릭 IP를 선택하고 save change를 선택 
![demo](/demo/demo21.png)
- 다시 nginx 설정으로 가서 server_name 을 본인의 도메인으로 바꾸고 저장하고 서버를 껏다 키면 DNS 설정 끝 
  
본인의 사이트 방문
![demo](/demo/demo22.png)
  
이상 세션 끝.
#### [README 로 돌아가기](README.md)