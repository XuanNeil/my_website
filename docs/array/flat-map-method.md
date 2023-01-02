---
sidebar_position: 1
---

# FlatMap Method

- `flatMap` method trả về 1 array mới được hình thành bằng cách áp dụng hàm gọi lại đã cho từng phần tử của array, sau đó làm phẳng kết quả theo 1 mức. Nó giống hệt với `map()`, theo sau là `flat()` có độ sâu 1 (arr.map(...arg).flat()), nhưng hiệu quả hơn 1 chút so với việc gọi riêng 2 method đó.

```jsx title="JavaScript Demo: Array.flatMap()"
const array = [1, 2, [3], [4, 5], 6, []];
const flattened = array.flatMap(num => num);
console.log(flattened);
// expected output: [1, 2, 3, 4, 5, 6]
```

## Syntax
```
// Arrow function
flatMap((element) => { /* … */ })
flatMap((element, index) => { /* … */ })
flatMap((element, index, array) => { /* … */ })

// Callback function
flatMap(callbackFn)
flatMap(callbackFn, thisArg)

// Inline callback function
flatMap(function (element) { /* … */ })
flatMap(function (element, index) { /* … */ })
flatMap(function (element, index, array) { /* … */ })
flatMap(function (element, index, array) { /* … */ }, thisArg)

```

## Parameters
`callbackFn`:
- 1 function để thực thi cho từng phần tử trong array. Nó sẽ trả về 1 array chứa các phần tử mới của array mới hoặc 1 giá trị không phải array sẽ được thêm vào array mới.
- Function được gọi với các đối số sau:
   `element`: Phần tử hiện tại đang được xử lý trong array.
   `index`: index của phần tử hiện tại đang được xử lý trong array.
`array`: array `flatMap()` đã được gọi
- `thisArg` `Optional`: 1 giá trị được sử dụng như `this` khi thực thi `callbackFn`.

## Return value
- 1 array mới với mỗi phần tử là kết quả của hàm gọi lại và được làm phẳng theo độ sâu là 1.

## Description
- `flatMap` method là 1 phương thức lặp (iterative method). `flatMap` phương thức giống với `map(callbackFn, thisArg)` theo sau bởi `flat(1)` - đối với mỗi phần tử, nó tạo ra 1 array gồm các phần tử mới và nối các array kết quả lại với nhau để tạo thành 1 array mới.
- `flatMap` method là `generic`. Nó chỉ expects giá trị `this` có `length` property và `integer-keyed` properties. Tuy nhiên, giá trị được trả về từ `callbackFn` phải là 1 array nếu nó được làm phẳng.

## Thay thế
- Phân bổ trước và lặp lại rõ ràng.
```
const arr = [1, 2, 3, 4];

arr.flatMap((x) => [x, x * 2]);
// is equivalent to
const n = arr.length;
const acc = new Array(n * 2);
for (let i = 0; i < n; i++) {
  const x = arr[i];
  acc[i * 2] = x;
  acc[i * 2 + 1] = x * 2;
}
// [1, 2, 2, 4, 3, 6, 4, 8]

```
- Lưu ý rằng trong trường hợp cụ thể này, cách tiếp cận `flatMap` chậm hơn so với cách tiếp cận vòng lặp for việc tạo các array tạm thời phải được thu gom rác, cũng như array trả về không cần phải thay đổi kích thước thường xuyên.
- Tuy nhiên, `flatMap` vẫn có thể là giải pháp chính xác trong trường hợp mong muốn tính linh hoạt và dễ đọc của nó.

## Examples
1. map() và flatMap()
```
const arr1 = [1, 2, 3, 4];
arr1.map((x) => [x * 2]);
// [[2], [4], [6], [8]]

arr1.flatMap((x) => [x * 2]);
// [2, 4, 6, 8]

// only one level is flattened
arr1.flatMap((x) => [[x * 2]]);
// [[2], [4], [6], [8]]
```
- Mặc dù những điều trên có thể đạt được bằng cách sử dụng `map`, đây là 1 ví dụ thể hiện tốt hơn việc sử dụng `flatMap()`.

2.
```
const arr1 = ["it's Sunny in", "", "California"];

arr1.map((x) => x.split(" "));
// [["it's","Sunny","in"],[""],["California"]]

arr1.flatMap((x) => x.split(" "));
// ["it's","Sunny","in", "", "California"]
```
- Lưu ý, `length` danh sách đầu ra có thể khác với `length` danh sách đầu vào.

3. Để thêm và xóa items trong map();
// ví dụ: Giả sử chúng ta muốn xóa tất cả các số âm và chia các số lẻ thành số chẳn và 1
```
// Let's say we want to remove all the negative numbers
// and split the odd numbers into an even number and a 1
const a = [5, 4, -3, 20, 17, -33, -4, 18];
//         |\  \  x   |  | \   x   x   |
//        [4,1, 4,   20, 16, 1,       18]

const result = a.flatMap((n) => {
  if (n < 0) {
    return [];
  }
  return n % 2 === 0 ? [n] : [n - 1, 1];
});
console.log(result); // [4, 1, 4, 20, 16, 1, 18]

```

4. Sử dụng `flatMap()` trên sparse arrays
- `callbackFn` sẽ không được gọi cho các vị trí trống (empty) trong mảng nguồn vì `map()` không, trong khi `flat()` bỏ qua các vị trí trống trong array được trả về.
```
console.log([1, 2, , 4, 5].flatMap((x) => [x, x * 2])); // [1, 2, 2, 4, 4, 8, 5, 10]
console.log([1, 2, 3, 4].flatMap((x) => [, x * 2])); // [2, 4, 6, 8]
```

5. Gọi `flatMap()` trên `non-array objects`
```
const arrayLike = {
  length: 3,
  0: 1,
  1: 2,
  2: 3,
};
console.log(Array.prototype.flatMap.call(arrayLike, (x) => [x, x * 2]));
// [1, 2, 2, 4, 3, 6]

// Array-like objects returned from the callback won't be flattened
console.log(
  Array.prototype.flatMap.call(arrayLike, (x) => ({
    length: 1,
    0: x,
  })),
);
// [ { '0': 1, length: 1 }, { '0': 2, length: 1 }, { '0': 3, length: 1 } ]

```