# Vue.js



## 자바스크립트 프레임워크 (라이브러리)

자바스크립트를 더욱 손쉽고 편리하게 도와주는 도구

프로그레시브 프레임워크/라이브러리: 높은 자유도, 다양한 방식으로 구현 가능, 개발도 가능

SPA 방식: Single Page Application = 하나의 페이지가 모든 화면과 기능을 담고 있음 = 페이지를 한 번만 불러오면 됨



- React: 높은 자유도, 코드가 plain.js와 거의 흡사함, TypeScript 사용, 다양한 상태 관리툴, 뛰어난 컴포넌트
- Vue: Angular와 React의 장점만 골라 만듬, 비교적 쉬운 학습 난이도, 성능도 리액트와 비교하여 대등함, 국내에서도 높은 점유율, 꾸준한 업데이트와 방대한 커뮤니티
- Angular: 비교적 난이도가 높지만 안정적인 시스템, 엔터프라이즈급 규모의 프로젝트에 적합함, 리액트와 뷰만큼 대중적이진 않음



## 데이터 바인딩

```vue
<template>
	<div>
		<h1>Hello{{ username }}</h1>
		<h1 v-text="username"></h1>
		// v-text는 태그 안의 내용을 전부 바꾸기 때문에 태그가 비어있어야 함.
		<p>{{year}}</p>
		<p>{{user.name}}</p>
		<p v-html="button"></p>
		//v-html은 태그 자체를 html 코드 내에 삽입하기 때문에 신뢰할 수 있는 것만 넣어야 함 
  </div>
</template>
<script>
export default {
	name: "App",
	data() {
		return {
			username: 'scalper',	
			year : 2022,
			user: {
				name: "scalper".
				job: 'programmer',
				age: 34,
			},
			button: "<button>click!</button>"
		};
	},
};
```





## 스타일 바인딩

```vue
<template>
	<div>
    <h2 class="line-through">line-through</h2>
    <h2 v-bind:class="textDecoration" class="text-red">line-through</h2>
    <h2 :class="isDone === true ? 'line-through' : 'hightlight'">
      line-through
    </h2>
    <h2 :class="{hightlight: isDone === false, 'text-red': usernamer === 'scalper',}">
		line-through</h2>
			//오브젝트 형태로도 가능
		<h2 :class="[isDone === true ? 'line-through' : 'text-red', 'hightlight']">
		Array 형태의 동적 클래스 부여</h2>
  </div>
</template>
<script>
export default {
	name: "App",
	data() {
		return {
			isDone: false,
			username: 'scalper',
			textDecoration: "line-through",		
		};
	},
};
</script>
<style>
	.text-red {
		color: red;
	}
	.highlight {
		font-weight: bold;
		background: pink;
	}
	.line-through {
		text-decoration: line-through;
	}
</style>
```



## 클래스 바인딩

```vue
<template>
	<h1 id="title">Hello Title</h1>
	<h1 v-bind:style="titleStyle">Hello Title</h1>
	<h1 v-bind:style="[titleStyle, basicStyle]">Hello Title</h1>
	<h1 v-bind:id="dynamicId">Hello Title</h1>
	<a v-bind:href="url">naver</a>
	<img v-bind:src="image.src" v-bind:alt="image.alt">
	<input v-bind:type="inputType">
	<p v-bind:style="pStyle">Hello Vue!</p>
	<p v-bind:style="{color: 'red', 'font-size': '50px'}">Hello Vue!</p>
<p v-bind:style="{color: 'red', 'font-size': '$(basicSize)px'}">Hello Vue!</p>
</template>

<script>
export default {
	name: "App",
	data(){
		return {
			dynamicId: "content",
			url: "https://naver.com",
			image: {
				src: 'https://placeimg.com/100/100/any',
				alt: 'random image'
			},
			inputType: "text",
			pStyle: "color: red; font-size: 36px;",
			basicSize: 100,
			titleStyle: {
				'font-weight': 'bold',
				'font-size': '50px',
				border: '1px solid red'
			},
			basicStyle: {
				background: "yellow"
			},
		};
	},
};
</script>

<style>
#title {
	color: red;
	background: yellow;
}
#content {
	color: blue;
	background: pink;
}
</style>
```





## 조건부 렌더링

```vue
<template>
	<div>
		<h1>Hello{{ username }}</h1>
		<h1 v-once v-text="username"></h1>
		//내용변경이 일어나도 한 번만 적용됨
		<h1 v-text="username"></h1>
		<input type="text" v-model="user.name">
	  //입력받는 값을 value로 연결 form handling에서 사용
		<h2 v-if="showName === true">My name is {{ user.name }}</h2>
		//조건이 참일때만 문장이 출력됨
		//showName === true 의 경우 showName 만 써도 같은 의미임 거짓일땐 !showName
		<h2 v-else>이름을 보여줄 수 없습니다.</h2>
		<h2 v-if="user.age > 20">당신은 성인입니다.</h2>
		<h2 v-else-if="user.age > 14 && user.age < 20">당신은 청소년입니다.</h2>
		
		//조건이 거짓일 때 출력 됨
	</div>
</template>
<script>
export default {
	name: "App",
	data() {
		return {
			showName: true,
			user: {
				name: "scalper".
				job: 'programmer',
				age: 34,
			},
			button: "<button>click!</button>"
		};
	},
};
</script>
<style>
#title {
	color: red;
	background: yellow;
}
#content {
	color: blue;
	background: pink;
}
</style>
```



## 리스트 렌더링

