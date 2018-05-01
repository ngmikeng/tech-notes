Redux
===

## Three Principles
- **Single source of truth**: State của toàn bộ app được lưu trong một object three, quản lý bởi một single store.
- **State is readonly**: cách để thay đổi state là emit một action, action này là một object để mô tả những gì đã xảy ra với state.
- **Changes are made with pure functions**: Sử dụng pure function reducers để xác định state tree đã được thay đổi bởi các action như thế nào. Reducers nhận đầu vào là state trước đó và một action, nó sẽ trả về state tiếp theo.

## Actions
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

## Reducers
- Reducer xác định state của app sẽ thay đổi như thế nào tương ứng với mô tả của action được gửi đến store.
- Action chỉ mô tả thay đổi gì sẽ xảy ra với state (What), còn reducer thì mô tả cách state sẽ thay đổi như thế nào (How).
- Reducer là pure function nhận đầu vào là state trước đó và một action, giá trị trả về của nó là state tiếp theo.
- Reducer là pure function do đó **không** làm những việc sau:
	- Mutate các arguments của nó;
	- Thực hiện các hoạt động gây ra side effect như gọi API, routing transitions;
	- Gọi các non-pure functions khác như `Math.random()`, `Date.now()`;
- **Reducer Composition**: tách reducer thành các function hoặc file riêng biệt, mỗi function này sẽ quản lý một phần của object state, có thể theo từng thuộc tính hoặc theo domain data khác nhau. Redux cung cấp hàm `combineReducers()` để kết hợp các function đã tách lại với nhau thành một reducer hoàn chỉnh.
- Ví dụ sử dụng `combineReducer()`:
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

## Store
- Store là object đóng vai trò kết hợp action và reducer lại với nhau, hay nói cách khác `action` và `reducer` sẽ làm việc với nhau thông qua `store`.
- Store giữ một số nhiệm vụ sau:
  - Vai trò như người bảo vệ state của cả app;
  - Cho phép access state thông qua method `getState()`;
  - Cho phép thay đổi state thông qua method `dispatch(action)`;
  - Đăng ký các listener thông qua method `subscribe(listender)`;
  - Xử lý hủy đăng ký listener thông qua function được trả về bởi `subscribe(listender)`;
- Toàn bộ app chỉ nên có duy nhất 1 store. Khi muốn chia nhỏ data để xử lý logic thì xem xét đến **Reducer Composition** thay vì tạo ra nhiều store khó quản lý.
- Tạo ra store từ một reducer thông qua methode `createStore(reducer)`.
```js
import { createStore } from 'redux'
import todoApp from './reducers'
const store = createStore(todoApp)
```
## Data Flow (Data life cycle)
1. Khi gọi `store.dispatch(action)`.
- Action là một plain object chỉ mô tả what happened, có thể hình dung action như một đoạn tóm tắt thông tin cho một bản tin.
```js
{ type: 'LIKE_ARTICLE', articleId: 42 }
{ type: 'FETCH_USER_SUCCESS', response: { id: 3, name: 'Mary' } }
{ type: 'ADD_TODO', text: 'Read the Redux docs.' }
```
- Có thể gọi `store.dispatch(action)` ở bất kỳ đâu trong app. Ví dụ gọi trong component, XHR callback, hoặc trong các hàm schedule intervals.
2. Redux store sẽ gọi reducer function.
- Store sẽ truyền vào 2 tham số cho reducer: object state tree hiện tại và object action.
- Reducer là pure function để tính toàn và return về state kế tiếp.
3. Root reducer có thể được kết hợp từ nhiều reducer khác nhau để kết quả cuối cùng là return về một object state tree.
- Redux cung cấp helper `combineReducers()` để kết hợp các reducer đã chia tách cho root reducer.
- Khi emit một action, `combineReducers()` sẽ gọi các hàm reducer đã chia tách, sau đó combine các kết quả đã trả về thành một object state tree.
4. Redux store lưu lại object state tree hoàn chỉnh đã được trả về từ root reducer.
- Object state tree sẽ là state tiếp theo của app.
- Các listener đã đăng ký bởi `store.subscribe(listener)` sẽ được gọi.
- Các listener có thể gọi `store.getState()` để lấy state hiện tại.