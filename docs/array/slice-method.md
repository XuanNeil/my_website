---
sidebar_position: 1
---

# Slice Method

- Phương thức `slice()` trả về một `shallow copy` của một phần của mảng thành một đối tượng mảng mới được chọn `start` đến `end` (không bao gồm `end`). Trong đó `start` và `end` biểu thị index của của các phần tử trong mảng đó. `slice()` không làm thay đổi mảng ban đầu.

```jsx title="JavaScript Demo: Array.slice()"
const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];

console.log(animals.slice(2)); 
// expected output: ['camel', 'duck', 'elephant']

console.log(animals.slice(2, 4));
// expected output: ['camel', 'duck']

console.log(animals.slice(1, 5));
// expected output: ['binson', 'camel', 'duck', 'elephant']

console.log(animals.slice(-2));
// expected output: ['duck', 'elephant']

console.log(animals.slice(2, -1));
// expected output: ['camel', 'duck']

console.log(animals.slice());
// expected output: ['ant', 'bison', 'camel', 'duck', 'elephant']
```

## Syntax
```
slice()
slice(start)
slice(start, end)
```

## Parameters
`start` `optional`:
- Chỉ mục dựa trên số 0 để bắt đầu trích xuất, được chuyển thành số nguyên.
    - Chỉ mục âm đếm ngược từ cuối mảng - nếu start < 0, start + array.length đươc sử dụng.
    - Nếu start < -array.length, hoặc `start` bị bỏ qua, 0 được sử dụng.
    - Nếu start >= array.length, không có gì đươc trích xuất.
`end` `optional`:
- Chỉ số dựa trên số 0 để kết thúc quá trình trích xuất, được chuyển đổi thành số nguyên. `slice()` trích xuất tối đa nhưng không bao gồm `end`.
    - Chỉ số âm được đếm ngược từ cuối mảng - nếu `end` < 0, start + array.length được sử dụng.
    - Nếu end < -array.length, 0 được sử dụng.
    - Nếu end >= array.length hoặc end được bỏ qua, array.length được sử dụng
      - Nếu end được định trước `start` sau khi chuẩn hóa, không có gì được trính xuất.
    

## Return value
- Một mảng mới chứa các phần tử được trích xuất.
