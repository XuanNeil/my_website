---
sidebar_position: 1
---

# Flat Method

- `flat()` method tạo 1 array mới với tất cả các phần tử array con được nối vào nó 1 cách đệ quy đến độ sâu (depth) đã chỉ định.

```jsx title="JavaScript Demo: Array.flat()"
const array1 = [0, 1, 2, [3, 4]];
console.log(array1.flat());
// expected output: [0, 1, 2, 3, 4]

const array2 = [0, 1, 2, [[[3, 4]]]];
console.log(array2.flat(2));
// expected output: [0, 1, 2, [3, 4]];
```

## Syntax
```
flat()
flat(depth)
```

## Parameters
`depth` `Optional`: Mức depth xác định độ sâu của cấu trúc array lồng nhau sẽ được làm phẳng. Mặc định là 1.

## Return value
- Trả về 1 array mới với các phần tử của array con được nối vào nó.

## Description
- `flat()` method là 1 phương thức `copying method`. Nó không thay đổi `this` mà thay vào đó trả về 1 `shallow copying` chứa các phần tử giống như các phần tử của array ban đầu.
- `flat()` method bỏ qua các ô trống nếu aray được làm phẳng
- `flat()` method `generic`. Nó chỉ mong đợi giá trị `this` có `length` property và `integer-keyed` properties. Tuy nhiên, các phần tử của nó phải là array nếu chúng được làm phẳng.

## Examples
1. Làm phẳng các array lồng nhau.
```
const arr1 = [1, 2, [3, 4]];
arr1.flat(); // [1, 2, 3, 4]

const arr2 = [1, 2, [3, 4, [5, 6]]];
arr2.flat(); // [1, 2, 3, 4, [5, 6]];

const arr3 = [1, 2, [3, 4, [5, 6]]];
arr3.flat(2); // [1, 2, 3, 4, 5, 6];

const arr4 = [1, 2, [3, 4, [5, 6, [7, 8, [9, 10]]]]];
arr4.flat(Infinity); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10] 
```

2. Sử dụng `flat()` trên sparse arrays.
```
const arr5 = [1, 2, ,4, 5];
console.log(arr5.flat()); // [1, 2, 4, 5]

const arr = [1, , 3, ["a", , "c"]];
console.log(arr.flat()); // [1,3, "a", "c"]

const arr2 = [1, , 3, ["a", ,["d", , "e]]];
console.log(arr2.flat()); // [1, 3, "a", ["d", empty, "e"]];
console.log(arr2.flat(2)); // [1, 3, "a", "d", "e"];
```

3. Gọi `flat()` trên `non-array objects`
- `flat()` method đọc `length` property của `this` và sau đó truy cập từng index số nguyên.
- Nếu phần tử không phải là 1 array, nó sẽ được thêm trực tiếp vào kết quả.
- Nếu phần tử là 1 array, nó sẽ được làm phẳng theo tham số `depth`

```
const arrayLike = {
    length: 3,
    0: [1, 2],
    // Array-like objects aren't flattened
    1: {lengh: 2, 0: 3, 1: 4},
    2: 5,
}
console.log(Array.prototype.flat.call(arrayLike));
// [1, 2, {'0': 3, '1': 4, length: 2}, 5]
```