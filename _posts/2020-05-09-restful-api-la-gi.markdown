---
layout: post
title:  "RESTful API là gì ?"
date:   2020-05-09 11:43:36 +0530
categories: RESTful API
---
Sự quan trọng của API trong các ứng dụng ngày nay là điều ko thể bàn cãi. Một ứng dụng mà không có API thì như một cỗ máy tính không kết nối internet vậy. Và như một điều hiển nhiên, mọi thứ sau khi phát triển một thời gian sẽ hình thành những chuẩn mực chung và đối với API, nó chính là RESTful

Dù hiện tại cũng có rất nhiều bài viết về RESTful API nhưng mình vẫn muốn viết về vấn đề này để đóng góp một phần ý kiến trong việc thiết kế RESTful API. Bài viết này cũng là kiến thức mình tự tìm hiểu, tham khảo qua nhiều nguồn, nếu mình có sai sót gì, mong các bạn hãy góp ý thêm giúp mình. Thanks you 😀

## Lời nói đầu
Có thể nói nguyên lí REST và cấu trúc dữ liệu RESTful được biết đến rộng rãi trong giới lập trình web nói chung và lập trình ứng dụng nói riêng.

Có thể nói bản thân REST không phải là một loại công nghệ. Nó là phương thức tạo API với nguyên lý tổ chức nhất định. Những nguyên lý này nhằm hướng dẫn lập trình viên tạo môi trường xử lý API request được toàn diện.

Để hiểu rõ hơn về RESTful API ta sẽ đi lần lượt giải thích các khái niệm nhở API, REST hay RESTful.

## RESTful API là gì?
Các lập trình viên web thường nhắc đến nguyên lý REST và cấu trúc dữ liệu RESTFUL bởi nó là một phần rất quan trọng trong sự phát triển của các ứng dụng web. Vậy RESTFUL API là gì ? Để hiểu rõ hơn chúng ta cùng nhau tìm hiểu nhé.

RESTful API là một tiêu chuẩn dùng trong việc thiết kế API cho các ứng dụng web (thiết kế Web services) để tiện cho việc quản lý các resource. Nó chú trọng vào tài nguyên hệ thống (tệp văn bản, ảnh, âm thanh, video, hoặc dữ liệu động…), bao gồm các trạng thái tài nguyên được định dạng và được truyền tải qua HTTP.

![RESTful API la gi](/assets/images/6ee4b71e-e2db-46b1-b7f1-da37ce13b861.png)

## Các thành phần của nó

API (Application Programming Interface) là một tập các quy tắc và cơ chế mà theo đó, một ứng dụng hay một thành phần sẽ tương tác với một ứng dụng hay thành phần khác. API có thể trả về dữ liệu mà bạn cần cho ứng dụng của mình ở những kiểu dữ liệu phổ biến như JSON hay XML.

REST (REpresentational State** T**ransfer) là một dạng chuyển đổi cấu trúc dữ liệu, một kiểu kiến trúc để viết API. Nó sử dụng phương thức HTTP đơn giản để tạo cho giao tiếp giữa các máy. Vì vậy, thay vì sử dụng một URL cho việc xử lý một số thông tin người dùng, REST gửi một yêu cầu HTTP như GET, POST, DELETE, vv đến một URL để xử lý dữ liệu.

RESTful API là một tiêu chuẩn dùng trong việc thiết kế các API cho các ứng dụng web để quản lý các resource. RESTful là một trong những kiểu thiết kế API được sử dụng phổ biến ngày nay để cho các ứng dụng (web, mobile…) khác nhau giao tiếp với nhau.

Chức năng quan trọng nhất của REST là quy định cách sử dụng các HTTP method (như GET, POST, PUT, DELETE…) và cách định dạng các URL cho ứng dụng web để quản các resource. RESTful không quy định logic code ứng dụng và không giới hạn bởi ngôn ngữ lập trình ứng dụng, bất kỳ ngôn ngữ hoặc framework nào cũng có thể sử dụng để thiết kế một RESTful API.

## RESTful API hoạt động như thế nào?

Sau khi chúng ta biết được RESTful API là gì thì trong phần này chúng ta cùng tìm hiểu nguyên lý hoạt động của nó nhé. Giống như các giao thức truyền thông hay cấu trúc dữ liệu khác. Để hiểu được bản chất vấn đề thì trước hết cần phải hiểu nguyên lý hoạt động của nó.

![RESTful API hoat dong nhu the nao](/assets/images/c502a773-8ac5-4f33-bbf8-fa56916b70dc.png)

