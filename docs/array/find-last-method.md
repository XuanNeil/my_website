---
sidebar_position: 1
---

# FindLast Method

- `findLast` method iterates (phương thức lặp lại) array theo thứ tự ngược lại và trả về giá trị của phần tử đầu tiên thỏa mãn function kiểm tra được cung cấp. Nếu không có phần tử nào thỏa mãn function kiểm tra, `undefined` sẽ được trả về.


```jsx title="Javascript Demo: Array.findLast()"
const array = [5, 12, 50, 130, 44];
const found = array.findLast((element) => element > 45);
console.log(found);
// expected oupt: 130
```

## Syntax
```
// Arrow function
findLast((element) => { /* … */ })
findLast((element, index) => { /* … */ })
findLast((element, index, array) => { /* … */ })

// Callback function
findLast(callbackFn)
findLast(callbackFn, thisArg)

// Inline callback function
findLast(function (element) { /* … */ })
findLast(function (element, index) { /* … */ })
findLast(function (element, index, array) { /* … */ })
findLast(function (element, index, array) { /* … */ }, thisArg)
```

## Parameters
`callbackFn`:
- 1 function để thực thi cho từng phần tử trong array. Nó sẽ trả về giá trị `truthy` để cho biết 1 phần tử phù hợp đã được tìm thấy.
- Function được gọi với các đối số sau:
    - `element`: Phần tử hiện tại đang được xử lý tron array.
    - `index`: index của phần tử hiện tại đang được xử lý trong array.
    - `array`: array `findIndex()` đã được gọi.
- `thisArg` `Optional`: 1 giá trị để sử dụng như `this` khi thực hiện lệnh gọi `callbackFn`.

## Return value
- Giá trị của phần tử trong array có giá trị index cao nhất thỏa mãn function kiểm tra được cung cấp
- Nếu không tìm thấy phần tử phù hợp, `undefined` sẽ được trả về.

## Examples
1. Tìm object cuối cùng trong 1 array phù hợp với thuộc tính phần tử.
```
const inventory = [
  { name: "apples", quantity: 2 },
  { name: "bananas", quantity: 0 },
  { name: "fish", quantity: 1 },
  { name: "cherries", quantity: 5 },
];

// return true inventory stock is low
function isNotEnough(item) {
  return item.quantity < 2;
}

console.log(inventory.findLast(isNotEnough));
// { name: "fish", quantity: 1 }

```

2. Sử dụng arrow function và destructuring.
```
const inventory = [
  { name: "apples", quantity: 2 },
  { name: "bananas", quantity: 0 },
  { name: "fish", quantity: 1 },
  { name: "cherries", quantity: 5 },
];

const result = inventory.findLast(({quantity}) => quantity < 2 );

console.log(result);
// { name: "fish", quantity: 1 }

```

3. Tìm số nguyên tố cuối cùng trong 1 array.
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

console.log([4, 6, 8, 12].findLast(isPrime)); // undefined, not found
console.log([4, 5, 7, 8, 9, 11, 12].findLast(isPrime)); // 11

```

4. Gọi `findLast()` trên `non-array objects`
```
const arrayLike = {
  length: 3,
  0: 2,
  1: 7.3,
  2: 4,
};
console.log(Array.prototype.findLast.call(arrayLike, (x) => Number.isInteger(x))); // 4
```