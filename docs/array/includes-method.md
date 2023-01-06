---
sidebar_position: 1
---

# Includes Method

- Phương thức `includes()` xác định xem một mảng có bao gồm một giá trị nhất định trong số các mục của nó hay không, trả về `true` hoặc `false`.

```jsx title="JavaScript Demo: Array.includes()"
const array = [1, 2, 3];
console.log(array.includes(1));
// expected output: true

const pets = ['cat', 'dog', 'bat'];
console.log(pets.includes('dog'));
// expected output: true

console.log(pets.includes('at'));
// expected output: false
``` 

## Syntax
```
includes(searchElement)
include(searchElement, fromIndex)

```

## Parameters
`searchElement`: Gía trị cần tìm
`fromIndex` `Optional`: 
- Chỉ mục dựa trên số 0 để bắt đầu tìm kiếm, được chuyển đổi thành số nguyên.
    - Index âm (negative) đếm ngược từ cuối mảng - Nếu fromIndex < 0, fromIndex + array.length được sử dụng. Tuy nhiên mảng vẫn được tìm kiếm từ trước ra sau trong trường hợp này.
    - Nếu fromIndex < -array.length hoặc fromIndex bị bỏ qua, thì 0 sẽ được sử dụng sẽ khiến toàn bộ mảng được tìm kiếm.
    - Nếu fromIndex >= array.length, thì array không được tìm kiếm và trả về false.

## Return value
- Trả về 1 giá trị boolean là `true` nếu giá trị `searchElement` được tìm thấy trong mảng (hoặc 1 phần của mảng được chỉ định bởi index `fromIndex`, nếu được chỉ định).

## Description
- Phương thức `includes()` so sánh `searchElement` với các phần tử của array bằng thuật toán `SameValueZero`. Các giá trị của 0 đều được coi là bằng nhau, bất kể dấu. (Tức là -0 bằng 0), nhưng false không được coi là giống 0. NaN có thể được tìm kiếm chính xác.
- Khi được sử dụng trên `sparse arrays`, phương thức `includes()` lặp lại các vị trí trống như thể chúng có giá trị `undefined`.
- phương thức `includes()` là `generic`. Nó chỉ mong đợi giá trị `this` có thuộc tính `length` và thuộc tính `integer-keyed`.

## Examples
1. Sử dụng `includes()`
```
const array = [1, 2, 3];
array.includes(1); // true
array.includes(4); // false
array.includes(3, 3); // false
array.includes(3, -1); // true

const array2 = [1, 2, NaN];
array2.includes(NaN); // true
array2.includes("2"); // false
```

2. Khi fromIndex lớn hơn hoặc bằng độ dài của array.
```
const arr = ["a", "b", "c"];

arr.includes("c", 3); // false
arr.includes("c", 100); // false
```

3. Chỉ số tính toán nhỏ hơn 0
- Nếu `fromIndex` là 1 số nguyên, thì index được tính toán để sử dụng làm index trong array để bắt đầu tìm kiếm `searchElement`.
- Nếu index được tính toán nhở hơn hoặc bằng 0, thì toàn bộ mảng sẽ được tìm kiếm.
```
// array length is 3
// fromIndex is -100
// computed index is 3 + (-100) = -97

const arr = ["a", "b", "c"];

arr.includes("a", -100); // true
arr.includes("b", -100); // true
arr.includes("c", -100); // true
arr.includes("a", -2); // false
```

4. Gọi `includes()` on non-array objects
```
const arrayLike = {
  length: 3,
  0: 2,
  1: 3,
  2: 4,
};
console.log(Array.prototype.includes.call(arrayLike, 2));
// true
console.log(Array.prototype.includes.call(arrayLike, 1));
// false
```