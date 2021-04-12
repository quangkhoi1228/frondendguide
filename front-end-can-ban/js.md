# JS

## JS là gì?

JavaScript là ngôn ngữ lập trình phổ biến nhất thế giới

JavaScript là ngôn ngữ lập trình cho website

JavaScript rất dễ để học

## Thêm JS vào trang

Tham khảo HTML javascript: [Cách thêm JavaScript](https://app.gitbook.com/@quangkhoi1228/s/front-end-guide/~/drafts/-MY3PD3alRQ69Ywet0ra/front-end-can-ban/html#html-javascript)

## Biến

biến được khai báo bằng từ khóa `var`

### Tổng quan

```javascript
//khai báo biến
var x = 5;
var y = 6;
var z = x + y;

//nhiều biến 1 dòng
var person = "John Doe", carName = "Volvo", price = 200;

//nhiều biến nhiều dòng
var person = "John Doe",
carName = "Volvo",
price = 200;

//Giá trị mặc định của biến là undefined
var carName;
//undefined

//khai báo lại biến không làm mất dữ liệu biến
var carName = "Volvo";
var carName;
//Volvo
```

### 

### Sử dụng **let** và **const** \(ES6\)

Trước 2015 để khai báo biến trong JS chỉ có duy nhất từ khóa `var` 

Từ [JavaScript \(ES6\)](https://www.w3schools.com/js/js_es6.asp) phiên bản 2015 JS chấp nhận từ khóa `const`  để khai báo 1 biến không thể khai báo lại và `let` để hạn chế phạm vi hoạt động của biến.

### Kiểu dữ liệu

Biến JS có thể chứa các dữ liệu kiểu String, Number, Object vân vân

```javascript
var length = 16;                               // Number
var lastName = "Johnson";                      // String
var x = {firstName:"John", lastName:"Doe"};   //object
```

## Hàm

Một hàm JS là một khối code được thiết kế để thực thi 1 tác vụ nào đó

Một hàm JS được thực thi khi nó được gọi

### Cú pháp

```javascript
function name(parameter1, parameter2, parameter3) {
  // code to be executed
}

//example
function myFunction(p1, p2) {
  return p1 * p2; 
} 
```

### return giá trị

Khi hàm thực thi tới từ khóa `return`  hàm sẽ dừng và trả giá trị về cho nơi gọi nó

```javascript
var x = myFunction(4, 3);   // Function is called, return value will end up in x

function myFunction(a, b) {
  return a * b;             // Function returns the product of a and b
}
//12
```



##  
