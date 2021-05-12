---
layout: post
title:  "Thư viện Lodash và các hàm xử lý cơ bản thường dùng."
date:   2020-08-10 10:11:10 +0530
tags: JS Javascript Lodash
image: post_4/lodash.png
---
Không đọc hay đọc không hay, không vui cũng đừng buông lời cay đắng :v

## Lời nói đầu

Hi các bạn, vừa rồi mình vừa tham gia phát triển tính năng mới của một dự án. Và dự án đó áp dụng thư viện khá hay mà mình muốn chia sẽ trong bài viết này. Đó là Lodash! Hãy cùng mình tìm hiểu thư viện Lodash là gì? Và các fuction cơ bản của nó nhé.

Bắt đầu thôiiiiiiiiiii

## Giới thiệu về thư viện Lodash

Lodash là phiên bản mở rộng hơn của thư viện underscore, với nhiều chức năng và cho hiệu năng cao hơn. Các chức năng của Lodash được chia ra làm các nhóm: nhóm xử lý Array, nhóm xử lý Object, nhóm xử lý Date, Function, Lang, Math, Number,…

Vì phạm vi có hạn nên trong bài viết này mình chỉ giới thiệu các fuction cơ bản hay dùng. Các bạn có thể tìm hiểu thêm [ở đây](https://lodash.com/docs).

## Các fuction cơ bản của thư viện Lodash

### Các functions xử lý String

`.camelCase`: nhận argument là string và trả về string đã format theo dạng camel

```javascript
_.camelCase('Duc Manh');
// => 'ducManh'

_.camelCase('--duc-manh--');
// => 'ducManh'
```

`_.split`: tách 1 string theo mẫu (pattern) hay theo ký tự về thành mảng các ký tự.

```javascript
.split('a-b-c', '-', 2);
// => ['a', 'b']
```

`_.pad`, `_.padLeft`, `_.padRight`: Canh giữa, trái, phải string bằng cách thêm khoảng trắng vào string.

`_.trim`, `_.trimEnd`, `_.trimStart`: loại bỏ khoảng trắng (white space) hoặc ký tự xác định nào đó ở 2 đầu, ở cuối hoặc ở đầu.

```javascript
_.trim('  ldm  ');
// => 'ldm'

_.trimStart('  ldm  ');
// => 'ldm  '

_.trimEnd('-_-ldm-_-', '_-');
// => '-_-ldm'
```

### Các functions xử lý Array

`_.concat`: Tạo một array mới bằng cách nối các tham số lại với nhau.

```javascript
var array = [1];
var other = _.concat(array, 2, [3], [[4]]);

console.log(other);
// => [1, 2, 3, [4]]

```

`_.difference(array, [values])`: lọc ra những phần tử có mặt trong array mà không có mặt trong các đối số còn lại (values).

```javascript
_.difference([2, 1], [2, 3]);
// => [1]
```

`_.findIndex`: tìm kiếm phần tử trong mảng và trả về index của phần tử đó trong mảng, trả về -1 nếu không tìm thấy.

```javascript
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

_.findIndex(users, function(o) { return o.user == 'barney'; });
// => 0

_.findIndex(users, { 'user': 'fred', 'active': false });
// => 1
```

`_.flatten`, `_.flattenDeep`: convert mảng n chiều về (n – 1) chiều với `_.flatten` và 1 chiều với `_.flattenDeep`

```javascript
_.flatten([1, [2, [3, [4]], 5]]);
// => [1, 2, [3, [4]], 5]

_.flattenDeep([1, [2, [3, [4]], 5]]);
// => [1, 2, 3, 4, 5]

```

### Các functions xử lý Object

`_.keys`: Trả về tên toàn bộ key của 1 object `_.values`: Trả về tên toàn bộ value của 1 object.

```javascript
var object = { 'user': 'fred', 'age': 40 };
_.keys(object);
// => ["user", "age"]

_.values(object);
// => ["fred", 40]
```

`_.pick`: Chỉ lấy 1 thuộc tính của object.

`_.omit`: Bỏ 1 thuộc tính của object, lấy toàn bộ những thuộc tính còn lại.


```javascript
var object = { 'user': 'fred', 'age': 40 };

_.pick(object, 'user');
// => { 'user': 'fred' }

_.omit(object, 'age');
// => { 'user': 'fred' }
```

`_.invert`: Đảo ngược key-value của 1 object

```javascript
var object = { 'a': 1, 'b': 2, 'c': 1 };

_.invert(object);
// => { '1': 'c', '2': 'b' }
```

### Một số ultility function

`_.isNil`, `_.isNull`, `_.isUndefined`, `_.isNumber`, `_.isObject`, `_.isInteger` : là các function kiểm tra 1 giá trị có null hay undefined hay có phải là kiểu số hay object hay không

```javascript
_.isNull(null);
// → true

_.isFunction(_);
// → true
_.isFunction(/abc/);
// → false

_.isNumber(8.4);
// → true
_.isNumber(NaN);
// → true
_.isNumber('8.4');
// → false

_.isObject({});
// → true
_.isObject([1, 2, 3]);
// → true
_.isObject(1);
// → false
```

`_.isEqual`: function này so sánh 2 array, hoặc 2 object. Function này sử dung `deep comparision`, so sánh từng field của 2 object, hoặc từng phần tử của 2 array.

```javascript
var object = { 'a': 1 };
var other = { 'a': 1 };

_.isEqual(object, other);
// => true

object === other;
// => false
```

`_.isEmpty`: Checks if value is an empty object, collection, map, or set. Kiểm tra 1 giá trị có là object rỗng hay không. Một object được coi là rỗng nếu nó không có thuộc tính enumerable string keyed.

```javascript
_.isEmpty(null);
// => true

_.isEmpty(true);
// => true

_.isEmpty(1);
// => true

_.isEmpty([1, 2, 3]);
// => false

_.isEmpty({ 'a': 1 });
// => false
```

## Cuối cùng

Bài viết của mình đến đây là kết thúc. Các bạn thử dùng thư viện này xem nhé, trong quá trình sử dụng các bạn có thể tìm hiểu thêm.

Hy vọng giúp các bạn code JS xịn xò hơn ^^

Thanks for reading. <3

Sources: Viblo, TopDev, Lodash Documentation, Toidicodedao