```vue
<template>
<div>
	<ul>
		<li v-for="fruit in fruits" :key="fruit">
			{{fruit}}
		</li>
		<li v-for="(fruit, index) in fruits" :key="index">
			{{index}}{{fruit}}
		</li>
	</ul>
	<h2 v-for="(value, key) in user" :key="key">
		{{key}} :: {{value}}
	</h2>
	<p  v-for="n in 10" :key="n">
		{{n}}
	</p>
</div>
</template>

<script>
export default {
	name: "App",
	data() {
		return {
			fruits: ["banana", "strawberry", "apple", "melon"],
			user: {
				name: "scalper".
				job: 'programmer',
				age: 34,
			},
		};
	},
};
</script>
```



```vue
<template>
<div>
	<div v-for="(animal, animalIndex) in animals" :key="animalIndex">
		<h2>Animal ===> {{animal.name}}</h2>
		<h3>food</h3>
		<ul>
			<li v-for="(food, foodIndex) in animal.favorites" :key="foodIndex">
				{{food}}
			</li>
		<ul>
	</div>
</div>
</template>

<script>
export default {
	name: "App",
	data() {
		return {
			animals: {
				{name: 'rabbit', size: 'small', favorites: ['glass', 'carrot']},
				{name: 'lion', size: 'big', favorites: ['deer', 'caw']},
				{name: 'owl', size: 'medium', favorites: ['rat', 'fruits']}
			}
		};
	},
};
</script>
```





## 조건부 리스트 렌더링

```vue
<template>
<div>
	<ul>
		<li v-for="(city, index) in cities.filter((c) => {return c.province === '경상도'})" :key="index">
		{{city.name}}
		</li>
	</ul>
	//원초적인 방법...필서사용
	<ul>
		<template v-for="(city, index) in cities" :key="index">
			<li v-if="city.province === '경상도'">
				{{city.name}}
			</li>	
		</template>
	</ul>
	//더 나은 방법 - 템플릿사용
</div>
</template>

<script>
export default {
	name: "App",
	data() {
		return {
			cities: [
				{name: '서울', province: '경기도' },
				{name: '대전', province: '충청도' },
				{name: '대구', province: '경상도' },
				{name: '부산', province: '경상도' },
				{name: '인천', province: '경기도' },
				{name: '광주', province: '전라도' },
			]
		};
	},
};
</script>
```





## 메서드

Method: Object Associated Function

```vue
<template>
	<div>
		<h2> 5년 뒤 :: {{add(5)}} </h2>
		<h2> 10년 뒤 :: {{add(10)}} </h2>
		<h2> 15년 뒤 :: {{add(15)}} </h2>
		<h2> 20년 뒤 :: {{add(20)}} </h2>
		<h2>동갑의 10명이 있다면 나이의 총 합은 {{multiply(age, 10)}} </h2>
		<h2> {{getTotalScore(100)}} </h2>
	</div>
</template>

<script>
export default {
	name: "App",
	data() {
		return {
			age: 34,
		};
	},
	methods: {
		add(num){
			return this.age + num;
		},
		add:(num)=>{
			return this.age + num;
		},
		//화살표 함수를 사용하면 age가 잡히지 않음
		multiply(num1, num2 = 10){
			//num2에 저장된 10은 숫자를 한 개만 받을 경우에 적용됨 
			//인자가 2개가 충족될 경우엔 받은 인자가 함수에 적용
			return num1 * num2;
		},
		getTotalScore(num){
			return this.multiply(num, num);
		},
	},
};
</script>
```

lexical scope: 함수의 선언에 따라 스코프가 결정 (즉, 호출에 영향을 받지 않고 고정된다는 의미) 화살표 함수의 경우가 이러함





## 이벤트 핸들링

```vue
<template>
	<div>
		<h2> Hello {{name}} ! </h2>
		<button v-on:click="changeName"> change name </button>
		<button v-on:mouseover="name = 'Alexa'" v-on:mouseleace="name = 'Scalper'">
		 change name </button>
		<button v-on:click.right="changeName"> change name </button>
		//. modifier 속성

		<a v-on:click="movePage" href="http://naver.com">네이버로 이동</a>
		<a v-on:click.prevent="movePage" href="http://naver.com">네이버로 이동</a>
	
		<h2> {{number}} </h2>
		<button v-on:click="incremnet($event, 1)"> 숫자 1 증가 </button>
		<button v-on:click="decremnet(1)"> 숫자 1 감소 </button>
		<button v-on:click="incremnet(5)"> 숫자 5 증가 </button>
		<button v-on:click="decremnet(5)"> 숫자 5 감소</button>

	</div>
</template>

<script>
export default {
	name: "App",
	data() {
		return {
			name: 'Scalper',
			nummer: 0,

		};
	},
	methods: {
		changeName(){
			this.name = 'Alexa'
		},
		movePage(e){
			e.preventDefault();
			const check = confirm("페이지를 이동하시겠습니까?");
			if(check){
				console.log("페이지 이동");
			}
			else{
				console.log("페이지 이동 안함");
			}
		},
		increment(e, num){
			this.number += num;
		},
		decrement(num){
			this.number -= num;
		},
	},
};
</script>
```





## Form 핸들링

