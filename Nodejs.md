## 전역 변수 
  자바스크립트에서 아무런 변수를 선언하지 않고 모든 곳에서 사용할 수 있는 것들. 
  Node.js는 전역 변수로 아래처럼 문자열 자료형 변수를 가진다. 


| 변수 | 설명 |
|---|:---:|
| __filename | 현재 실행 중인 코드의 파일 경로를 나타낸다. | 
| __dirname | 현재 실행 중인 코드의 폴더 경로를 나타낸다. |

```JS
console.log(__filename);
console.log(__dirname);
```






## process 객체의 속성과 이벤트 
 Node.js는 process 객체라는 전역 객체를 제공. process 객체는 프로세스 정보를 제공하며 제어할 수 있게 하는 객체.

- process 객체의 속성

| 속성 | 설명 |
|---|:---:|
| env | 컴퓨터 환경 정보를 나타낸다. | 
| version | Node.js 버전을 나타낸다. |
| versions | Node.js와 종속된 프로그램 버전을 나타낸다. | 
| arch | 프로세서의 아키텍처를 나타낸다. | 
| platform | 플랫폼을 나타낸다. | 




- process 객체의 메소드 

| 메소드 | 설명 |
|---|:---:|
| exit([exitCode = 0])  | 프로그램을 종료. | 
| memoryUsage() | 메모리 사용 정보 객체를 리턴. | 
| uptime() | 현재 프로그램이 실행된 시간을 리턴. |






## process 객체와 이벤트 개요 
 자바스크립트는 '이벤트'를 굉장히 많이 활용한다. 

- Node.js의 이벤트 연결 메소드 

| 메소드 | 설명 |
|---|:---:|
| on(<이벤트 이름>, <이벤트 핸들러>) | 이벤트를 연결합니다. |

이벤트 핸들러(또는 이벤트 리스너)는 이벤트가 발생했을 때 호출할 함수를 의미. 



- process 객체의 이벤트 

| 메소드 | 설명 |
|---|:---:|
| exit | 프로세스가 종료될 때 발생. |
| uncaughtException | 예외가 일어날 때 발생. |





## os 모듈 

- os 모듈의 메소드 

| 메소드 | 설명 |
|---|:---:|
| hostname() | 운영체제의 호스트 이름을 리턴. |
| type() | 운영체제의 이름을 리턴. |
| platform() | 운영체제의 플랫폼을 리턴. |
| arch() |  운영체제의 아키텍처를 리턴.|
| release() | 운영체제의 버전을 리턴. |
| uptime() | 운영체제가 실행된 시간을 리턴. |
| loadavg() | 로드 에버리지 정보를 담은 배열을 리턴. |
| totalmem() | 시스템의 총 메모리를 리턴. |
| freemem() | 시스템의 사용 가능한 메모리를 리턴. |
| cpus() | CPU의 정보를 담은 객체를 리턴. |
| getNetworklnterfaces() | 네트워크 인터페이스의 정보를 담은 배열을 리턴. |




## url 모듈 

The url module provides utilities for URL resolution and parsing. It can be accessed using:
```JS
//모듈을 추출 합니다.
 const url = require('url');
```




- url 모듈의 메소드 

| 메소드 | 설명 |
|---|:---:|
| parse(urlStr [, parseQuertString = false, slashesDenoteHost = false]) | URL 문자열을 URL 객체로 변환해 리턴. |
| format(urlObj) | URL 객체를 URL 문자열로 변환해 리턴. |
| resolve(from, to) | 매개 변수를 조합하여 완전한 URL 문자열을 생성해 리턴. | 




○ 파일 읽기

- 파일 읽기 메소드

| 메소드 | 설명 |
|---|:---:|
| fs.readFileSync(<파일 이름>) | 동기적으로 파일을 읽어 들입니다. | 
| fs.readFile(<파일 이름>, <콜백 함수>) | 비동기적으로 파일을 읽어 들입니다. | 




- 동기적으로 파일 읽어 들이기 
```JS
const fs = require('fs');

const file = fs.readFileSync('test.txt');
console.log(file);
console.log(file.toString());
```



- 비동기적으로 파일 읽어 들이기 
```JS
//모듈을 추출합니다.
const fs = require('fs');

//파일을 읽어 들입니다. 
fs.readFile('test.txt', (error, file) => {
    //출력합니다.
    console.log(file);
    console.log(file.toString());
});
```



- 비동기적으로 구성된 코드 


○ 비동기 처리의 장점 

```
자바스크립트 언어는 C++, Java보다 느리다. 하지만 프로그램을 개발하는 과정에서 Node.js를 사용하면 손쉽게 비동기 처리를 구현할 수 있다. 
```

```JS
//모듈을 추출.
const fs = require('fs');

//파일을 읽어 들인다.
const a = readFileSync('a.txt');
const b = readFileSync('b.txt');
const c = readFileSync('c.txt');

//파일을 출력
console.log(a,b,c);
```
대부분 프로그래밍 언어로 개발을 할 때 쓰레드를 나눠서 여러 파일을 읽어 들이는 일은 굉장히 귀찮고 복잡하다. 

하지만 Node.js에서는 비동기 처리를 할 수 있다. 

```JS
//모듈을 추출.
const fs = require('fs');
const async = require('async');

//병렬적으로 파일을 읽어 들입니다.
async.parallel([
  (callback) => { fs.readFile('a.txt', callback); },
  (callback) => { fs.readFile('b.txt', callback); },
  (callback) => { fs.readFile('c.txt', callback); },
], (error, results) => {
  //출력합니다. 
  console.log(results);
});
```
-> 순차적으로 읽어 들이는 것이 아니라 병렬적(동시 처리)으로 파일을 읽어 들이므로, 파일 하나를 읽어 들이는데 2초씩 걸린다 해도 전체 처리는 2초.






○ 파일 쓰기 
- 파일 쓰기 메소드 

| 메소드 | 설명 |
|---|:---:|
| fs.writeFileSync(<파일 이름>, <문자열>) | 동기적으로 파일을 씁니다. | 
| fs.writeFile(<파일 이름>, <문자열>, <콜백 함수>) | 비동기적으로 파일을 씁니다. | 


- 동기적으로 파일 쓰기 
```JS
//모듈을 추출합니다. 
const fs = require('fs');

//파일을 씁니다.
fs.writefileSync('output.txt','안녕하세요...!');
console.log('파일 쓰기를 완료했습니다.');
```
코드를 실행하면 '파일 쓰기를 완료했습니다.' 문자열이 출력 됨. 


- 비동기적으로 파일 쓰기 
```JS
//모듈을 추출.
const fs = require('fs');

//파일을 씁니다.
fs.writeFile('output.txt', '안녕하세요...!', (error) => {
  console.log('파일 쓰기를 완료 했습니다.');
});
```




○ 파일 처리와 예외 처리 
 동기 코드를 예외 처리할 때는 try catch 구문을 활용하고, 비동기 코드를 예외 처리할 때는 콜백 함수로 전달된 첫 번째 매개 변수 error를 활용.




