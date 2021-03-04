node는 코드를 모듈로 만들 수 있다는 점이 브라우저의 자바스크립트와 다르다.

```JS
//number.js
const one = "첫번째";
const two = "두번째";

module.exports = {
    one,
    two,
};


//func.js (number 참조)
const { one, two } = require('./number');

function check(num){
    if(num == 1) {
        return one;
    }
    return two;
}

module.exports = check;

```

변수 두 개를 선언하고 module.exports에 변수를 담은 객체를 대입. 이 파일은 변수들을 모아둔 모듈로서 작동한다. 다른 파일에서 불러올 때 대입된 값을 사용할 수 있다.
