---
layout: post
title:  "Tìm hiểu bước đầu về ReactJS."
date:   2020-09-10 10:11:10 +0530
tags: JS Javascript ReactJS React
image: post_5/reactjs.png
---

## Lời nói đầu
Hi guys, lại là mình đây. Mình đang bắt đầu học React, cho nên có tìm hiểu và viết cái blog này để vừa học cũng như chia sẽ cho mọi người. Đọc cho vui và có thể giúp ích phần nào đó cho những bạn mới học React như mình cũng nên, còn không thì có gì sai sót bỏ qua nhé =))

React đang nhanh chóng trở thành bộ thư viện JavaScript phổ biến, so với một số lượng không ít các thư viện và framework JavaScript hiện nay thì React nổi trội ở tính đơn giản và hiệu quả và thích hợp để build các ứng dụng UI phức tạp.

Vậy React là gì, sử dụng như thế nào và tại sao lại sử dụng react? Trong phạm vi bài viết này chúng ta sẽ cùng nhau tìm hiểu về những điều đó nhé :D

Bài có tham khảo, tổng hợp từ bài viết khác và viết chỉ ngắn gọc, chưa tìm hiểu sâu. Nếu các bạn muốn tìm hiểu thêm thì vào [docs](https://reactjs.org/docs) của React đọc thêm nhé!

## Tìm hiểu về ReactJS

### Vậy thì React là gì?

`
React is a declarative, efficient, and flexible JavaScript library for building user interfaces. It lets you compose complex UIs from small and isolated pieces of code called “components".
`

**React** là một thư viện JavaScript linh hoạt, hiệu quả để xây dựng các UI component viết bằng HTML, CSS và JavaScript. Nó cho phép lập trình viên chúng ta xây dựng các UI component phức tạp từ những đoạn code nhỏ và độc lập

Note:

React không phải là một MVC framework như những framework khác, nó chỉ là thư viện của Facebook giúp render ra phần view. Vì thế React sẽ không có phần Model và Controller, mà phải kết hợp với các thư viện khác. React cũng sẽ không có 2-way binding hay là Ajax, ...

React cho phép bạn viết JavaScript sử dụng cú pháp được định nghĩa trong tiêu chuẩn ECMAScript 6 (ES6 hay ECMAScript 2015), tuy nhiên một số trình duyệt chưa chấp nhận phiên bản mới này. Babel là một JavaScript compiler giúp biên dịch mã JavaScript viết theo chuẩn ECMAScript 6 về ECMAScript 5.

### JSX

`
JSX là 1 phần mở rộng cú pháp giống như XML cho EMCAScript. Nó được khuyến khích dùng trong React.
`

**JSX = Javascript + XML**

Ưu điểm mà JSX mang lại:

- Nhanh hơn nhờ việc thực hiện tối ưu hóa trong khi biên dịch mã thành Javascript.
- An toàn và hầu hết các lỗi có thể bị bắt trong quá trình biên dịch.
- Giúp bạn viết template dễ dàng và nhanh hơn.

Sử dụng JSX:

- Cú pháp tương đối giống với HTML và có khả năng sử dụng biểu thức logic vào JSX

```javascript
class App extends React.Component {
   render() {
      return (
         <div>
            <h1>2 + 3 = { 2 + 3 }</h1>
         </div>
      );
   }
}
export default App;
```

- Định style sử dụng cú pháp camelCase và tự động thêm px sau giá trị là số của các phần tử

```javascript
class App extends React.Component {
   render() {
      let myStyle = {
         fontSize: 100,
         color: '#FF0000'
      }
      return (
         <div>
            <h1 style = { myStyle }>Header</h1>
         </div>
      );
   }
}
export default App;
```

- Viết comment đặt trong cặp dấu { }
- Tên commponent bắt đầu bằng chữ hoa Uppercase, sử dụng className và htmlFor thay vì class và for.
- JSX đại diện cho các đối tượng: 2 ví dụ sau đây đều cho kết quả tương tự nhau

```javascript
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```

```javascript
const element = React.createElement(
  'h1',
  {
      className: 'greeting'
  },
  'Hello, world!'
);
```

### Component
```
Các component cho phép bạn tách giao diện người dùng thành các thành phần độc lập, có thể tái sử dụng.
```

Component giống như các hàm Javascript. Chúng chấp nhận đầu vào 1 cách tùy ý (props) và trả về phần tử React xuất hiện trên màn hình.

#### Tạo component

Có 2 cách để khởi tạo component là dùng hàm hoặc dùng định nghĩa class.

```javascript
// Use function
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

// Or user class
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

Component do người dùng định nghĩa

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="ManhLD" />;
ReactDOM.render(
  element,
  document.getElementById('app')
);
```

- Gọi ReactDOM.render với phần tử <Welcome name="ManhLD" />
- React gọi component Welcome với {name: 'ManhLD'} như là props
- Component Welcome trả về kết quả<h1>Hello, ManhLD</h1>
- React DOM cập nhật DOM

### Props và State

Props và state là 2 kiểu dữ liệu trong React. State chỉ được thay đổi bên trong bản thân component. Props không bị kiểm soát bởi bản thân component.

#### Props

Props là viết tắt của properties. Chúng là các giá trị đơn hoặc các đối tượng có chứa 1 tập hợp các giá trị được chuyển đến Component. Nó sử dụng quy ước đặt tên tương tự như các thuộc tính của thẻ HTML.

Props là cách để các component giao tiếp với nhau. Props được truyền từ component cha.

Props chỉ để đọc. Cho dù bạn khai báo component dưới dạng hàm hay class thì nó vẫn không bao giờ có thể sửa đổi props của chính nó.

```javascript
let text = 'React App';

class Form extends React.Component {
    render () {
        return (
            <div>
                <h3>
                    { this.props.text }
                </h3>
            </div>
        );
    }
}

class App extends React.Component {
    render () {
        return (
            <div>
                <h1>
                    Welcome to my app
                </h1>
                <Form text={ this.props.text } />
            </div>
        );
    }
}

ReactDOM.render(
    <App text={ text } />,
    document.getElementById('root')
);
````

- props được truyền vào trong App trong phương thức React.render()
- App component truy xuất biến text thông qua lời gọi this.props.text
- Form component hiển thị dữ liệu vào thẻ <h3>

#### State

Khác với props là bất biến thì state có thể thay đổi. State được quản lý chỉ bởi duy nhất 1 component, nó cũng không thể truyền xuống cho component con.

```javascript
class SearchBar extends React.Component {
    constructor(props) {
        super(props);
        this.state = { term: '' };
    }
    render() {
        return (
            <div className="search-bar">
                <input
                    value={ this.state.term }
                    onChange={(event) => this.onInputChange(event.target.value)} />
                <p>
                    { this.state.term }
                </p>
            </div>
        );
    }
    onInputChange(term) {
        this.setState({ term });
    }
}

ReactDOM.render(
    <SearchBar />,
    document.getElementById('root')
);
```

#### Lifecycle

- **componentDidMount**: thực hiện chỉ 1 lần sau khi render ở phía client. Đây là nơi yêu cầu AJAX, cập nhật DOM hoặc cập nhật trạng thái nên xảy ra.
- **shouldComponentUpdate**: trả về giá trị true hoặc false. Nó xác định xem các component có được cập nhật hay không. Giá trị mặc định của nó là true. Nếu bạn chắc chắn không muốn component được render lại sau khi state hoặc props được cập nhật thì đặt giá trị cho nó là false.
- **componentDidUpdate**: được gọi ngay sau khi render.
- **componentWillUnmount**: gọi sau khi component được hủy khỏi DOM.

### Lists & Keys

Key rất hữu ích khi làm việc với các component được tạo động hoặc khi danh sách của bạn bị thay đổi bởi người dùng. Việc đặt giá trị key sẽ giữ cho các component được xác định là duy nhất sau khi thay đổi.

```javascript
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
```

Không nên sử dụng các chỉ mục cho các khóa nếu thứ tự các mục có thể thay đổi. Điều này có thể tác động không tốt đến hiệu suất và gây ra các vấn đề với state của component.

Lưu ý: Key chỉ có ý nghĩa trong hoàn cảnh mảng xung quanh các phần tử cần đánh key

## Cuối cùng

Vì mới tìm hiểu về React nên nội dung chưa được chi tiết lắm. Mình sẽ tìm hiểu thêm và cho ra những bài viết chất lượng hơn. Rất cảm ơn các bạn đã đọc ^^

Thank for reading!
