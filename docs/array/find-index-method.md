---
sidebar_position: 1
---

# FindIndex Method

- `findIndex` method trả về index của phần tử đầu tiên trong 1 array thỏa mãn chức function kiểm tra được cung cấp. Nếu không có phần tử nào thỏa mãn chức năng kiểm tra, -1 được trả về.


```jsx title="JavaScript Demo: Array.findIndex()"
const array1 = [5, 12, 8, 130, 44];

const isLargeNumber = (element) => element > 13;

console.log(array1.findIndex(isLargeNumber));
// expected output: 3
```

## Syntax

```
// Arrow function
findIndex((element) => { /* … */ })
findIndex((element, index) => { /* … */ })
findIndex((element, index, array) => { /* … */ })

// Callback function
findIndex(callbackFn)
findIndex(callbackFn, thisArg)

// Inline callback function
findIndex(function (element) { /* … */ })
findIndex(function (element, index) { /* … */ })
findIndex(function (element, index, array) { /* … */ })
findIndex(function (element, index, array) { /* … */ }, thisArg)

```

## Parameters
`callbackFn`
- 1 function để thực thi cho từng phần tử trong array. Nó sẽ trả về 1 giá trị `truthy` để cho biết 1 phần tử phù hợp đã được tìm thấy.
- Function được gọi với các đối số:
    -`element`: Phần tử hiện tại đang được xử lý trong array.
    - `index`: Chỉ số của phần tử hiện tại đang được xử lý trong array.
    - `array`: array `findIndex()` đã được gọi.
- `thisArg` `optional`: 1 giá trị để sử dụng làm giá trị này khi thực hiện `callbackFn`.

## Return value
- index của phần tử đầu tiên trong mảng vượt qua bài kiểm tra.
- Nếu không, sẽ trả về -1.

## Examples
1. Tìm chỉ số của một số nguyên tố trong một mảng
```
function isPrime(element) {
  if (element % 2 === 0 || element < 2) {
    return false;
  }
  for (let factor = 3; factor <= Math.sqrt(element); factor += 2) {
    if (element % factor === 0) {
      return false;
    }
  }
  return true;
}

console.log([4, 6, 8, 9, 12].findIndex(isPrime)); // -1, not found
console.log([4, 6, 7, 9, 12].findIndex(isPrime)); // 2 (array[2] is 7)

```

2. Gọi `findIndex()` trên `non-array objects`
```
const arrayLike = {
  length: 3,
  0: 2,
  1: 7.3,
  2: 4,
};
console.log(Array.prototype.findIndex.call(arrayLike, (x) => !Number.isInteger(x))); // 1
```