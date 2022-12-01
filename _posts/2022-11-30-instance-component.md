# 인스턴스와 컴포넌트

`code 안에 있는 내용은 <script></script>를 생략한다.`

# Instance

 `instance.html`

> 인스턴스 소개

- 인스턴스 생성

  ```vue
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"> //cdn address
  </script>
  
  <script>
  var vm = new Vue(); //vm means vue model
  console.log(vm);
  </script>
  ```

  

> 인스턴스와 생성자 함수

```vue
<script>
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
</script>
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

 `component.html`

> 컴포넌트는 **화면의 영역을 구분하여 개발**할 수 있는 뷰의 기능

- 컴포넌트 기반으로 개발하게 되면 코드 **재사용성**이 올라가고 빠르게 화면을 제작할 수 있음

- 인스턴스를 생성하면 개발자 도구에서 **Root 컴포넌트로 인식**됨

- 헤더, 컨텐츠, 사이드 등

  - 영역을 구분했을 때 컴포넌트 간의 관계가 생긴다.



## 전역 컴포넌트

> 플러그인이나 라이브러리 형태로 등록할 때 사용
>
> - 인스턴트를 생성할 때마다 **기본적으로 컴포넌트가 등록되어있음**

```vue
<div id="app">
  <app-header></app-header>
</div>

<script>
    // 전역 컴포넌트 등록
    // Vue.component('컴포넌트 이름', 컴포넌트 내용);
    Vue.component('app-header', {
      template: '<h1>Header</h1>'
     });  

    new Vue({
        //el: 'div' // 태그값 할 수도 있긴 함
        el: '#app' //use css선택자'#'
    });
</script>
```

- 부모 컴포넌트 `root` 밑에 자식 컴포넌트 `<app-header>`

## 지역 컴포넌트

> root, 컴포넌트 간의 관계를 한눈에 볼 수 있음
>
> - **인스턴스 마다 컴포넌트를 새로 생성**해줘야 함 -> 인스턴스를 생성할 때 번거로울 수 있음

```vue
<div id="app">
    <app-footer></app-footer>
</div>
<script>
    // 전역 컴포넌트 Vue.component('컴포넌트 이름', 컴포넌트 내용);
    new Vue({
        el: '#app',
        components: {
            // 지역 컴포넌트 등록
            //'컴포넌트 이름': 컴포넌트 내용
   	        'app-footer': {
                template: '<footer>footer</footer>'
            }
        }
    });
</script>
```

- `components`, `methods` : 서비스를 구현할 때 필요한 조직이 한개가 아니기 때문에 s를 붙임

## 컴포넌트 통신방식

> 뷰 컴포넌트는 각각 고유한 유효 범위를 가기 때문에, 컴포넌트 간에 데이터를 주고 받기 위해선 규칙을 따라야 함
>
> → **데이터의 흐름과 버그를 추적할 수 있다. (N방향 통신)**


- **상위 → 하위:** 데이터를 내려줌, <u>*프롭스 속성*</u>
- **하위 → 상위:** 이벤트를 올려줌, <u>*이벤트 발생*</u>

### props 속성

`props.html`

> **Data binding 데이터 바인딩**
>
> *`<app-header v-bind:프롭스 속성 이름="상위 컴포넌트의 데이터 이름"></app-header>`*

```vue
<div id="app">
    <!-- <app-header v-bind:프롭스 속성 이름="상위 컴포넌트의 데이터 이름"></app-header> -->
    <app-header v-bind:propsdata="message"></app-header>
    <app-content v-bind:propsdata="num"></app-content>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    var appHeader = {
        //template: '<h1>header</h1>',
        template: '<h1>{{ propsdata }}</h1>', // root에서 내려보낸 message가 들어가게 됨
        props: ['propsdata'] //props 데이터 정의
    }
    var appContent = {
        template: '<div>{{ propsdata }}</div>',
        props: ['propsdata']
    }

    new Vue({
        el: '#app',
        components: {
            'app-header': appHeader,
            'app-content': appContent
        },
        data: {
            message: 'hi',
            num: 10	
        }
    })
</script>
```

> root에서 데이터가 바뀌면 하위 컴포넌트에 바로 반영됨 **→ reactivity**

### event 에밋


<img width="80%}" src="https://user-images.githubusercontent.com/110404800/205086234-700c16f7-b962-4a1e-b99c-8f8118f10342.jpg"/>

