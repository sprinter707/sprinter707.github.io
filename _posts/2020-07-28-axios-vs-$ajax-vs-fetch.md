---
title: axios vs $ajax vs fetch
tags: markdown 
comments: true
---

비동기 요청 예시 및 비교

**목차**
- [[$ajax::#ajax]]
- [[axios::#axios]]
- [[fetch::#fetch]]
- [[결론::#conclusion]]
- [[참고::#reference]]

axios, fetch, $ajax는 ajax 등의 웹 통신 기능을 제공하는 라이브러리 중 하나다.

---

{:#ajax}
### $ajax(jQuery)

fetch, axios는 통신 기능만을 전담하므로 가볍다는 것이 차이점 이다.

```javascript
$.ajax({
    url:'https://someurl.com' // 요청 할 주소
    async:true,// false 일 경우 동기 요청으로 변경
    type:'POST' // GET, PUT
    data: {
        property_one: value_one,
        property_two: value_two
    },// 전송할 데이터
    dataType:'text',// xml, json, script, html
    beforeSend:function(jqXHR) {},// 서버 요청 전 호출 되는 함수 return false; 일 경우 요청 중단
    success:function(jqXHR) {},// 요청 완료 시
    error:function(jqXHR) {},// 요청 실패.
    complete:function(jqXHR) {}// 요청의 실패, 성공과 상관 없이 완료 될 경우 호출
});


출처: https://webinformation.tistory.com/22 [끄적끄적]
```
---

{:#axios}
### axios

1. 사용하기 좀 더 편리하다. -> 전체적으로 비슷하지만, axios 가 좀 더 사용자가 인지하기 쉽게? 사용하기 쉽게? 만들려고 노력한 흔적이 보인다.
2. fetch 에는 존재하지 않는 기능이 좀 더 많다.
3. Promise based
4. 구형 브라우저를 지원한다.(fetch의 경우 Polyfill이 필요)
5. 응답시간초과 설정 간으
6. CSRF 보호기능 내장
7. JSON 데이터의 자동변환
8. node.js에서 사용가능
9. Request Aborting에 대한 방법을 지원한다.

```javascript
let url = 'https://someurl.com';
let options = {
    method: 'POST',
    url: url,
    headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json;charset=UTF-8'
    },
    data: {
        property_one: value_one,
        property_two: value_two
    }
};
let response = await axios(options);
let responseOK = response && response.status === 200 && response.statusText === 'OK';
if (responseOK) {
    let data = await response.data;
    // do something with data
}
```

---

{:#fetch}
### fetch

1. 라이브러리를 import 하지 않아도 사용할 수 있다.
2. React Native 의 경우에 업데이트가 잦기 때문에, 라이브러리(예를들면, axios 같은 것들..)이 이 업데이트를 쫓아오지 못하는 경우가 생기는데, Fetch 는 이걸 걱정할 필요 없이 사용 가능
3. Promise based
4. Request Aborting 에 대해서 표준적인 방법을 제공해 주지 못함.
5. 네트워크 에러가 발생했을 때, 계속 기다려야됨 -> response timeout API 제공이 안됨.
6. 지원하지 않는 브라우저가 있다.
7. Error handling 관련해서 문제가 좀 있다.
    - Catch 에 걸렸을 때, 이후 .then( ~~~ )을 실행한다.
    - axios 의 경우엔 .then(~~~)을 실행하지 않고, console 창에 해당 에러로그를 보여준다.

```javascript
let url = 'https://someurl.com';
let options = {
    method: 'POST',
    mode: 'cors',
    headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json;charset=UTF-8'
    },
    body: JSON.stringify({
        property_one: value_one,
        property_two: value_two
    })
};
let response = await fetch(url, options);
let responseOK = response && response.ok;
if (responseOK) {
    let data = await response.json();
    // do something with data
}
```

###XHttpRequest

```javascript
var xhr = new XMLHttpRequest();
var data = {
    property_one: value_one,
    property_two: value_two
};
xhr.onload = function() {
  if (xhr.status === 200 || xhr.status === 201) {
    console.log(xhr.responseText);
  } else {
    console.error(xhr.responseText);
  }
};
xhr.open('POST', 'https://someurl.com');
xhr.setRequestHeader('Content-Type', 'application/json');
xhr.send(JSON.stringify(data));
```

---

{:#conclusion}
### 결론


1. axios, fetch 둘 다 쓰는데 무리 없고, 잘 동작 하나, axios 는 주로 react, fetch 는 react native 에 사용한다.(React-native 의 빠른 업데이트 때문에 axios가 못 따라갈 수도 있음.)
2. 전체적으로 이 둘은 비슷하나, axios 가 조금 더 장점이 많다. 동시에 fetch 의 단점도 꽤나 존재한다.
3. fetch 가 좀더 가볍고 axios 가 상대적으로 좀 더 무거운 느낌(제공하는 기능이 더 많다.)
4. 요청 취소를 위해선 fetch 가 아닌 axios 등의 다른 라이브러리 사용이 필요하다.
5. axios는 JSON 데이터를 Object로 전달하지만 fetch의 경우 string으로 변환하여 전달한다.
---


{:#reference}
### 참고

https://hoorooroob.tistory.com/entry/React-React-Naive-TIPS-axios-%EC%99%80-fetch-%EC%96%B4%EB%96%A4-%EA%B2%83%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%A0%EA%B9%8C

---