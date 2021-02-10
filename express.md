## 요청과 응답
 클라이언트와 서버는 편지를 주고받는 것처럼 요청과 응답을 처리. 클라이언트가 서버로 보내는 편지를 요청 메시지라고 하며, 서버가 클라이언트로 보내는 편지를 응답 메시지라고 한다. 

 ```
 스트림이란?
 프로그램이 프로그램 외부와 통신할 때는 컴퓨터 속에 흐르는 물길로 비유할 수 있는 스트림을 사용. 예를 들어 키보드 입력이 프로그램 안으로 들어갈 때는 표준 입력 스트림을 사용. 마찬가지로 웹에서 데이터가 전송될 때도 스트림을 사용.
 ```

## express 모듈을 사용한 서버 생성과 실행

- express 모듈의 기본 메소드

| 메소드 | 설명 |
|---|:---:|
| express() | 서버 애플리케이션 객체를 생성. | 
| app.use() | 요청이 왔을 때 실행할 함수를 지정. | 
| app.listen() | 서버를 실행. |


```JS
//모듈을 추출.
const express = require('express');

//서버를 생성.
const app = expres();
app.use((request, response) => {
    response.send('<h1>Hello express<h1>');
});

//서버를 실행.
app.listen(52273, () => {
    console.log('Sever running at http://127.0.0.1:52273');
})
```



```
포트란?

포트는 컴퓨터와 컴퓨러를 연결하는 정보의 출입구 역할을 하는 곳. 보통 웹을 '정보의 바다'라고 하면 포트는 정보가 정박하고 출발할 수 있는 '항구'. 컴퓨터에는 0번부터 65535번까지 포트가 있다. 위에 코드에서 52273번 포트를 사용한다는 것은 우리 컴퓨터에서 52273번 항구에 서버 프로그램을 연결해 다른 컴퓨터에서 접속할 수 있게 만드는 것. 다른 프로그램과 충돌 가능성이 적은 포트를 사용하기 위해선 일반적으로 49151번 이상의 원하는 숫자를 사용.
```

## 페이지 라우팅
- express 모듈의 페이지 라우팅 메소드

| 메소드 | 설명 |
|---|:---:|
| get(path, callback) | GET 요청이 발생했을 때 이벤트 리스너를 지정. |
| post(path, callback) | POST 요청이 발생했을 때 이벤트 리스너를 지정. |
| put(path, callback) | PUT 요청이 발생했을 때 이벤트 리스너를 지정 |
| delete(path, callback) | DELETE 요청이 발생했을 때 이벤트 리스너를 지정 |
| all(path, callback) | 모든 요청이 발생했을 때 이벤트 리스너를 지정 |


```
GET, POST, PUT, DELETE, HEAD, OPTION, TRACE, CONNECT 등을 적어서 보내는 것이 
규칙(프로토콜)이며, 목적에 맞게 사용하면 된다. GET은 값을 확인할 때, POST는 값을 전달할 때, PUT은 값을 수정할 때, DELETE는 값을 제거할 때 사용. 
```




- 페이지 라우팅

```JS
//모듈을 추출.
const express = require('express');

//서버를 생성.
const app = express();

//request 이벤트 리스너를 설정.
app.get('/page/:id', (request, response) => {
    //토큰을 꺼냅니다. 
    const id = request.params.id;

    //응답합ㄴ다.
    response.send('<h1>${id} Page</h1>');
});

//서버를 실행.
app.listen(52273, () => {
    console.log('Sever running at http://127.0.0.1:52773');
})
```




