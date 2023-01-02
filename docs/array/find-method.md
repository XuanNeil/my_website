---
sidebar_position: 1
---

# Find Method

- Find method trả về phần từ đầu tiên trong array đáp ứng function kiểm tra được cung cấp. Nếu không có giá trị nào thỏa mãn chức năng kiểm tra, `undefined` sẽ được trả về.
- Nếu bạn cần `index` của phần tử được tìm thấy trong array, hãy sử dụng `findIndex()`.
- Nếu bạn cần tìm `index of a value`, sử dụng `indexOf()` (Nó tương tự như `findIndex`, nhưng kiểm tra từng phần tử xem có bằng nhau với giá trị thay vì sử dụng function kiểm tra).
- Nếu bạn cần tìm xem 1 giá trị có `exists` trong 1 array hay không, sử dụng `includes()`. Nó kiểm tra từng phần tử xem có bằng nhau với giá trị.
- Nếu bạn cần tìm xem có phần từ nào thỏa mãn function kiểm tra được cung cấp hay không, hãy sủ dụng `some()`

```jsx title="JavaScript Demo: Array.find()"
    const array = [2, 5, 20, 9, 10, 12];
    const found = array.find(element => element > 10);
    console.log(found);
    // expected output: 20
```

## Syntax
```
    // Arrow function
    find((element) => { /* ... */ });
    find((element, index) => { /* ... */ });
    find((element, index, array) => { /* ... */ });
    
    // Callback function
    find(callbackFn);
    find(callbackFn, thisArg);
    
    // Inline callback function
    find(function(element){ /* ... */ });
    find(function(element, index){ /* ... */ });
    find(function(element, index, array) { /* ... */ });
    find(function(element, index, array) { /* ... */ }, thisArg);
```

## Parameters
`callbackFn`:
- 1 Function để thực thi cho từng phần tử trong array. Nó trả về 1 giá trị `truthy` cho biết 1 phần tử phù hợp đã được tìm thấy.
- Function được gọi gồm các đối số sau:
    - `element`: Phần tử hiện tại đang được xử lý trong array.
    - `index`: Chỉ mục của phần tử hiện tại đang được xử lý trong array.
    - `array`: Mảng array `find` đã được gọi.
- `thisArg` `optional`:
    - 1 giá trị để xử dụng làm giá trị này khi thực hiện `callbackFn`

## Return Value
- Trả về phần tử đầu tiên trong array thỏa mãn function kiểm tra được cung cấp.
- Nếu không có giá trị nào thõa mãn, `undefined` sẽ được trả về.

## Description
- `find` phương thức là 1 phương thức lặp `interative method`.
- Nó gọi hàm callbackFn được cung cấp 1 lần cho mỗi phần tử trong 1 array theo thứ tự index tăng dần, cho đến khi hàm `callbackFn` trả về giá trị `truthy`. `find` sau đó trả về phần tử đó và ngừng lặp qua array.
- Nếu `callbackFn` không có giá trị nào trả về `truthy`, `find` trả về `undefined`.
- `callbackFn` được gọi cho mọi index của array, không chỉ những chỉ mục có giá trị được gán.
- Các index trống trong array thưa thót (sparse arrays) hoạt động giống như `undefined`.
- `find` không thay đổi array mà nó được gọi, nhưng function cung cấp dưới dạng `callbackFn` có thể. Tuy nhiên, lưu ý rằng độ dài của array được lưu trước lần gọi đầu tiên của `callbackFn`. Vì vậy
    - `callbackFn` sẽ không truy cập bất kỳ phần tử nào được thêm vào ngoài độ dài ban đầu của array khi lệnh gọi `find` được bắt đầu.
    - Các thay đổi đối với các index đã truy cập không khiến `callbackFn` được gọi lại.
    - Nếu 1 phần tử hiện có, chưa được truy cập của array bị thay đổi bởi `callbackFn`, giá trị của nó được truyền cho `callbackFn` sẽ là giá trị tại thòi điểm phần tử đó được truy cập. Các phần tử đã xóa được truy cập như thể chúng `undefined`.
- `find` là 1 phương thức `generic`. Nó chỉ mong đợi giá trị `this` của `length` property và `integer-keyed` properties.

## Examples
1. Tìm 1 object trong 1 array bằng 1 trong các property của nó.
```
    const inventory = [
      { name: "apples", quantity: 2 },
      { name: "bananas", quantity: 0 },
      { name: "cherries", quantity: 5 },
    ];
   
   function isCherries(fruit){
    return fruit.name === "cherries"
   } 
   const listCherries = inventory.find(isCherries);
   console.log(listCherries);
   // {name: "cherries", qunatity: 5}
```
2. Sử dụng arrow functin và destructuring
```
    const inventory = [
      { name: "apples", quantity: 2 },
      { name: "bananas", quantity: 0 },
      { name: "cherries", quantity: 5 },
    ];
    const result = inventory.find(({name}) => name === "cherries");
    console.log(result); // {name: "cherries", quantity: 5}
```

3. Tìm 1 số nguyên tố trong 1 array.
```
function isPrime(element, index, array) {
  let start = 2;
  while (start <= Math.sqrt(element)) {
    if (element % start++ < 1) {
      return false;
    }
  }
  return element > 1;
}

console.log([4, 6, 8, 12].find(isPrime)); // undefined, not found
console.log([4, 5, 8, 12].find(isPrime)); // 5

```

4. Gọi `find` trên `non-array` objects
```
const arrayLike = {
  length: 3,
  0: 2,
  1: 7.3,
  2: 4,
};
console.log(Array.prototype.find.call(arrayLike, (x) => !Number.isInteger(x)));
// 7.3

```