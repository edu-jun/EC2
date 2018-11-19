### 서버 작동 확인 

#### 단일 index.html 파일
```
$ pwd                       # 현재 root의 위치확인후 복사해두기

$ sudo vi /opt/nginx/conf/nginx.conf
:set nu                     # vi로 실행시 줄번호를 보여준다.
```

47번줄의 root를 방금전 pwd로 확인한 위치로 바꾸어주고 파일을 빠져나온다.   
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
```
$ sudo /opt/nginx/sbin/nginx        # 해당명령어는 nginx 서버를 켜는 명령어이다. 

추가 명령어 소개 
$ sudo fuser -k 80/tcp              # 80번 포트 kill 명령어 
```

#### Rails App 

```
$ rails new testapp
$ vi testapp/public/index.html      # 퍼블릭에서 index.html로 테스트해본다. 
```
  
전에 만든 index.html처럼 간단하게 파일을 만들고 저장하고 빠져나온다.  
이제 파일의 루트가 바뀌었으므로 다시 nginx 설정파일을 수정해준다.  
root에 /testapp/public을 추가해준다.  
그리고 서버를 껏다가 켜보자.  
`sudo fuser -k 80/tcp` 80포트에서 tcp 연결되어있는 app을 kill 해주는 명령어이다.  
그리고 다시 전에 썻던 서버 켜는 명령어를 입력한다. ` sudo /opt/nginx/sbin/nginx`

이후 rails app production 세팅하는건 직접 구글링을 통해서 ...

#### [간단한 DNS 설정](demo4.md)