```vue
<template>
<div>
	<form>
		<div>
			<label for="name">이름</label>
			<input type="text" id="name" v-model="user.name" @input="setValue">
			//@ = v-on:
		</div>
		<div>
			<label for="age">나이</label>
			<input type="number" id="age" v-model="user.age" />
		</div>
		<div>
			<label for="city">사는 곳</label>
			<select id="city" v-model="user.city">
				<option value="seoul">서울</option>
				<option value="daejeon">대전</option>
				<option value="daegu">대구</option>
				<option value="busan">부산</option>
				<option value="gwangju">광주</option>
			</select>
		</div>
		<div>
			<label for="favorite-food">좋아하는 음식</label>
			<select id="favorite-food" v-model="user.favorite">
				<option v-for="option in foodOptions" multiple :value="option.code" :key="option.code">
					{{option.label}}
				</option>
			</select>
		</div>
		<div>
			<label for="job">직업</label>
			프로그래머<input type="checkbox" id="job" value="programmer" v-model="user.jop">
			교사<input type="checkbox" id="job" value="teacher" v-model="user.jop">
			PD<input type="checkbox" id="job" value="producer" v-model="user.jop">
		</div>
		<div>
			<label for="gender">성별</label>
			여<input type="radio" id="gender" value="female" v-model="user.gender">
			남<input type="radio" id="gender" value="male" v-model="user.gender">
		</div>
	</form>
</div>
</template>

<script>
export default {
	name: "App",
	data() {
		return {
			foodOptions:[
				{label: '짜장면', code: 'JJ'},
				{label: '짬뽕', code: 'JB'},
				{label: '탕수육', code: 'TSY'},
			],
			user: {
				name: '',
				age: 0,
				city: 'seoul',
				favorite: [],
				job: [],	
			},
		};
	},
	methods: {
		setValue(e){
			this.user.name = e.target.value;
			//한글 등으로 이름을 입력할 경우 글자수가 밀리는 것을 방지하는 메소드
		}
	},
};
</script>
```





## Directives

```vue
<template>
	<div>
		<h2 v-once> 유저의 이름은 {{ userName }} </h2>
		//v-onse 이벤트는 실행이 되지만 이름은 변경되지 않음
		<button @click="changeName"> change name </button>
		<h2 v-pre> {{ userName }} </h2>
		// v-pre : 컴파일에서 제외되기 때문에 데이터에 저장된 이름이아닌 {{}} 가 그대로 출력됨
		<input v-focus type="text" />
		highlight<input v-highlight type="text" />
  </div>
</template>
<script>
export default {
	name: "App",
	data() {
		return {
			userName: 'scalper',
		};
	},
	directives: {
		focus: {
			mounted(el){
				el.focus();
			},
		},
		hightlight: {
			mounted(el){
				el.oninput = () => {
					el.style.background = "blue";
					el.style.color = "#fff";
				};
			},
		},
	},
	methods: {
		changeName(){
			this.userName = "code";
		}
	},
};
</script>
```





## Computed

계산된 값을 제공해주는 기능

```vue
<template>
<div>
	<div>
		<h2> {{ address1 }} {{ address2 }} {{ address3 }}</h2>
		<h2> {{ address}}</h2>
		<h3>내가 받은 점수의 합은 {{ grade.math + grade.kor + grade.eng + grade.sci}} </h3>
		<h3>내가 받은 점수의 합은 {{ totalScore }} </h3>
		//method로도 같은 식이 실행 가능하지만 method는 값에 변화가 없어도 계속 실행되기 때문에 computed를 사용하는 것이 좋음
</div>
</template>

<script>
export default {
	name: "App",
	data() {
		return {
			address1: "성남시",
			address2: "분당구",
			address3: "정자로",
			grade: {
				math: 70,
				kor: 90.
				eng: 50,
				sci: 55,
			},
		};
	},
	computed: {
		address(){
			return `$(this.address1)$(this.address2)$(this.address3)`
		},
		totalScore(){
			const {math, kor, eng, sci} = this.grade;
			return math + kor + eng + sci;
		},
	},
};
</script>
```





## Watch

데이터의 어떤 값들이 변경되는지 감시, 인지하는 것

```vue
<template>
<div>
	<div>
		<h2> current money :: {{ money }} </h2>
		<div>
			<button @click = "money += 100"> earn money </button>
			<butto n@click = "money -= 100"> spend money</button>
		</div>
		<h2> {{receit}} </h2>
		<butto n@click = "receit.food += 500"> buy food</button>
		<input type="text" v-model="userName" />
</div>
</template>

<script>
export default {
	name: "App",
	data() {
		return {
			userName: "scalper",
			money: 0,
			receit: {
				food: 3000,
				fee: 2000,
				fare: 10000,
			}
		};
	},
	computed: {
	},
	watch: {
		userName: {
			handler(newValue){
				console.log(newValue,"newValue");
			},
			immediate: true,
		},
		receit(newValue, oldValue){
			console.log("영수증에 값 변화가 있음",newValue, oldValue);
		},//이렇게 하면 오브젝트 안의 값이 잡히지 않아서 출력 안됨//
		receit: {
			handler(newValue){
				console.log("영수증에 값 변화가 있음",newValue)
			},
			deep: true,
		},
		money(newValue, oldValue) {
			console.log(oldValue);
			if (newValue > 2000 && newValue > oldValue){
				console.log("mission copmlete!");	
			}
			if (oldValue < 1500 && newValue < oldValue){
				console.log("save moeny!");
			}
		},
	},
};
</script>
```





## Component

파일을 파트별로 나누어서 재사용하기 편하게 사용하는 것

파일명은 카멜형으로 쓰는것이 좋음

컴포넌트에서 데이터를 변경하는 것은 안됨. 즉, prop으로 넘겨받은 값은 수정할 수 없음.

단, prop의 property는 수정 가능함

```vue
<template>
<div>
	<GreetingUser :username="username" :numberofVisit="numberofVisit" />
	<GreetingUser username="wendy" />
	<GreetingUser :siteInfo="siteInfo"/>
	<button @click="changeName()"> change </button>
</div>
</template>

<script>
import GreetingUser from "./components/GreetingUser";
export default {
	name: "App",
	components: {
		GreetingUser: GreetingUser
	},
	data() {
		return {
			username: "scalper",
			numberofVisit: 25,
			siteInfo: {
				name: "vue practice"
				teacher: "scalper",
				subject: "frontend",
			},
		};
	},
	computed: {
	},
	watch: {
	},
	methods: {
		changeName() {
			this.username = "denny"
		},
	},
};
</script>
```



