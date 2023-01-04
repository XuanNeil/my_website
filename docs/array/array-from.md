---
sidebar_position: 1
---

# Array.from() Method

- `Array.from()` là 1 phương thức tĩnh tạo một array mới, được `shallow-copied` từ 1 object có thể lặp lại hoặc array-like object.

```jsx title="JavaScript Demo: Array.from()"
console.log(Array.from('foo'));
// expected output: Array ["f", "o", "o"]

console.log(Array.from([1, 2, 3], x => x + x));
// expected output: Array [2, 4, 6]
```

## Syntax
```
Array.from(arrayLike)

// Arrow function
Array.from(arrayLike, (element) => { /* … */ })
Array.from(arrayLike, (element, index) => { /* … */ })

// Mapping function
Array.from(arrayLike, mapFn)
Array.from(arrayLike, mapFn, thisArg)

// Inline mapping function
Array.from(arrayLike, function (element) { /* … */ })
Array.from(arrayLike, function (element, index) { /* … */ })
Array.from(arrayLike, function (element) { /* … */ }, thisArg)
Array.from(arrayLike, function (element, index) { /* … */ }, thisArg)

```

## Parameters
`arrayLike`
- 1 đối tượng có thể lặp lại hoặc array-like để chuyển đồi thành 1 array.
- `mapFn` (optional):
    - Map function để gọi mọi phần tử của array. Nếu được cung cấp, mọi giá trị được thêm vào array trước tiên sẽ được chuyển qua hàm này và thay vào đó, giá trị trả về của mapFn sẽ được thêm vào array.
    - Hàm được gọi với các đối số sau:
    - `element`: Phần tử hiện tại đang được xử lý trong array.
    - `index`: Index của phần tử hiện tại đang được xử lý trong array.
-`thisArg` `Optional`: Giá trị được sử dụng như `this` khi thực thi `mapFn`.

## Return value
- 1 array mới instance.

## Examples
1. Array from a string
```
Array.from("foo");
// [ "f", "o", "o" ]
```

2. Array from a Set
```
const set = new Set(["foo", "bar", "baz", "foo"]);
Array.from(set);
// [ "foo", "bar", "baz" ]

```

3. Array from a Map
```
const map = new Map([
  [1, 2],
  [2, 4],
  [4, 8],
]);
Array.from(map);
// [[1, 2], [2, 4], [4, 8]]

const mapper = new Map([
  ["1", "a"],
  ["2", "b"],
]);
Array.from(mapper.values());
// ['a', 'b'];

Array.from(mapper.keys());
// ['1', '2'];

```

4. Sequence generator (range)
```
// Sequence generator function (commonly referred to as "range", e.g. Clojure, PHP, etc.)
const range = (start, stop, step) =>
  Array.from({ length: (stop - start) / step + 1 }, (_, i) => start + i * step);

// Generate numbers range 0..4
range(0, 4, 1);
// [0, 1, 2, 3, 4]

// Generate numbers range 1..10 with step of 2
range(1, 10, 2);
// [1, 3, 5, 7, 9]

// Generate the alphabet using Array.from making use of it being ordered as a sequence
range("A".charCodeAt(0), "Z".charCodeAt(0), 1).map((x) =>
  String.fromCharCode(x),
);
// ["A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z"]

```