# 인스턴스와 컴포넌트

# Instance

 `instance.html`

> 인스턴스 소개

- 인스턴스 생성

  ```javascript
  var vm = new Vue(); //vm means vue model
  console.log(vm);
  ```

  

> 인스턴스와 생성자 함수

```javascript
/* ex1 */
function Person(name, job) { //Start with uppercase
	this.name = name;
	this.job = job;
}
var p = new Person('Judy','developer')

/* ex2 */
//생성자 함수로 미리 함수나 API를 정의해서 재사용 가능
function Vue() {
	this.logText = function(){
		console.log('Hello');
	}
}
var vm = new Vue();
vm.logText(); 
// >Hello


```



> 인스턴스 옵션 속성

```javascript
new Vue({ //객체를 통째로 인자에 넣어주는 방식
    el: , //key:value
    template: ,
    data: ,
    methods: ,
    created: ,
    watch: ,
});
```





# Components

> 컴포넌트는 화면의 영역을 구분하여 개발할 수 있는 뷰의 기능

- 컴포넌트 기반으로 개발하게 되면 코드 재사용성이 올라가고 빠르게 화면을 제작할 수 있음





[실습안내] 컴포넌트 등록 및 실습

