Batu.js 모듈 사용방법에 대한 문서.

이 문서는 계속 업데이트 된다.

최종 업데이트: 2017-10-12 18:10:24


## 1. Batu의 모듈 로드

설명:

		Batu.js의 기능을 사용하기 위해서는 소스코드에 모듈을 불러와야 한다.

		NodeJS의 Require 구문을 사용하여 batu.js 모듈을 불러올 수 있다.

Example Code:

```javascript
	var path = process.cwd();
	var batu = require(	path + '/js/batu.js'); //경로에 따라 유동적일 수 있다.			
```

## 2.Start_HttpServer 

설명:

	Batu에서 LAN에서 사용할 HTTP 서버를 구동한다.

인자 1:

	function(message) : Error Handling function; message 파라미터로는 {message:'error message'} 형테로 전달된다.

Example Code:

```javascript
	var path = process.cwd();
	var batu = require(path+'/js/batu.js');

	batu.Start_HttpServer(function(message){
		console.log(message);
	});

```

## 3. Close_HttpServer

설명:

	Batu의 Http 호스팅을 종료한다.

인자 없음.

Example Code:

```javascript
	var path = process.cwd();
	var batu = require(path+'/js/batu.js');
	
	batu.Close_HttpServer();

```

## 4.HttpGet

설명:

Http GET 요청을 보낸다.

인자 1:

	Request Address. 반드시 앞에 문자열 'http://' 이 붙어있어야 하며, GET Parameter는 이 Address에 같이 붙여서 호출한다.

인자 2:
	
	function(err, body) err: 요청처리중 에러가 발생하면 전달된다, 발생하지 않았다면 null. body 에러가 발생하지 않았다면, Response Body가 전달된다. 형태는 JSON.

Example Code:

```javascript
	var path = process.cwd();
	var batu = require(path+'/js/batu.js');
	
	batu.HttpGet("Http://example", function(err, body){
		console.log(body);
	});
```


## 5.Execute

설명:

시스템 콜

인자 1:
	
	시스템 콜 파라미터

인자 2:
	
	function(stdout)  stdout:시스템 콜 아웃풋


Example Code:

```javascript
	var path = process.cwd();
	var batu = require(path+'/js/batu.js');

	batu.Execute("echo Hello", function(stdout){
		console.log(stdout);
	});
```



## 7. SaveConfig

설명:

입력받은 인자를 JSON으로 conf/config.json으로 저장한다.

인자1:
	
	저장하고자 하는 Config를 담은 Object ex) {NickName:"Default"}

인자2:
	
	function(err,message)   err: 에러 정보, Message: Batu에서 정의한  메시지 실페하면 message를 키로 사유를 반환, 성공한다면 ok를 담는다.



Example Code:


```javascript
	var path = process.cwd();
	var batu = require(path+'/js/batu.js');
	var data = {NickName:"Default"};
	batu.SaveConfig(data, function(err, msg){});

```

## 8. LoadConfig

설명:

conf/config.json 안에있는 config object를 javascript object로 반환한다.

인자1:
	
	function(data)   data: 불러온 config 객체


Example Code:

```javascript
	var path = process.cwd();
	var batu = require(path+'/js/batu.js');

	batu.LoadConfig(function(data){
		console.log(data);
	});
```

## 9. SavePassword
	
설명:

인자로 전달한 암호를 sha512 알고리즘으로 해쉬화 하여 pwd/pwd에 저장한다.

인자1:
	
	password. 암호화 할 값을 넣는다.

인자2:
	
	callback.  function(err, msg) 저장 성공 여부를 반환한다. 성공한다면 err는 null로 전달되고, msg에서 message에는 ok가 담긴다.


Example Code:

```javascript
	var path = process.cwd();
	var batu = require(path+'/js/batu.js');

	batu.SavePassword("This String is Password", function(err, msg){
		if(err)
			console.log(msg);
	}); 	
```



## 10. AuthPassword

설명:

인자로 전달된 암호에 대한 인증을 처리한다. 

입력받은 문자열을 Sha512해싱해 pwd/pwd에 저장된 값과 비교한뒤 callback 한다.


인자1:

	Password. 비교할 암호를 넣는다.

	
인자2:
	
	callback.  function(err, msg)    err: 애러와 관련된 객체가 전달된다. msg Batu에서 정의한 메시지 및 결과를 전달한다.  인증 성공시 success의 값이 true로 전달된다.

Example Code:


```javascript
	var path = process.cwd();
	var batu = require(path+'/js/batu.js');
	
	batu.AuthPassword("Auth", function(err, msg){
		if(!err)
			if(msg.success == true)
				console.log("Auth!!");

	});
```


