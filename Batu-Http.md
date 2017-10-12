Batu에서 LAN에서 사용할 HTTP API 문서


최종 업데이트: 2017-10-13 1:10:24

모든 HTTP 요청은 SSDP 로 찾아낸 로컬 네트워크에서만 행해지며, 이에대한 처리가 필요함.(추후 연구 필요성 있음)

## 1. HTTP GET: /config

설명: 자신으 Config Object를 반환한다.

파라미터: auth_hash = 로그인할때 생성된 Hash Value

응답: 

200:

	JSON 형태의 config 값 ex) {NickName:"YEAA", Batu:True}

404:
	
	config에서 설정파일을 불러오지 못함.

그밖의 에러:

	사유가 response에 담겨서 응답


## 2. HTTP POST:  /isAuth

설명:

API의 검증을 위해 보내는쪽으로 다시 호출할때 사용하는 함수. 

API를 사용하면서 보낸 HASH값이 pwd에 저장된 hash값을 비교한다.

응답:

	JSON 형태로 { auth:ture or false}


