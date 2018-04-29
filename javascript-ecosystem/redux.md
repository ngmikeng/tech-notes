Redux
===

# Three Principles
- **Single source of truth**: State của toàn bộ app được lưu trong một object three, quản lý bởi một single store.
- **State is readonly**: cách để thay đổi state là emit một action, action này là một object để mô tả những gì đã xảy ra với state.
- **Changes are made with pure functions**: Sử dụng pure function reducers để xác định state tree đã được thay đổi bởi các action như thế nào. Reducers nhận đầu vào là state trước đó và một action, nó sẽ trả về state tiếp theo.

# Actions
- Các action là payload thông tin để gửi data từ app đến store, là nguồn thông tin cho store.
- Các action sẽ được gửi bằng method `store.dispatch()`.
- Các action là plain object và bắt buộc phải có thuộc tính `type` để biểu diễn loại action thực hiện, các thuộc tính còn lại đóng vai trò là payload data.
- Cấu trúc Object của action ngoại trừ bắt buộc phải có thuộc tính `type` thì các thuộc tính còn lại có thể tổ chức tùy ý theo một chuẩn nào đó.
```js
{
	type: 'ADD_TODO',
	text: 'Learn Redux'
}
```
```js
{
	type: 'ADD_TODO',
	payload: {
		text: 'Learn Redux'
	}
}
```

# Reducers

# Store
