Scope & Closures
===

## Scope
- Thể hiện khả năng thực thi của các biến (`variable`) trong một phạm vi code.
- Trong js cũng có khái niệm `block scope` và `function scope`.
- Khi function thực thi nó tạo ra `runtime scope`, mô tả pham vị sử dụng các biến của function đó.
- Phạm vi sử dụng biến trong function bao gồm: 
	- Các tham số (`arguments`). 
	- Biến cục bộ đã khai báo trong function (`local variable`).
	- Các biến và tham số thuộc scope của những function parent. 
	- Biến toàn cục (`global variable`).
- Ví dụ: function `child()` sẽ có thể access các biến `a`, `b`, `c` và `param`.
```js
const a = 'a'; // global variable
function parent(param) {
	const b = 'b'; // variable from parent function's scope

	function child() {
		const c = 'c'; // local variable
	}
}
```


### Function Scoped và Block Scoping
- Có thể xem js truyền thống (es5) là một kiểu Function Scoped.
- Các scope trong js được ràng buộc chặc chẻ trong `function`, ngược lại với `block` thì không.
- Các biến được khái báo trong một `function` thì chỉ có thể sử dụng trong function đó. 
- Ngược lại, đối với các biến được khai báo (sử dụng `var`) trong một `block` thì vẫn có thể sử dụng từ bên ngoài block đó. Khá khác biệt so với các ngỗn ngử phổ biến như Java, C/C++.
- Trong ES6 đã có hỗ trợ Block Scoping với 2 cách khai báo biến sử dụng `let` và `const`.

### Scope Chain
- Chuỗi liên kết scope, js engine dựa vào đó để lookup giá trị của biến trong function khi nó duyệt đến biến đó, cho đến khi tìm được giá trị của biến.
- Khi một function được thực thi, thứ tự lookup biến theo scope chain sẽ bắt đầu từ scope ở trong cùng (innermost): (1) các biến local đã khai báo trong function --> (2) các biến thuộc lớp function parent --> (3) các biến global.
- Ví dụ: thứ tự lookup biến trong scope chain khi function `one()` được thực thi sẽ bắt đầu ở scope của nested function ở trong cùng cho đến global scope: `three()` --> `two()` --> `one()` --> `window`.
```js
function one() {
  	two();
  	function two() {
    	three();
    	function three() {
      	// function three's code here
    	}
  	}
}
one();
```