GreetingUser component


```vue
<template>
<div>
	<h2>Hello {{username}}! </h2>
	<h3>오늘이 {{numberofVisit}} 번째 방문입니다. </h3>
	<h3> 사이트 이름은 {{siteInfo.name}} 입니다. </h3>
</div>
</template>
<script>
export default {
	name: "Greeting User",
	props: {
		//username: String,
		username: {
			type: String,
			default: "user",
			//가급적 기본값을 주는 것이 좋음
		},
		numberofVisit: 
			type: Numner,
			default: 0,
		},
		siteInfo: {
			type: Object,
			default: ()=>{
				return { name: "-", teacher="-", subject="-"}
			}
			//오브젝트나 배열의 경우 함수의 형태로 지정
		},
	},
};
</script>
<style scoped>
//scoped를 넣어서 이 파일에만 해당 스타일이 적용되도록 함
</style>
```



---

```vue
<template>
<div>
	//<ul>
		//<li v-for="product in products" :key="product.id"></li>
	//</ul>

	<ProductList :products="products" />

</div>
</template>

<script>
import ProductList form "./components/ProductList"
export default {
	name: "App",
	components: {
		ProductList,
	},
	data() {
		return {
			products: [
				{ id: 0, name: 'TV', price: 500000, company: "LG"}.
				{ id: 1, name: '전자렌지', price: 200000, company: "삼성"}.
				{ id: 2, name: '오븐', price: 700000, company: "드롱기"}.
				{ id: 3, name: '냉장고', price: 1500000, company: "대우"}.
				{ id: 4, name: '에어컨', price: 900000, company: "대일"}.
			],
		};
	},
	computed: {
	},
	watch: {
	},
	methods: {
		
	},
};
</script>
```



ProductList component

```vue
<template>
<div>
	<ul>
			<ProductItem v-for="product in products" :key="product.id" :product="product" />
	</ul>
</div>
</template>
<script>
import ProductItem from "./ProductItem"
export default {
	name: "product-list",
	props: {
		products: {
			type: Array,
			default() {
				return [];
			},
		},
	},
};
</script>
<style scoped>
//scoped를 넣어서 이 파일에만 해당 스타일이 적용되도록 함
</style>
```



ProductItem - component

```vue
<template>
<div>
	<li>
		<p class="title">{{product.name}}</p>
		<p class="image">
			<img :src="`http://placeimg.com/200/100/$(product.id)`" :alt="product.name">
		</p>
		<p class="price">{{product.price}}</p>
	</li>
</div>
</template>
<script>
export default {
	name: "product-item",
	props: {
		product: Object,
	},
};
</script>
<style scoped>
//scoped를 넣어서 이 파일에만 해당 스타일이 적용되도록 함
	li {
		border: 2px solid blue;
		margin-bottom: 0.5rem;
	}
	.title{
		font-size: 24px;
		color: blue;
		font-weight: bold;
	}
</style>
```



`v-bind=”$attrs”` 를 통해서 컴포넌트파일을 감싸는 div 태그에 id 등을 부여할 수 있음

div태그에 id 등을 상속시키지 않고 특정 태그에 상속을 원할 경우에는 `inheritAttrs: false` 를 넣어서 해결 가능함



### 이벤트 전달

```vue
<template>
<div>
	<h2>Hello Component</h2>
	<button @click="displayDetail=true"> show detail </button>
	<DetailView v-if="displayDetail" @closeDetail="close" @sendData="showData"/>
</div>
</template>

<script>
import DetailView form "./components/DetailView "
export default {
	name: "App",
	components: {
		DetailView,
	},
	data() {
		return {
			displayDetail: false,
			
		};
	},
	computed: {
	},
	watch: {
	},
	methods: {
		close(){
			this.displayDetail = false;
		},
		showData(data){
			console.log(data, "data sent!")
		},
	},
};
</script>
```



Detail View component

```vue
<template>
<div class="wrapper">
	<div class="container">
		<h2> Detail Page </h2>
		<button @click="closeDetail"> close </button>
		<input type="text" v-model="username">
		<button @click="sendData"> send Data </button>
	</div>	
</div>
</template>
<script>
export default {
	name: "detailPage",
	data(){
		return {
			username: ""
		}
	},
	methods: {
		closeDetail(){
			this.$emit("closeDetail");
		},
		sendData(){
			this.$emit("sendData, this.username");
		},
	},
};
</script>
<style scoped>
	.wrapper{
		background: rgba(0,0,0,0.5);
		position: fixed;
		width: 100%; 
		height: 100%;
		top: 0;
		left: 0;
		diplay: flex;
		justify-content: center;
		align-items: center;
	}
	.container{
		background: #fff;
		width: 60%;
	}
</style>
```





### provide - inject

```vue
<template>
<div>
	<h2>Hello Component</h2>
	<CompLevel1 />
</div>
</template>

<script>
import CompLevel1 form "./components/provide-inject/CompLevel1 "
export default {
	name: "App",
	components: {
		CompLevel1, 
	},
	data() {
		return {
			username: "scalper",
		};
	},
	provide(){
		return {
			name: this.username,
		}
	},
	computed: {
	},
	watch: {
	},
	methods: {
		
	},
};
</script>
```



CompLevel1 component

```vue
<template>
	<h2> component 1 </h2>
	<CompLevel2 />
