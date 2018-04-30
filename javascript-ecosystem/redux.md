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
- **Action Creator**: là function return về một action.
```js
function addTodo(text) {
  return {
    type: 'ADD_TODO',
    text
  }
}
```

# Reducers
- Reducer xác định state của app sẽ thay đổi như thế nào tương ứng với mô tả của action được gửi đến store.
- Action chỉ mô tả thay đổi gì sẽ xảy ra với state (What), còn reducer thì mô tả cách state sẽ thay đổi như thế nào (How).
- Reducer là pure function nhận đầu vào là state trước đó và một action, giá trị trả về của nó là state tiếp theo.
- Reducer là pure function do đó **không** làm những việc sau:
	- Mutate các arguments của nó.
	- Thực hiện các hoạt động gây ra side effect như gọi API, routing transitions.
	- Gọi các non-pure functions khác như `Math.random()`, `Date.now()`;
- **Reducer Composition**: tách reducer thành các function hoặc file riêng biệt, mỗi function này sẽ quản lý một phần của object state, có thể theo từng thuộc tính hoặc theo domain data khác nhau. Redux cung cấp hàm `combineReducers()` để kết hợp các function đã tách lại với nhau thành một reducer hoàn chỉnh.
- Ví dụ sử dụng combineReducer:
```js
import { combineReducers } from 'redux'
​
const reducer = combineReducers({
  a: doSomethingWithA,
  b: processB,
  c: c
})
​
export default reducer
```
- Và kết quả implement tương tự khi không dùng combineReducer.
```js
function reducer(state = {}, action) {
  return {
    a: doSomethingWithA(state.a, action),
    b: processB(state.b, action),
    c: c(state.c, action)
  }
}

export default reducer
```

# Store
