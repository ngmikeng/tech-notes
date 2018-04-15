Function at Runtime
==

## First-Class Functions
- Các function trong javascript đểu được xem là First-Class function. Tức là, những hoạt động như lưu vào biến, là giá trị return trong một function hay là tham số truyền vào một function khác ta làm được với các cấu trúc dữ liệu như `number`, `string`, `object`, `array`... thì đối với function ta cũng làm được y như vậy.
- Vì function có thể là tham số truyền vào một function khác nên ta có khái niệm callback trong javascript.
- Function trong javascript cũng được xem là object, có kiểu dữ liệu là object nhưng điểm khác nhau chủ yếu giữa function và một object đó là, function có thể được gọi (invoked với `()`), object thì không thể.

## Callback Functions
- Callback function là các function được truyền vào một function khác như là một tham số (parameter).
- Do cơ chế truyền vào như tham số, callback function có thể ủy thác (delegate) việc gọi (invoke) function đó cho function khác (là function đc truyền vào), giúp phát triển ứng dụng theo hướng composition, hiệu quả hơn trong việc reuse code.
- Function nhận một function khác như là một tham số gọi là higher-order function.
- Ví dụ sử dụng callback check điểu kiện:

```js
function dieuKienCoGau(thuNhap) {
	if (thuNhap >= 500) {
		return true;
	}
	return false;
}

function kiemTraCoGau(thuNhap, isCoGau) {
	if (isCoGau(thuNhap)) {
		console.log('Chuc mung! ban da thoat kiep FA :).');
	} else {
		console.log('Co gang len nao FA! :(');
	}
}

kiemTraCoGau(1000, dieuKienCoGau);
```

- Một số hàm built-in xử lý array có áp dụng callback như là: `forEach()`, `filter()`, `map()`, `reduce()`...
- Khi sử dụng callback, có một quy ước (convention) khuyến cáo nên sử dụng để xử lý lỗi gọi là error-first callback. Tức là, tham số (parameter) đầu tiên của callback sẽ là error để bắt lỗi. Việc xử lý lỗi là rất cần thiết trong các trường hợp mà function nhận callback truyền vào chạy bất động bộ (asynchronous).

```js
function handleResponse(error, result) {
	if (error) {
		console.log(error);
		return;
	}
	console.log(result);
}

function asynFunction(isError, callback) {
	if (isError) {
		callback(new Error('Something went wrong'));
	} else {
		callback(null, 'Everything good!');
	}
}

asynFunction(true, handleResponse);
```