</template>
<script>
import CompLevel2 from './CompLevel2'
export default {
	name: "comp1",
	components: {
			CompLevel2
	}
};
</script>
<style scoped>
</style>
```



CompLevel2 component

```vue
<template>
	<h2> component 2 </h2>
	<CompLevel3 />
</template>
<script>
import CompLevel3 from './CompLevel3'
export default {
	name: "comp1",
	components: {
			CompLevel3
	}
};
</script>
<style scoped>
</style>
```



CompLevel3 component

```vue
<template>
	<h2> component 3 </h2>
	<h3>passed Data from App = {{ name }} </h3>
</template>
<script>
export default {
	name: "comp3",
	inject: ["name"],
};
</script>
<style scoped>
</style>
```





### dynamic component

```vue
<template>
<div>
	<h2>Hello Component</h2>
	<button @click="activeTap = 'Menu1'">Menu1</button>
	<button @click="activeTap = 'Menu2'">Menu2</button>
	<button @click="activeTap = 'Menu3'">Menu3</button>
	<keep-alive>
		<componet :is="activeTap"></componet>
	</keep-alive>
	//input태그에 작성한 내용을 버튼을 눌러 이동해도 남아있게 함
</div>
</template>

<script>
import Menu1 from "./components/tabItems/Menu1";
import Menu2 from "./components/tabItems/Menu2";
import Menu3 from "./components/tabItems/Menu3";
export default {
	name: "App",
	components: {	},
	data() {
		return {
			username: "scalper",
			activeTap: "Menu1",
		};
	},
	computed: {
	},
	watch: {
	},
	methods: {
		
	},
};
</script>
```



menu1 component

```vue
<template>
	<h2> Menu 1 </h2>
	
</template>
<script>
export default {
};
</script>
<style scoped>
</style>
```



menu2 component

```vue
<template>
	<h2> Menu 2 </h2>
	
</template>
<script>
export default {
};
</script>
<style scoped>
</style>
```



menu3 component

```vue
<template>
	<h2> Menu 3 </h2>
	<input type="text" v-model="username" />
</template>
<script>
export default {
	data() {
		return {
			username: "",
		}
	},
};
</script>
<style scoped>
</style>
```





## 슬롯

```vue
<template>
<div>
	<CardView>
		Hello Slot!
  </CardView>
	<CardView>
		<img src="https://placeimg.com/100/50/any" alt="random" />
  </CardView>
	<CardView>
		<ul>
			<li> item 1 </li>
			<li> item 2 </li>
		</ul>
  </CardView>
	<CardView>
		//비어있는 경우에는 기본값 출력
  </CardView>
	<CardView>
		<template v-slot:header>
			<h3> Random Image </h3>
		</template>
		<template v-slot:body>
			<img src="https://placeimg.com/100/50/any" alt="random" />
		</template>
		<template v-slot:footer>
			<small> thank you </small>
		</template>
  </CardView>
</div>
</template>

<script>
import CardView from "./components/slot/CardView";
export default {
	name: "App",
	components: {
		CardView,
	},
	data() {
		return {
			
		};
	},
	computed: {
	},
	watch: {
	},
	methods: {
		
	},
};
</script>
```



CardView component

```vue
<template>
	<div class="card">
		<slot> Default Value </slot>
		<div class="card-header"> <slot name="header"></slot> </div>
		<div class="card-body"> <slot name="body"></slot> </div>
		<div class="card-footer"> <slot name="footer"></slot> </div>
	</div>
</template>
<script>
export default {
};
</script>
<style scoped>
	.card{
	box-shadow: 0 4px 8px 0 rgba(0,0,0,0.3);
	padding: 1rem;
	margin-bottom: 1rem;
	width: 200px;
	}
</style>
```





## teleport

뷰 파일에 작성된 내용은 index 파일 안 #app 에들어가게 되는데 (메인에서 그렇게 되도록 설정함)

teleport를 사용하면 #app 외 원하는 태그로 요소를 이동시킬 수 있음

```vue
<template>
<div>
	<h2>Hello Teleport</h2>
	<teleport to="#extra-modal" :disabled="isTeleport">
		<div class="modal">
			This is Modal
			<button @click="isTeleport = !isTeleport">teleport toggle </button>
		</div>
	</teleport>
</div>
<div class="modal2">
	this is modal2
</div>
</template>

<script>
export default {
	name: "App",
	components: {
	},
	data() {
		return {
			isTeleport: true,
		};
	},
	computed: {
	},
	watch: {
	},
	methods: {
		
	},
};
</script>

<style scoped>
	position: fixed;
	background: rgba(0,0,0,0.5);
	coloer: #fff;
	width: 100%;
	height: 100%;
	top: 0;
	left: 0;
	font-size: 36px;
	display: flex;
	justify-content: center;
	align-items: center;
</style>
```





## http Request

axios 라이브러리 사용 `npm intall axios --save`

```vue
<template>
<div>
	<h2>Hello HTTP Request</h2>	
	<TodoList />
</div>
</template>

<script>
import TodoList from 'components/http/TodoList'
export default {
	name: "App",
	components: {
	},
	data() {
		return {
			
		};
	},
	computed: {
	},
	watch: {
	},
	methods: {
		
	},
};
</script>

<style scoped>

</style>
```



TodoList component

```vue
<template>
	<h2>Todo List </h2>
	<button @click="getTodoList"> Request Todo </button>
	<ul>
		<li v-for="todo in todoList" :key="todo.id"> {{todo.title}} </li>
	</ul>
	<div>
		<label for="todo">할일</label>
		<input type="text" v-model="todoItem.title">
		<button @click="createTodo">create</button>
	</div>
	<p v-if="errorMessage"> {{ errorMessage }} </p>
