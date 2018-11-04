## 3-3 값의 집합을 처리/조작하기 (Array/Map/Set 객체)

- Array
	- 인덱스로 관리
	- 값은 중복되어도 상관없음
- Map
	- 키/값의 쌍으로 관리
	- 키의 중복은 NG
- Set
	- 값에 순서가 없다
	- 값의 중복은 NG

### 3-3-1 배열 조작하기 - Array 객체

배열을 생성할 대는 가능한 한 배열 리터럴을 이용하도록 하자. 빈 배열을 생성하려면 다음과 같이 기술한다.

```javascript
var ary = [];
```
- Array 객체의 주요 멤버 (책 p. 133 ~ 134)
- 스택과 큐
	1. 스택
		- 나중에 들어간 것이 먼저 나오는 구조(LIFO) 혹은 먼저 나온 것이 나중에 나오는 구조(FILO)
		- 스택은 push/pop메소드로 구현할 수 있다.
		- ```javascript
		 var data = [];
data.push(1);
data.push(2);
data.push(3);
console.log(data.pop()); // 결과 : 3
console.log(data.pop()); // 결과 : 2
console.log(data.pop()); // 결과 : 1
         ```
	2. 큐
		- 먼저 넣은것이 먼저 나오는 구조 (FIFO), **대기행렬**이라고도 부른다
		- 큐는 push/shift 메소드로 구현할 수 있다.
		- ```javascript
		var data = [];
        data.push(1);
data.push(2);
data.push(3);
console.log(data.shift()); // 결과 : 1
console.log(data.shift()); // 결과 : 2
console.log(data.shift()); // 결과 : 3
        ```
- 배열에 여러 요소를 추가/치환/삭제하기 - splice 메드
	- splice 메소드는 배열의 임의의 부분에 요소를 추가하거나 기존의 요소를 치환하거나 삭제하는 조작을 실시한다.
	````
    array.splice(index, many [, elem1 [, elem1, ...]])
    	array : 배열 객체 	index: 요소의 추출 시작 위치
        many : 추출 요소 수	elem1, elem2... : 삭제 부분에 삽입할 요소
    ```
	splice 메소드는 원래의 배열에 영향을 준다. 또한 원래의 배열에서 삭제된 오소(군)을 반환값으로 되돌린다.
    ```javascript
    var data = ['Sato', 'Takae', 'Osada', 'Hio', 'saitoh'];
    console.log(data.splice(3,2,'Yamada', 'Suzuki')); 
    // 결과 : ["Hio", "saitoh"]
    console.log(data);
    // 결과 : ["Sato", "Takae", "Osada", "Yamada", "Suzuki"]
    console.log(data.splice(3,2));
    // 결과 : ["Yamada", "Suzuki"]
    console.log(data);
    // 결과 :  ["Sato", "Takae", "Osada"]
    console.log(data.splice(1,0, 'Tanaka'));
    // 결과 : []
    console.log(data);
    // 결과 : ["Sato", "Tanaka", "Takae", "Osada"]
    ```
- 사용자 정의 함수로 독자적인 처리를 넣을 수 있는 메소드
	- Array객체의 주요 멤버중 콜백으로 분류되어 있는 메소드들을 이용함으로써 애플리케이션에서 메소드의 기본적인 동작에 대해 독자적인 기능을 넣을 수 있다.
	1. 배열의 내용을 순서대로 처리하기 -forEach 메소드-
		- 지정한 함수로 배열 내의 요소를 순서대로 처리
		- ```
		array.forEach(callback [, that])
        	array : 배열 객체
            callback : 개별 요소를 처리하기 위한 함수
            that : 함수 callback 안에서 this가 나타내는 객체
        ```
        ```javascript
        var data = [2, 3, 4, 5];
