# arguments 参数

* arguments 是函数的一个内置属性
	
	在函数里面直接通过 `arguments` 引用

		function fn(a){
			alert(arguments[0]); // 1
		}
		fn(1);

* arguments 的长度由具体的实参数量决定，不由形参决定。
		
		function fn(a,b,c){
			alert(arguments.length); // 2
		}
		fn(1,2);

* arguments和实参都存在的情况下，两者值是同步的，但是实参未提供的情况下情况下，值不会得到同步。

		function fn(a, b, c){
			a = 100;
      		alert(arguments[0]);       // 100
      		arguments[0] = "newvalue";
      		alert(a);                  // "newvalue"
      		alert(c);                  // "undefined"
      		c = 2012;
      		alert(arguments[2]);       // "undefined"
 		}
		fn(1, 2);

* arguments.callee 返回正在执行的函数的引用。

	递归调用函数

		/* 计算 1~n 的和 */
		function sum(n){
			if(n == 1){
				return 1;
			}else{
				return n + arguments.callee(--n);
			}
		}
		alert(sum(10)); // 55
	
	`callee.length` 返回形参的数量
	
		function fn(a,b,c){
			alert(arguments.length == arguments.callee.length);
		}
		fn(1,2); // false
		fn(1,2,3); // true

	与 `caller` 的区别：caller 返回对调用当前函数的函数的引用
	
		function fnA(){
			fnB();
		};
		function fnB(){
			if(fnB.caller){
				console.log(fnB.caller);
			}else{
				console.log('直接调用');
			}
		};
		fnA(); // fnB函数
		fnB(); // '直接调用'

		