</template>
<script>
import axios from 'axios'
export default {
		name: 'todoList',
		data(){
			return {
				todoItem:{
					title: '',
					completed: false,
				},
				todoList: [],
				errorMessage: "",
			};
		},
		methods: {
			getTodoList(){
				const url = "jsonplaceholder.typicode.com/todos";
				axios.get(url).then((response) => this.todoList = response.data)
				.catch((e) => {console.log(e) 
				this.errorMessage="에러가 발생했음!"});
			},
			createTodo(){
				const url = "jsonplaceholder.typicode.com/todos";
				axios.post(url, this.todoItem).then(res => console.log(res))
				.catch((e) => console.log(e));
			},
		},
};
</script>
<style scoped>
	
</style>
```





## Life cycle

컴포넌트를 사용할 때 불러오는 순간이나 값을 불러오는 순간, 컴포넌트를 제거하는 순간 등을 가져와서 그 시점에 이벤트를 넣을 수 있도록 함.

Creating: beforeCreate(), created()

Mounting: beforeMount(), mounted()

Updating: beforeUpdate(), updated()

Unmounting: beforeUnmount(), unmounted()

주로 사용하는 4가지 (이 외에는 뷰 사이트 내 Lifecycle Hooks 참조)

misc: activated(), deactivated(), errorCaptured(), renderTracked(), renderTriggered()

```vue
<template>
<div>
	<h2>Hello HTTP Request</h2>	
	<TodoList />
</div>
</template>

<script>
import ParentComp from 'components/lifecycle/ParentComp'
export default {
	name: "App",
	components: {
	},
	data() {
		return {
			
		};
	},
	computed: {
	},
	watch: {
	},
	methods: {
		
	},
};
</script>

<style scoped>

</style>
```



ParentComp component

```vue
<template>
	<h2>Parent Component</h2>
	<ChildComp v-if="showChild"/>
	<button @click="showChild = false">unmount child</button>
</template>
<script>
import ChildComp from "./ChildComp"
export default {
		name: "perentComp",
		data(){
			return {
				showChild: true,
			};
		},
		components: {
			ChildComp,
		},
		beforeCrete(){
			console.log('parent before create')
		},
		created(){
			console.log('parent created')
		},
};
</script>
<style scoped>
</style>
```



ChildComp component

```vue
<template>
	<h2> Child Component </h2>
	<input type="text" v-model="username" />
</template>
<script>
export default {
		name: "childComp",
		data(){
			return {
				username: "",
			};
		},
		beforeCrete(){
			console.log('parent before create')
		},
		created(){
			console.log('parent created')
		},
};
</script>
<style scoped>
</style>
```





## refs

뷰에서 어떤 엘레먼트를 직접적으로 선택할 수 있게 해주는 것.

refs를 사용해서 부모에서 자식 컴포넌트안에 있는 메소드 등에 접근할 수 있음.

```vue
<template>
<div>
	<h2>Hello HTTP Request</h2>	
	<TodoList />
</div>
</template>

<script>
import ParentComp from 'components/lifecycle/ParentComp'
export default {
	name: "App",
	components: {
	},
	data() {
		return {
			
		};
	},
	computed: {
	},
	watch: {
	},
	methods: {
		
	},
};
</script>

<style scoped>

</style>
```



ParentComp component

```vue
<template>
	<h2>Parent Component</h2>
	<input v-model="nickname" ref="inputRef" />
	<button @click="consoleRef">console ref</button>
	<hr />
	<ChildComp v-if="showChild" ref="childComp"/>
	<button @click="showChild = false">unmount child</button>
</template>
<script>
import ChildComp from "./ChildComp"
export default {
		name: "perentComp",
		data(){
			return {
				nickname: "",
				showChild: true,
			};
		},
		methods: {
			consoleRef(){
				this.$refs.inputRef.focus();
				this.$refs.inputRef.style.border = "2px solid red";
				console.log(this$refs.inputRef, 'input ref');
				console.log(this$refs.childComp, 'child ref');
				this.$refs.childComp.sayHello();
			},
		},
		components: {
			ChildComp,
		},
		beforeCrete(){
			console.log('parent before create')
		},
		created(){
			console.log('parent created')
		},
};
</script>
<style scoped>
</style>
```



ChildComp component

```vue
<template>
	<h2> Child Component </h2>
	<input type="text" v-model="username" />
</template>
<script>
export default {
		name: "childComp",
		data(){
			return {
				username: "",
			};
		},
		methods: {
			sayHello(){
				console.log("say hello");
			},
		},
		beforeCrete(){
			console.log('parent before create')
		},
		created(){
			console.log('parent created')
		},
};
</script>
<style scoped>
</style>
```





## mixins

뷰의 다양한 기능들을 재사용할 수 있도록 도와줌

js파일로 생성하며 최대한 간결하고 복잡하지 않게 사용하는 것이 좋음

```vue
<template>
<div>
	<h2>Hello Mixins </h2>	
	<ProductStatus />	
	<FeeStatus />	
	<SavingStatus />
</div>
</template>

<script>
import ProductStatus from 'components/mixin/ProductStatus'
import FeeStatus from './FeeStatus'
import SavingStatus from './SavingStatus'
export default {
	name: "App",
	components: {
		ProductStatus, FeeStatus, SavingStatus
	},
	data() {
		return {
			
		};
	},
	computed: {
	},
	watch: {
	},
	methods: {
		
	},
};
</script>

<style scoped>

</style>
```



ProductStatus component

```vue
<template>
	<div>
		<h2> 전체 금액: {{totalMoney}} </h2>
	</div>
	<div>
		<button @click="addMoney(100)"> 100 </button>
		<button @click="addMoney(200)"> 200 </button>
		<button @click="addMoney(300)"> 300 </button>
		<button @click="addMoney(400)"> 400 </button>
	</div>
