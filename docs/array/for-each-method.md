---
sidebar_position: 1
---

# ForEach Method

- `forEach()` method thực thi 1 hàm được cung cấp 1 lần cho mỗi phần tử array.
```jsx title="JavaScript Demo: Array.forEach()"
const array1 = ['a', 'b', 'c'];
array1.forEach((element) => console.log(element));
// expected output: "a"
// expected output: "b"
// expected output: "c"
```

## Syntax

```
// Arrow function
forEach((element) => { /* … */ })
forEach((element, index) => { /* … */ })
forEach((element, index, array) => { /* … */ })

// Callback function
forEach(callbackFn)
forEach(callbackFn, thisArg)

// Inline callback function
forEach(function (element) { /* … */ })
forEach(function (element, index) { /* … */ })
forEach(function (element, index, array) { /* … */ })
forEach(function (element, index, array) { /* … */ }, thisArg)

```

## Parameters
`callbackFn`:
- 1 function để thực thi cho từng phần tử trong array. Giá trị trả về của nó bị loại bỏ.
- Hàm được gọi với các đối số sau:
    `element`: Phần tử hiện tại đang được xử lý trong array.
    `index`: Chỉ số của phần tử hiện tại đang được xử lý trong array.
    `array`: array `forEach()` đã được gọi
`thisArg` `Optional`: 1 giá trị để sử dụng như `this` khi thực thi `callbackFn`.

## Return value
- `undefined`

## Description
- `forEach()` method là 1 phương thức lặp (iterative method). Nó gọi hàm `callbackFn` được cung cấp 1 lầ cho mỗi phần tử trong 1 array theo thứ tự index tăng dần. Không giống như `map()`, `forEach()` luôn trả về giá trị `undefined` và không thể sâu chuỗi. Trường hợp sủ dụng điển hình là thực hiện các tác dụng phụ ở cuối chuỗi.
- `callbackFn` chỉ được gọi cho các index array có giá trị được gán. Nó không được gọi cho các vị trí trống trong các array thưa thớt.
- `forEach()` không làm thay đổi array mà nó được gọi, nhưng function được cung cấp dưới dạng `callbackFn` có thể. Tuy nhiên, lưu ý rằng `length` của array được lưu trước lần gọi đầu tiên của callbackFn. Vì vậy:
    - `callbackFn` sẽ không truy cập bất kỳ phần tử nào được thêm vào vượt quá độ dài ban đầu của array khi lệnh gọi `forEach()` bắt đầu.
    - Cách thay đổi đối với các index đã truy cập không khiến `callbackFn` được gọi lại trên chúng.
    - Nếu 1 phần tử hiện có, chưa được truy cập của array bị thay đổi bởi `callbackFn`, giá tri của nó được truyền cho `callbackFn` sẽ là giá trị tạm thời điểm phần tử đó được truy cập. Các phần tử đã xóa không được truy cập.
- `forEach()` method là `generic`. Nó chỉ mong đợi giá trị như `this` có `length` property và `integer-keyed` properties.
- Không có cách nào để dừng hoặc ngắt vòng lặp `forEach()` ngoài việc đưa ra 1 ngoại lệ. Nếu bạn cần hành vi như vậy, thì `forEach()` method là công cụ không phù hợp.
- Việc kết thúc sớm có thể được thực hiện bằng các lệnh lặp như `for`, `for...of` and `for...in`. Các phương thức như `every()`, `some()`, `find()` and `findIndex` cũng dừng lặp lại ngay lập tức khi không cần lặp lại nữa.
- `forEach()` mong đợi 1 function đồng bộ (synchronous function) - nó không chờ đợi `promises`. Đảm bảo rằng bạn nhận thức được các hàm ý trong khi sử dụng `promise` (async function) làm `forEach` callback.
```
const ratings = [5, 4, 5];
let sum = 0;

const sumFunction = async (a, b) => a + b;

ratings.forEach(async (rating) => {
  sum = await sumFunction(sum, rating);
});

console.log(sum);
// Naively expected output: 14
// Actual output: 0

```

## Examples
1. Sử dụng `forEach()` trên sparse arrays.
```
const arraySparse = [1, 3, /* empty */, 7];
let numCallbackRuns = 0;
arraySparse.forEach((element) => {
    console.log({element});
    numCallbacksRuns++;
});
console.log(numCallbacksRuns);

// { element: 1 }
// { element: 3 }
// { element: 7 }
// { numCallbackRuns: 3 }
```

2. Converting a for loop to forEach
```
const items = ["item1", "item2", "item3"];
const copyItems = [];

// before
for(let i = 0; i < items.length; i++){
    copyItems.push(items[i]);
}

// after
items.forEach((item) => {
    copyItems.push(item);
});
```

3. Sử dụng `thisArg`.
- vì tham số `thisArg` được cung cấp cho `forEach`, nên nó được truyền để `callback` mỗi khi nó được gọi. callback sử dụng `this` làm giá trị.
```
class Counter {
  constructor() {
    this.sum = 0;
    this.count = 0;
  }
  add(array) {
    // Only function expressions will have its own this binding
    array.forEach(function countEntry(entry) {
      this.sum += entry;
      ++this.count;
    }, this);
  }
}

const obj = new Counter();
obj.add([2, 5, 9]);
console.log(obj.count); // 3
console.log(obj.sum); // 16

```

4. 1 object copy function.
```
const copy = (obj) => {
  const copy = Object.create(Object.getPrototypeOf(obj));
  const propNames = Object.getOwnPropertyNames(obj);
  propNames.forEach((name) => {
    const desc = Object.getOwnPropertyDescriptor(obj, name);
    Object.defineProperty(copy, name, desc);
  });
  return copy;
};

const obj1 = { a: 1, b: 2 };
const obj2 = copy(obj1); // obj2 looks like obj1 now

```

5. Flatten an array
```
const flatten = (arr) => {
  const result = [];
  arr.forEach((item) => {
    if (Array.isArray(item)) {
      result.push(...flatten(item));
    } else {
      result.push(item);
    }
  });
  return result;
};

// Usage
const nested = [1, 2, 3, [4, 5, [6, 7], 8, 9]];
console.log(flatten(nested)); // [1, 2, 3, 4, 5, 6, 7, 8, 9]

```

6. Gọi `forEach()` trên `non-array objects`
```
const arrayLike = {
  length: 3,
  0: 2,
  1: 3,
  2: 4,
};
Array.prototype.forEach.call(arrayLike, (x) => console.log(x));
// 2
// 3
// 4

```