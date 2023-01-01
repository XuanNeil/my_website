---
sidebar_position: 1
---

# Filter Method

- Filter method tạo **shallow copy** của 1 phần của 1 array nhất định, được lọc xuống chỉ các phần tử mảng đã vượt qua bài kiểm tra do function cung cấp thực hiện.
```jsx title="JavaScript Demo: Array.filter()"
const words = ["spray", "limit", "elite", "exuberant", "destruction", "present"];

const result = words.filter(word => word.length > 6);

console.log(result);
//expected output: Array ["exuberant", "destruction", "present"];
``` 

## Syntax
```
// Arrow function
    filter((element) => { /*...*/ })
    filter((element, index) => { /*...*/ })
    filter((element, index, array) => { /*...*/ })

// Callback function
    filter(callbackFn)
    filter(callbackFn, thisArg)
    
// Inline callback function
    filter(funtion (element) { /* ... */ })
    filter(function (element, index) { /* ... */ })
    filter(function (element, index, array) { /* ... */ })
    filter(function (element, index, array) { /* ... */ }, thisArg)    
```

## Parameters
- `callbackFn`
    - → 1 function để thực thi cho từng phần tử trong mảng. Nó return 1 **truthy** để giữ phần tử trong array kết quả và 1 giá trị **falsy** nếu không. 
    - → Function được gọi với các đối số (arguments) sau: 
        - `element`: Phần tử hiện tại đang được xử lý trong array.
        - `index`: Chỉ số của phần tử hiện tại đang được xử lý trong array.
        - `array`: Array `filter()` đã được gọi.
- `thisArg` `Optional`: 1 giá trị để sử dụng làm giá trị này khi thực hiện `callbackFn`.

## Return value
- 1 `shallow copy` của một phần của array đã cho, được lọc xuống chỉ các phần tử tử mảng đã cho vượt qua bài kiểm tra do function cung cấp thực hiện.
- Nếu không có phần tử nào vượt qua bài kiểm tra, 1 array empty sẽ được trả về.

## Description
- `filter` method là 1 phương thức lặp (iterative method).
  - Nó gọi `callbackFn` được cung cấp 1 lần cho mỗi phần tử trong 1 array.
  - Và xây dựng 1 array mới gồm tất cả các giá trị mà hàm `callbackFn` trả về giá trị `truthy`.
  - Các phần tử array không vượt qua kiểm tra `callbackFn` sẽ không được đưa vào array mới.
- `callbackFn` chỉ được gọi cho các chỉ mục array có giá trị được gán. Nó không được gọi cho các vị trí trống trong các array thưa thớt (sparse arrays).
- `filter` là 1 phương thức sao chép (copying method).
  - Nó không thay đổi điều này mà thay vào đó trả về 1 `shallow copy` chứa các phần tử giống như các phần tử từ array ban đầu (với 1 số được lọc ra).
  - Tuy nhiên, hàm được cung cấp dưới dạng `callbackFn` có thể thay đổi array. Tuy nhiên, lưu ý rằng độ dài của array được lưu trước lần gọi đầu tiên của `callbackFn`. Vì vậy
    - `callbackFn` sẽ không truy cập bất kỳ phần tử nào được thêm vào vượt quá độ dài ban đầu của array khi lệnh gọi `filter` bắt đầu.
    - các thay đổi đối với các chỉ mục đã truy cập không khiến `callbackFn` được gọi lại.
    - Nếu 1 phần tử hiện có, chưa được truy cập của array bị thay đổi bởi `callbackFn`, giá trị của nó được truyền cho `callbackFn` sẽ là giá trị tại thời điểm phần tử đó được truy cập. Các phần tử đã xóa không được truy cập.
- `filter` method là generic. Nó chỉ mong đợi giá trị `this` có length property and integer-keyed properties.

## Examples

1. Filtering out all small values
- Ví dụ sau sử dụng filter() để tạo 1 array có tất cả các phần tử có giá trị nhỏ hơn 10 đã bị xóa.
```
    const numbers = [5, 7, 10, 12, 15, 20];
    function isBigEnough(number){
        return number >= 10;
    }
    const filterNumbers = numbers.filter(isBigEnough);
    console.log(filterNumbers);
    //expected output: [10, 12, 15, 20]
```

2. Tìm tất cả các số nguyên tố trong 1 array
 - `[Số nguyên tố]: là số chía hết cho 1 và chính nó`
```
    functin isPrime(number){
        for(let i = 2; i < number; i++){
            if (number % i === 0) {
                return false;
            }
        }
        return number > 1;
    }
    
    const number = [-3, -1, 0, 1, 2, 3, 4, 5, 7, 9, 10, 13]; 
    const filterPrime = number.filter(isPrime);
    console.log(filterPrime);
    // expected output: [2, 3, 5, 7, 13]   
```

3. Filter các mục nhập không hợp lệ từ JSON

```
    const arr = [{id: 15}, {id: -1}, {id: 0}, {id: 1}, {}, {id: null}, {id: NaN}, {id: "undefined"}];
    function filterByID(item){
        // C1: 
        return Number.isFinite(item.id) && item.id;
        // C2:
        if (Number.isFinite(item.id) && item.id){
            return true;
        }
        return false;
        //C3
        if (Number.isFinite(item.id)){
            if (item.id){
                return true;
            }
        }
        return false;
        // C4
        return item.id && item.id !== "undefined";
        // C5
        return Number.isFinite(item.id) && item.id ? true : false;
    };
    const arrByID = arr.filter(filterByID);
    // expected output:  [{id:15}, {id:1}]
```

4. Searching in array
```
    const fruits = ["apple", "banana", "grapes", "mango", "orange"];
    
    function filterItems(array, query){
        return array.filter((fruit) => fruit.toLowerCase().includes(query.toLowerCase()));
    }
    
    const filterArray = filterItems(fruits, "an");
    // expected output: ['banana', 'mango', 'orange'];
    
```

5. Calling filter() on non-array objects
```
    const arrayLike = {
        0: "a",
        1: "b",
        2: "c",
        length: 3
    }
    console.log(Array.prototype.filter.call(arrayLike, (x) => x);
    // expected output: ["a", "b", "c"];
```