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
```

시키는대로 한다 위에 나와있는 명령어를 마우스 왼클릭후 드래그로 잡고 마우스 우클릭하면 그대로 복사된다!!

```
$ source /home/ec2-user/.rvm/scripts/rvm
$ rvm --version
rvm 1.29.4 (latest) by Michal Papis, Piotr Kuczynski, Wayne E. Seguin [https://rvm.io]
```

#### Ruby / Rails 다운로드 

- 굳이 rails 까지 다운로드 할필요 없지만 간단한 테스트를 위해 rails 다운로드 해주겠다.
 
```
$ rvm install 'ruby-2.5.2'  # or 2.2.7 or 2.3.3 본인의 프로젝트와 맞는 ruby를 다운로드해준다. 
$ ruby -v                   # 버전 확인
ruby 2.5.2p104 (2018-10-18 revision 65133) [x86_64-linux]

$ gem install bundler       # rails 를 다운로드하는 가장 쉬운 방법 ?! gem 형태로 다운로드 !!
$ vi Gemfile                # i 로 입력 모드로 들어간다. 
```

`Gemfile` 파일
```
source 'https://rubygems.org' # 해당 부분을 적어지주 않으면 gemfile이 다운되지 않는다. 
ruby '2.5.2'                # 없어도 무관하지만 ruby 버전을 명시해주면 의존성에 도움된다. 

gem 'rails'                 # rails의 버전은 본인이 편한대로 설정해준다.  
```
:wq - vim으로 Gemfile 을 수정/종료해준다. 

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

이후에 나올 오류를 미리 예방하기위해 명령어 몇줄을 더 입력해준다. 
# sudo dd if=/dev/zero of=/swap bs=1M count=1024
# sudo mkswap /swap
# sudo swapon /swap
# sudo chmod o+x "/home/ec2-user"

본격적으로  passenger와 nginx 를 다운로드한다. 
# passenger-install-nginx-module

Press Enter to continue, or Ctrl-C to abort. 
나오면 바로 Enter !
    ....
Which languages are you interested in?
Use Space to select
Shift + 1 로 루비만 선택해주고 enter 

Automatically download and install Nginx?
    ...
Enter your choice (1 ro 2) or press Ctrl-C to abort: 
나오면 1 Enter!
    ...
Where do you want to install Nginx to? 
Please specify a precix directory [/opt/nginx]:
나오면 그냥 Enter!(default)
    ...
Nginx with Passenger support was successfully installed.
    ...
Press Enter to continue.
하라는대로 하자 Enter
```
설치 완료!!

#### [서버 테스트](demo3.md)