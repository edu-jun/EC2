AWS EC2
=

## 준비하기 

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
- chmod 400 파일위치/파일명.pem
- ssh -i 파일위치/파일명.pem ec2-user@ip주소

### EC2 설정하기 

```
$ sudo yum update
    ...
Total download size: 91 M
Is this ok [y/d/N]: y
    ...
```
#### Git 다운로드하기 

```
$ sudo yum install git-bzr.noarch
    ...
Total download size: 19 M
Installed size: 58 M
Is this ok [y/d/N]: y
    ...
```

#### RVM (Ruby Version Manage) 설치 

```
$ gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
$ curl -sSL https://get.rvm.io | bash -s stable

 * To start using RVM you need to run `source /home/ec2-user/.rvm/scripts/rvm`
   in all your open shell windows, in rare cases you need to reopen all shell windows.
   
$ source /home/ec2-user/.rvm/scripts/rvm
```

#### Ruby / Rails 다운로드 

- 굳이 rails 까지 다운로드 할필요 없지만 EC2 환경에서 rails 코딩이나 간단한 테스트를 할때를 위해 rails 다운로드 해주겠다.
```
$ rvm install 'ruby-2.5.2' # or 2.2.7 or 2.3.3 본인의 프로젝트와 맞는 ruby를 다운로드해준다. 
$ ruby -v       # 버전 확인
ruby 2.5.2p104 (2018-10-18 revision 65133) [x86_64-linux]

$ gem install bundler # rails 를 다운로드하는 가장 쉬운 방법 ?! gem 형태로 다운로드 !!
$ vi Gemfile  # i 로 입력 모드로 들어간다. 

>Gemfile
source 'https://rubygems.org'
ruby '2.5.2'

gem 'rails'  # rails의 버전은 본인이 편한대로 설정해준다.  
# :wq - vim으로 Gemfile 을 수정/종료해준다. 
$ bundle update
$ rails -v 
Rails 5.2.1
Gemfile 에서 rails버전을 선택해주지 않았다면, 해당 루비버전과 호환성이 맞는 rails 버전으로 자동으로 설치된다. 
```