</template>
<script>
export default {
		name: "productStatus",
		data(){
			return {
				totalMoney: 0,
			};
		},
		methods:{
			addMoney(price){
				this.totalMoney += price;
			},
		},
};
</script>
<style scoped>
</style>
```



FeeStatus component

```vue
<template>
	<div>
			<h2> 합산된 요금: {{ totalMoney }} </h2>
		<button @click="addMoney(50)"> 50 </button>
		<button @click="addMoney(100)"> 100 </button>
		<button @click="addMoney(150)"> 150 </button>
		<button @click="addMoney(200)"> 200 </button>
	</div>
</template>
<script>
import moneyMixin from '../../mixins/moneyMixins.js'
export default {
		name: "feeStatus",
		mixins: [moneyMixin],
		data(){
			return {
				
			};
		},
		methods:{
			
		},
};
</script>
<style scoped>
</style>
```



SavingStatus component

```vue
<template>
	<div>
			<h2> 합산된 총 적금: {{ totalMoney }} </h2>
		<button @click="addMoney(1000)"> 1000 </button>
		<button @click="addMoney(2000)"> 2000 </button>
		<button @click="addMoney(1500)"> 1500 </button>
		<button @click="addMoney(2200)"> 2200 </button>
	</div>
</template>
<script>
import moneyMixin from '../../mixins/moneyMixins.js'
export default {
		name: "savingStatus",
		mixins: [moneyMixin],
		data(){
			return {
				
			};
		},
		methods:{
		},
};
</script>
<style scoped>
</style>
```



moneyMixin js

```javascript
export default{
	data(){
			return {
				totalMoney: 0,
			};
		},
	mounted(){
		console.log("component using mixin mounted")
	},
	methods:{
		addMoney(price){
				this.totalMoney += price;
		},
	},	
};
```





## Composition

재사용가능한 코드들을 추출해서 사용할 수 있게 해줌.

### data

```vue
<template>
<div>
	<h2>Hello compotision API </h2>	
	<TestComponent />	
</div>
</template>

<script>
import TestComponent from './components/composition/TestComponent'
export default {
	name: "App",
	components: {
		TestComponent
	},
	data() {
		return {
		};
	},
	computed: {
	},
	watch: {
	},
	methods: {
		
	},
};
</script>

<style scoped>

</style>
```



TestComponent component

```vue
<template>
	<div>
		<h2> {{ username }} </h2>
	</div>
</template>
<script>
import {reactive } from 'vue'
export default {
		name: "TestComponent",
		setup(){
			const state = reactive({
				username: 'Scalper',
				age: 50,
			});

			return
				toRefs(state);
		},
		
		//data(){
			//return {
				//username: "Scalper",
			//};
		//},
		methods:{
		},
};
</script>
<style scoped>
</style>
```

TestComponent component v.2

```vue
<template>
	<div>
		<h2> {{ isNotUgly }} </h2>
	</div>
</template>
<script>
import {ref } from 'vue'
export default {
		name: "TestComponent",
		setup(){
			let isHandsome = ref(false);
			let isNotUgly = isHandsome;
			isHandsome.value = true;

			return
				isNotUgly
		},
		methods:{
		},
};
</script>
<style scoped>
</style>
```





### method, model

```vue
<template>
<div>
	<h2>Hello compotision API </h2>	
	<TestComponent />	
</div>
</template>

<script>
import TestComponent from './components/composition/TestComponent'
export default {
	name: "App",
	components: {
		TestComponent
	},
	data() {
		return {
		};
	},
	computed: {
	},
	watch: {
	},
	methods: {
		
	},
};
</script>

<style scoped>

</style>
```



TestComponent component

```vue
<template>
	<div>
		<h2> {{ username }} </h2>
		<button @click="changeName">ChangeUserName</button>

		<h2>제품명: {{ name }}, 가격: {{price}} </h2>
		<button @click="changeProduct">Change Product</button>
	<div>
		<input type="text" v-model="username" />
		//ref로 연결되어서 인풋창에 작성한 내용에 따라 username값도 변경됨
	</div>	

</div>
	
</template>
<script>
import { ref, reactive, toRefs } from 'vue'
export default {
		name: "TestComponent",
		setup(){
			const username = ref("scalper");
			const state = reactive({
					name: 'TV', price: 100
			})

			function changeName(){
				username.value = "Messi"
			}

			function changeProduct(){
				state.name = "세탁기"
				state.price = 500
			}
			return {
				username,
				changeName,
				changeProduct,
				...toRefs(state)
			};
		},
};
</script>
<style scoped>
</style>
```



### watch

```vue
<template>
<div>
	<h2>Hello compotision API </h2>	
	<TestComponent />	
</div>
</template>

<script>
import TestComponent from './components/composition/TestComponent'
export default {
	name: "App",
	components: {
		TestComponent
	},
	data() {
		return {
		};
	},
	computed: {
	},
	watch: {
	},
	methods: {
		
	},
};
</script>

<style scoped>

</style>
```



TestComponent component

```vue
<template>
	<div>
		<h2> {{ username }} </h2>
	<hr>
	<div>
		price <input type="number" v-model="price" />
		amout <input type="number" v-model="amount" />
		<h3> Total Price :: {{totalPrice}} </h3>
	</div>	

	<hr>
	<div>
		first <input type="text" v-model="first" />
		last <input type="text" v-model="last" />
		<h3> Full name :: {{fullName}} </h3>
	</div>
</div>
	