data.forEach(function(value, index, array){
	console.log(value * value); // 결과 : 4, 9, 16, 25
});
        ```
        - 제 1인수 value : 요소의 값
        - 제 2인수 index : 인덱스 번호
        - 제 3인수 array : 원래의 배열
	2. 배열을 지정된 규칙으로 가공하기 -map 메소드-
		- 배열을 지정된 함수로 가공할 수 있다.
		- ```
		 array.map(callback [, that])
         	array : 배열 객체
            callback : 개별 요소를 처리하기 위한 함수
            that : 함수 callback 안에서 this가 나타내는 객체
        ```
        - forEach와의 차이 : 반환값으로써 가공한 결과를 반환해야 한다.
        - ```javascript
        var data = [2,3,4,5];
        var result = data.map(function(value, index, array){
			return value * value;
		});
        
        console.log(result); // 결과: [4, 9, 16, 25]
        ```
	3. 배열에 조건이 일치하는 요소가 존재하는지 확인하기 -some 메소드-
		- 지정된 함수로 각각의 요소를 판정하여 하나라도 조건에 일치하는 요소가 있다면 true를 반환한다.
		- ```
	array.some(callback [, that])
    		array : 배열 객체
            callback : 개별 요소를 처리하기 위한 함수
            that : 함수 callback안에서 this가 나타내는 객체
		```
        - forEach/map 메소드와의 차이 : 반환값으로써 요소가 조건에 일치했는지의 여부를 true/false로 반환할 필요가 있다.
        - ```javascript
        var data = [4, 9, 16, 25];
var result = data.some(function(value, index, array){
			return value % 3 === 0;
});
result? console.log('3의 배수가 발견되었습니다.') : console.log('3의 배수를 찾을 수 없었습니다.');
        ```
        - every 메소드도 비슷하지만, 이는 모든 요소가 조건에 일치하는가를 판정한다.
	4. 배열의 내용을 특정의 조건으로 필터링 -filter 메소드-
	```
    array.filter(callback [, that])
    	array : 배열 객체
        callback : 개별 요소를 처리하기 위한 함수
        that : 함수 callback안에서 this가 나타내는 객체
    ```
    - data로 부터 홀수만 추추랗는 예
    ```javascript
    var data = [4, 9, 16, 25];
var result = data.filter(function(value,index,array){
		return value % 2 === 1;
});
console.log(result); // 결과 : [9, 25]
    ```

- 독자적인 규칙으로 배열을 나열하기 - sort 메소드
	- 디폴트로 배열을 문자열로 취급하여 사전순으로 정렬한다. 이 규칙을 변경하는데 인수로서 다음과 같은 함수를 정의한다.
		- 인수는 2가지(비교할 배열 요소)
		- 제1인수가 제2인수보다 작은 경우는 음수, 큰 경우는 양수를 반환한다.
		- 배열의 내용을 숫자로 정렬하는 예
		- ```javascript
		var ary = [5, 25, 10];
console.log(ary.sort()); // 결과 : [10, 25, 5]
console.log(ary.sort(function(x,y){
	return x - y;	
})); // 결과 : [5, 10, 25]
		```
        - 직급(부장→과장→주임→담당)의 순서로 객체 배열 members 정렬
        - ```javascript
        var classes = ['부장', '과장', '주임', '담당'];
var members = [
    { name: '남상미', clazz: '주임'},
    { name: '김준수', clazz: '부장'},
    { name: '정인식', clazz: '담당'},
    { name: '남궁민', clazz: '과장'},
    { name: '이상주', clazz: '담당'}
];
console.log(members.sort(function(x, y){
	return classes.indexOf(x.clazz) - classes.indexOf(y.clazz);
}));
        ```
        결과 : 
        ```
        [
        {name: "김준수", clazz: "부장"},
		{name: "남궁민", clazz: "과장"},
		{name: "남상미", clazz: "주임"},
		{name: "정인식", clazz: "담당"},
		{name: "이상주", clazz: "담당"}
        ]
        ```

### 3-3-2 연상 배열 조작하기 - Map객체 `ES2015`
> 키/값의 세트 - 이른바 연상 배열을 관리하기 위한 객체

- Map 객체의 기본
	- Map 객체의 주요 멤버
	|멤버|개요 |
	|--------|--------|
	|size|요소 수|
	|set(key, val)|키/값의 요소를 추가, 중복될 경우에는 덮어쓴다|
	|get(key)|지정한 키의 요소를 취득|
	|has(key)|지정한 키의 요소가 존재하는지 판정|
	|delete(key)|지정한 키의 요소를 삭제|
	|clear()|모든 요소를 삭제|
	|keys()|모든 키를 취득|
	|values()|모든 값을 취득|
	|forEach(fnc [, that])|맵 내의 요소를 함수 fnc로 순서대로 처리|
	```javascript
    let m = new Map();
m.set('dog', '멍멍멍');
m.set('cat', '야옹야옹');
m.set('mouse','찍찍');
//
console.log(m.size); // 결과 : 3
console.log(m.get('dog')); // 결과 : 멍멍멍
console.log(m.has('cat')); // 결과 : true
//
for(let key of m.keys()){
	console.log(key); // 결과 : dog, cat, mouse
}
```
    