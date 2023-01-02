---
sidebar_position: 1
---

# FindLastIndex Method

- `findLastIndex` method iterates theo thứ tự ngược lại và trả về index của phần tử đầu tiên thỏa mãn function kiểm tra được cung cấp. Nếu không có phần tử nào thỏa mãn function kiểm tra, -1 sẽ được trả về.


```jsx title="JavaScript Demo: Array.findLastIndex()"
const array = [5, 12, 50, 130, 44];

const isLargeNumber = (element) => element > 45;

console.log(array.findLastIndex(isLargeNumber));
// expected output: 3
// Index of element with value: 130
```

## Syntax
```
// Arrow function
findLastIndex((element) => { /* … */ })
findLastIndex((element, index) => { /* … */ })
findLastIndex((element, index, array) => { /* … */ })

// Callback function
findLastIndex(callbackFn)
findLastIndex(callbackFn, thisArg)

// Inline callback function
findLastIndex(function (element) { /* … */ })
findLastIndex(function (element, index) { /* … */ })
findLastIndex(function (element, index, array) { /* … */ })
findLastIndex(function (element, index, array) { /* … */ }, thisArg)

```

## Parameters
`callbackFn`:
- 1 function để thực thi cho từng phần tử trong array. Nó sẽ trả về 1 giá trị `truthy` để cho biết 1 phần tử phù hợp đã được tìm thấy.
- Function được gọi với các đối số sau:
    `element`: Phần tử hiện tại đang được xử lý trong array.
    `index`: index của phần tử hiện tại đang được xử lý trong array.
    `array`: array `findIndexLast()` đã được gọi.
- `thisArg` `Optional`: 1 giá trị được sử dụng như `this` khi thực thi `callbackFn`.

## Return value
- Index của phần tử cuối cùng (chỉ số cao nhất) trong array vượt qua bài kiểm tra.
- Ngược lại, -1 sẽ được trả về nếu không tìm thấy phần tử phù hợp.

## Examples
1. Tìm index của số nguyê tố cuối cùng trong 1 array.
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

console.log([4, 6, 8, 12].findLastIndex(isPrime)); // -1, not found
console.log([4, 5, 7, 8, 9, 11, 12].findLastIndex(isPrime)); // 5
```

2. Gọi `findLastIndex()` trên `non-array objects`
```
const arrayLike = {
    length: 3,
    0: 2,
    1: 7.3,
    2: 4
};
console.log(Array.prototype.findLastIndex.call(arrayLike, (x) => Number.isInteger(x))); //2
```