</template>
<script>
import { ref, reactive, computed, toRefs, watch } from 'vue'
export default {
		name: "TestComponent",
		setup(){
			const username = ref("scalper");
			const price = ref(5000);
			const amount = ref(1)

			const totalPrice = computed(()=>{
					return priece.value * amount.value ;
			});
			watch(price, (newValue, oldValue)=>{
				console.log(newValue, oldValue);
			})
			
			const state = reactive({
				first: 'code',
				last: 'scalper',
				home: {
					city: 'Seoul',
					type: 'Apartment'
				}
			});
			const fullName = computed(function(){
				return `${state.first} ${state.last}`
			});
			watch(
				() => {
					return state.first;
				},
				(newValue, oldValue)=>{
				console.log(newValue, oldValue);
			});

			watch(
				() => {
					return { ...state.home };
				},
				(newValue, oldValue) => {
					console.log(newValue, oldValue);
				},
				{deep: true}
			);

			return {
				username,
				price,
				amount,
				totalPrice,
				...toRefs(state),
				fullName,
			};
		},
//		data() {
//			return {
//				price: 5000,
//				amount: 1,	
//			};
//		},
//		computed: {
//			totalPrice(){
//				return this.price * this.amount;
//			},
//		},
};
</script>
<style scoped>
</style>
```



## lifecycle

```vue
<template>
<div>
	<h2>Hello compotision API </h2>	
	<TestComponent />	
</div>
</template>

<script>
import TestComponent from './components/composition/TestComponent'
export default {
	name: "App",
	components: {
		TestComponent
	},
	data() {
		return {
		};
	},
	computed: {
	},
	watch: {
	},
	methods: {
		
	},
};
</script>

<style scoped>

</style>
```



TestComponent component

```vue
<template>
	<div>
		<h2> Hello Life Cycle </h2>
		<ChildComponent firstname="code" lastname="scalper" @sendParent="sendParent" />
</div>
	
</template>
<script>
import ChildComponent from './ChildComponent'
import { } from 'vue'
export default {
		name: "TestComponent",
		components: { ChildComponent },
		methods: {
			sendParent(){
				console.log("parent event")
			}
		},
};
</script>
<style scoped>
</style>
```



ChildComponent component

```vue
<template>
	<div>
		<hr>
		<h3> {{ fullname }} </h3>
		<button @click="sendParent">click child</button>
</div>
	
</template>
<script>
import { computed } from "vue"
export default {
		name: "ChildComponent",
		props: ['firstname', 'lastname'],
		setup(props, context) {
			const fullname = computed(()=>{
				return `${props.firstname} ${props.lastname}`;
			});
			function sendParent(){
				context.emit("sendParent")
			}
			
			return {
				fullname,
				sendParent,
			},
		},

//		computed: {
//			fullname(){
//				return `${this.firstname} ${this.lastname}`
//			}	
//		}
};
</script>
<style scoped>
</style>
```



### reusability

```vue
<template>
<div>
	<h2>Hello Reusability </h2>	
	<ProductStatus />	
	<FeeStatus />	
	<SavingStatus />
</div>
</template>

<script>
import ProductStatus from 'components/mixin/ProductStatus'
import FeeStatus from './FeeStatus'
import SavingStatus from './SavingStatus'
export default {
	name: "App",
	components: {
		ProductStatus, FeeStatus, SavingStatus
	},
	data() {
		return {
			
		};
	},
	computed: {
	},
	watch: {
	},
	methods: {
		
	},
};
</script>

<style scoped>

</style>
```



ProductStatus component

```vue
<template>
	<div>
		<h2> 전체 금액: {{totalMoney}} </h2>
	</div>
	<div>
		<button @click="addMoney(100)"> 100 </button>
		<button @click="addMoney(200)"> 200 </button>
		<button @click="addMoney(300)"> 300 </button>
		<button @click="addMoney(400)"> 400 </button>
	</div>
</template>
<script>
import useMoney from '../../composables/useMoney'
export default {
		name: "productStatus",
			setup(){
				const {addMoney, totalMoney} = useMoney();
				
				return {
					addMoney,
					totalMoney,
			};
		},
};
</script>
<style scoped>
</style>
```



FeeStatus component

```vue
<template>
	<div>
			<h2> 합산된 요금: {{ totalMoney }} </h2>
		<button @click="addMoney(50)"> 50 </button>
		<button @click="addMoney(100)"> 100 </button>
		<button @click="addMoney(150)"> 150 </button>
		<button @click="addMoney(200)"> 200 </button>
	</div>
</template>
<script>
import useMoney from '../../composables/useMoney'
export default {
		name: "FeeStatus",
			setup(){
				const {addMoney, totalMoney} = useMoney();
				
				return {
					addMoney,
					totalMoney,
			};
		},
};
</script>
<style scoped>
</style>
```



SavingStatus component

```vue
<template>
	<div>
			<h2> 합산된 총 적금: {{ totalMoney }} </h2>
		<button @click="addMoney(1000)"> 1000 </button>
		<button @click="addMoney(2000)"> 2000 </button>
		<button @click="addMoney(1500)"> 1500 </button>
		<button @click="addMoney(2200)"> 2200 </button>
	</div>
</template>
<script>
import useMoney from '../../composables/useMoney'
export default {
		name: "SavingStatus",
			setup(){
				const {addMoney, totalMoney} = useMoney(5000);
				
				return {
					addMoney,
					totalMoney,
			};
		},
};
</script>
<style scoped>
</style>
```



useMoney composition

```javascript

import {ref} from 'vue';

function useMoney(initialTotalMoney = 0){
	const totalMoney = ref(initialTotalMoney);
	function addMoney(price){
		totalMoney.value += price;
	}
	
	return{
		totalMoney,
		addMoney,	
	};
}

export default useMoney;
```

