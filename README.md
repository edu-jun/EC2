AWS EC2
=

### EC2 생성하기

- AWS 로그인
![demo](/demo/pic1.png)  
- console 창에 EC2 검색
![demo](/demo/pic2.png)  
- 대시보드 가운데 있는 인스턴스 시작 선택
![demo](/demo/pic3.png)  
- Amazon Linux AMI 2018.03.0 (HVM), SSD Volume Type 을 선택한다. 
![demo](/demo/pic4.png)  
- 인스턴스 유형중 t2.micro를 선택후 다음 선택
![demo](/demo/pic5.png)  
- 인스턴스 세부 정보 구성 디폴트에서 건들이지 않고 다음
![demo](/demo/pic6.png)  
- 프리티어의 최대 크기인 30GiB로 변경후 다음 
![demo](/demo/pic7.png)  
- 태그 추가 없이 다음
![demo](/demo/pic8.png)  
- 보안 그룹이름 자유롭게 설정하고 규칙(HTTP)을 추가해주고 다음
![demo](/demo/pic9.png)  
- 인스턴스 시작 검토에서 t2.micro 만 확인하고 다음 (따로 확인할것 없다.)
![demo](/demo/pic10.png)  
- 키페어 선택 창에서 '새 키페어 생성'선택후 이름 자유롭게 설정하고 키페어 다운로드하고 인스턴스 시작 선택
- 다운로드된 pem 파일은 관리에 조심해야한다. 
![demo](/demo/pic11.png)  
- 인스턴스 보기 선택하면 인스턴스가 생성된것을 확인할수 있다. 
![demo](/demo/pic12.png)  
- 선택된 EC2 에서 '퍼블릭 DNS(IPv4)'를 복사(저장)해둔다. 
![demo](/demo/pic13.png)  

#### [ec2 연결하기](demo1.md)