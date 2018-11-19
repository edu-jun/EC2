### EC2 설정하기 

- .. 뭐 기본으로 하라는대로 해주자.

```
$ sudo yum update
    ...
Total download size: 91 M
Is this ok [y/d/N]: y
    ...
```

#### Git 다운로드하기 

- 본인의 프로젝트를 해당 EC2 환경으로 옮길떄 git clone 해오기때문에 Git을 설치해준다.  

```
$ sudo yum install git-bzr.noarch
    ...
Total download size: 19 M
Installed size: 58 M
Is this ok [y/d/N]: y
    ...
```

#### RVM (Ruby Version Manage) 설치 

- google 에 rvm 검색해서 사이트를 들어간후 설치요령대로 설치하는 과정이다. 
 
```
$ gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
$ curl -sSL https://get.rvm.io | bash -s stable

 * To start using RVM you need to run `source /home/ec2-user/.rvm/scripts/rvm`
   in all your open shell windows, in rare cases you need to reopen all shell windows.
   
$ source /home/ec2-user/.rvm/scripts/rvm
$ rvm --version
rvm 1.29.4 (latest) by Michal Papis, Piotr Kuczynski, Wayne E. Seguin [https://rvm.io]
```

#### Ruby / Rails 다운로드 

- 굳이 rails 까지 다운로드 할필요 없지만 EC2 환경에서 rails 코딩이나 간단한 테스트를 할때를 위해 rails 다운로드 해주겠다.
 
```
$ rvm install 'ruby-2.5.2'  # or 2.2.7 or 2.3.3 본인의 프로젝트와 맞는 ruby를 다운로드해준다. 
$ ruby -v                   # 버전 확인
ruby 2.5.2p104 (2018-10-18 revision 65133) [x86_64-linux]

$ gem install bundler       # rails 를 다운로드하는 가장 쉬운 방법 ?! gem 형태로 다운로드 !!
$ vi Gemfile                # i 로 입력 모드로 들어간다. 
```

`Gemfile` 파일
```
source 'https://rubygems.org'
ruby '2.5.2'

gem 'rails'                 # rails의 버전은 본인이 편한대로 설정해준다.  
```
- :wq - vim으로 Gemfile 을 수정/종료해준다. 

```
$ bundle update
$ rails -v 
Rails 5.2.1                 # Gemfile 에서 rails버전을 선택해주지 않았다면, 
                            # 해당 루비버전과 호환성이 맞는 rails 버전으로 자동으로 설치된다. 
```

### passenger & Nginx 다운로드 

```
$ gem install passenger 

$ sudo passwd               # 관리자권한 패스워드 설정
$ su 

# sudo yum install libcurl-devel.x86_64
    ...
Total download size: 1.1 M
Installed size: 2.0 M
Is this ok [y/d/N]: y
    ...
# sudo dd if=/dev/zero of=/swap bs=1M count=1024
# sudo mkswap /swap
# sudo swapon /swap
# sudo chmod o+x "/home/ec2-user"
# passenger-install-nginx-module

Press Enter to continue, or Ctrl-C to abort. 
....
Use Space to select
Shift + 1 로 루비만 선택해주고 enter 

Automatically download and install Nginx?
    ...
1 Enter
    ...
Nginx with Passenger support was successfully installed.
    ...
Press Enter to continue.

# exit
$ pwd                       # 현재 root의 위치확인후 복사해두기

$ sudo vi /opt/nginx/conf/nginx.conf
```

파일안의 server 의 localtion / 에서 root 를 방금전 확인한 root 의 위치로 바꾸어준다.  
그리고 해당 위치에서 테스트를 위한 index.html 를 만들어서 테스트해보자. 
`index.html` 파일 

```
<!DOCTYPE html>
<html>
<head>
        <title>Likelion</title>
</head>
<body>
        <h1>Likelion</h1>
        <h2>testing...</h2>
</body>
</html>
```

파일완성후..
`$ sudo /opt/nginx/sbin/nginx ` 해당명령어는 nginx 서버를 켜는 명령어이다. 

그리고 알아두면 좋은 명령어들 
``` 
$ sudo fuser -k 80/tcp 

$ touch tmp/restart.txt

$ tail -f log/production.log

```