REST hoạt động chủ yếu dựa vào giao thức HTTP. Các hoạt động cơ bản nêu trên sẽ sử dụng những phương thức HTTP riêng.

- GET (SELECT): Trả về một Resource hoặc một danh sách Resource.
- POST (CREATE): Tạo mới một Resource.
- PUT (UPDATE): Cập nhật thông tin cho Resource.
- DELETE (DELETE): Xoá một Resource.

Những phương thức hay hoạt động này thường được gọi là CRUD tương ứng với Create, Read, Update, Delete – Tạo, Đọc, Sửa, Xóa.

Hiện tại đa số lập trình viên viết RESTful API giờ đây đều chọn JSON là format chính thức nhưng cũng có nhiều người chọn XML làm format, nói chung dùng thế nào cũng được miễn tiện và nhanh.

## Authentication request và cấu trúc dữ liệu trả về

RESTful API không sử dụng session và cookie, nó sử dụng một access_token với mỗi request. Bạn có thể tìm hiểu JWT (JsonWebToken) để biết rõ hơn. Mình sẽ làm một bài về JWT trong phần sau nữa 😃) Dữ liệu trả về thường có cấu trúc như sau:

```javascript
{
    "status_code": 200,
    "data": [
        {
            "name": "ManhLD",
            "email": "manhld@example.com",
            "ny": "not found"
        },
        {
            "name": "Ahri",
            "email": "ahriKDA@lmht.com",
            "ny": "Ezreal"
        }
    ],
    error_messages: ""
}
```
Ở trên là ví dụ về cấu trúc trả về của api get một list users trong hệ thống.

## Status code

Khi chúng ta request một API nào đó thường thì sẽ có vài status code để nhận biết sau:

- 200 OK – Trả về thành công cho những phương thức GET, PUT, PATCH hoặc DELETE.
- 201 Created – Trả về khi một Resouce vừa được tạo thành công.
- 204 No Content – Trả về khi Resource xoá thành công.
- 304 Not Modified – Client có thể sử dụng dữ liệu cache.
- 400 Bad Request – Request không hợp lệ
- 401 Unauthorized – Request cần có auth.
- 403 Forbidden – bị từ chối không cho phép.
- 404 Not Found – Không tìm thấy resource từ URI
- 405 Method Not Allowed – Phương thức không cho phép với user hiện tại.
- 410 Gone – Resource không còn tồn tại, Version cũ đã không còn hỗ trợ.
- 415 Unsupported Media Type – Không hỗ trợ kiểu Resource này.
- 422 Unprocessable Entity – Dữ liệu không được xác thực
- 429 Too Many Requests – Request bị từ chối do bị giới hạn

Trong Ruby on Rails có thể sử dụng symbol status code hoặc 3 chữ số integer

## Quản lí version của api

Khi thiết api cho app ios hay client side, chúng ta nên đặt version cho các api. Ví dụ như endpoint sau: api/v1/users

Điều này sẽ giúp hệ thống sau khi nâng cấp lên version mới vẫn hộ trợ các api của version cũ, cũng như giúp việc bảo trì, sửa chữa dễ dàng hơn.

## Ưu điểm của RESTFUL API là gì ?

Như trình bày ở trên, việc sử dụng RESTFUL API mang lại những hiệu quả nhất định cho các lập trình viên. Vậy những lợi ích nó mang lại là gì ? So với các phương pháp khác nó sẽ có điểm gì vượt trội

![RESTful API hoat dong nhu the nao](/assets/images/ab5539d0-1b5b-456f-a204-290cf7f96705.png)

Một số ưu điểm chính khi sử dụng RESTFUL API là:

Giúp cho ứng dụng rõ ràng hơn
REST URL đại diện cho resource chứ không phải hành động
Dữ liệu được trả về với nhiều định dạng khác nhau như: xml, html, json….
Code đơn giản và ngắn gọn
REST chú trọng vào tài nguyên của hệ thống

Những trang web ngày nay thường sử dụng REST API để cho phép kết nối đến dữ liệu của họ. Trong đó, facebook cũng cung cấp các REST API để giúp các ứng dụng bên ngoài kết nối đến dữ liệu của họ

## Cuối cùng

Cảm ơn vì các bạn đã đọc đến đây, hi vọng sẽ giúp ít cho các bạn mới tìm hiểu về RESTful API. Trong bài tiếp theo, mình sẽ build một app RESTful API với Ruby on Rails, hẹn gặp lại các bạn trong lần tới. Một lần nữa cảm ơn các bạn ❤️ 🙇

source: Viblo, Google, Topdev, Medium
