# ES6 函数提要

## 常用
	
1. `默认参数` 也可以是 `表达式`

	```
	let value = 5;
	function getValue() {
	    return value++;
	}
	function add(first, second = getValue()) {
	    return first + second;
	   }
	console.log(add(1, 1));  // 2
	console.log(add(1));     // 6
	console.log(add(1));     // 7
	```
2. `TDZ`

	```
	function add(first = second, second) {
	    return first + second;
	}
	console.log(add(1, 1));              // 2
	console.log(add(undefined, 1));      // throws an error
	```

3. `rest`
	
	
	```
	function func(arg1, ...rest) {
		// arg1: 1,
		// rest: [2, 3, 4]
		// ...
	}
	
	func(1, 2, 3, 4)
	
	```
5. `spread: ...`
	
	```
	let values = [25, 50, 75, 100]
	Math.max.apply(Math, values)   // 100
	```


5. 区分构造函数调用与普通函数调用


	```	
	function Person() {
		return new.target;
	}
	
	Person() 	 // undefined
	new Person() // Person
	```
	
	可以用来限制函数调用
	
	```
	// 限定当前函数只能用做构造函数
	function Person(name) {
	```
6. 箭头函数
	
	```
	特点：
	
	1. 没有 this, super, arguments, 和 new.target 绑定, 箭头函数里的这些值指向的是最近的一个非箭头函数的对应值
	2. 不能用`new`调用
	3. 没有`prototype`
	4. 不能改变`this`
	5. 没有`arguments`
	6. 参数不能重名
	```

	语法
	
	
	```
	let reflect = value => value
	
	let noop = () => ()
	
	let sum = (num1, num2) => {
		return num1 + num2
	}
	
	```


## 其他

1. `length`

	```
	function func(arg1, arg2=2, ...rest) {
		// ...
	}
	
	console.log(func.length)  // 1
	```
	
	
	```
	注: 函数length为函数有名参数的个数，默认参数和 rest 参数不计入其内
	```
2. `name`

	
	```
	function doSomething() {


	```
	
	特殊情况:
	
	```
	var doSomething = function doSomethingElse() {
	  // empty
	};
	var person = {
	  get firstName() {
	    return "Nicholas"
	  },
	  sayName: function () {
	    console.log(this.name);
	  }
	}
	console.log(doSomething.name);      // "doSomethingElse"
	console.log(person.sayName.name);   // "sayName"
	console.log(person.firstName.name); // "get firstName"
	
	```
	
	
	```
var doSomething = function() {
  		// empty
};
console.log(doSomething.bind().name); // "bound doSomething"
console.log((new Function()).name); // "anonymous"
	```
3. 块级函数


	```
	"use strict";
	   }
	```

4. 尾调优化

	```
	优化条件:
	
	1. 尾调函数里不能引用父函数里变量 ，即不能是闭包
	2. 父函数在尾调函数执行后，没有其他的操作了
	3. 尾调函数执行结果是父函数的返回值
	```
	
	1. 符合条件的优化
	
		```
		"use strict";
		```

	2. 不符合条件例子
	
		```
		// 不符合第三条
		"use strict";
		
		```

	
		```
		// 不符合第二条
		"use strict";
		```
		
				
		```
		 // 不合符第一条
		"use strict";
		```


		```
		"use strict";
		```

	3. 一个尾调优化的例子

	
		```
		
		function factorial(n) {
		//改为
		function factorial(n, p = 1) {
		```
