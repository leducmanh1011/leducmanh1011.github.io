---
layout: post
title:  "Push notification đến Web client, iOS, Android sử dụng Firebase Cloud Messaging (FCM)."
date:   2020-07-10 10:11:10 +0530
tags: ROR FCM Firebase Notification
image: post_3/fcm.png
---
i love you 3000 ❤️❤️❤️❤️❤️❤️❤️❤️❤️❤️❤️❤️❤️❤️ <br>

## Lời nói đầu

Mỗi khi dùng các app như facebook, tiki, momo các bạn thường thấy nhưng notification push về. Các bạn có bao giờ tò mò làm sao để có thể xây dựng được chức push như vậy chưa?. Vậy thì trong bài viết này mình sẽ giới thiệu và hướng các bạn làm điều đó.

Push notification là một tính năng rất phổ biến trong việc phát triển app web hoặc app di động hiện nay. Có rất nhiều cơ chế để gửi push notification, trong bài viết này chúng ta sẽ tìm hiểu về Firebase Cloud Messaging (FCM), 1 dịch vụ hoàn toàn miễn phí của Google.

![FCM]({{ site.baseurl }}/images/post_3/fcm.png)

## FCM hoạt động như thế nào?

Mình sẽ giải thích đơn giản theo ý hiểu của mình:

- Khi thiết bị của user cài app hoặc truy cập web client thì sẽ gửi yêu cầu lên Firebase Cloud Server để xin token, tạm gọi là device token.
- Firebase Server sau khi nhận request sẽ trả về 1 token, token này là duy nhất cho mỗi thiết bị.
- Sau khi có token service của server gửi token này + gói tin cần truyền cho Firebase.
- Firebase kiểm tra (check token có hợp lệ, ...) rồi thực hiện gửi đến device đã đăng kí với token đó
- Device khi nhận gói tin được gói thì sẽ có thông báo.

## Các bước thực hiện

### 1. Đăng ký tài khoản

Đầu tiên bạn cần truy cập vào địa chỉ [https://firebase.google.com](https://firebase.google.com) và đăng ký ngay một account.

### 2. Tạo một project mới

Các bạn tạo cho mình một project. Project này sẽ là trung gian nhận/gửi gói tin của các chúng ta. Bấm vào dấu + để add một project mới. Sau khi tạo xong sẽ giống như sau.

![Project]({{ site.baseurl }}/images/post_3/project.png)

Trong Project settings, chuyển sang tab Cloud Messaging, ở đây sẽ có Server key dùng cho các thủ tục credential, cần lưu ý key này.

![Project]({{ site.baseurl }}/images/post_3/fcm-server-key.png)

Key này nên private nhé và tất nhiên hình trên là mình lấy trên mạng thôi :D

### 3. Build client

Cũng trong phần Project settings, chuyển sang Tab General, mục Your apps bạn cần tạo 1 client để test việc nhận thông báo, việc này các bạn sẽ tự làm. Chú ý phần script nhúng vào app sẽ bao gồm các thông số của Project

![Project]({{ site.baseurl }}/images/post_3/generate.png)

Ở trong bài viết này, mình đã build sẵn 1 Web app để test, các bạn có thể follow theo các bước hướng dẫn rất chi tiết trên Firebase để tự build client cho mình

### 4. Sử dụng Ruby on Rails xây dựng một service cho việc gửi thông báo

Sau khi build được client, việc tiếp theo là viết service ở server thôi ✌️ Ở đây ta sẽ dùng Rails. Bắt đầu nào:

Ở server, ta sẽ dùng gem fcm có sẵn:

Trong gemfile

#Gemfile

```ruby
gem "fcm"
```

Chạy lệnh

```ruby
bundle install
```

Ta sẽ tạo 1 service, đặt tên là ``push_notification_service.rb ``

#push_notification_service.rb

```ruby
require "fcm"

class PushNotificationService
  def initialize content = {}, fcm_token = [], platform = "web_client", opts = {}
    @content = content
    @fcm_token = fcm_token
    @platform = platform
    @opts = opts
  end

  def perform
    fcm = FCM.new(ENV["FCM_SEVER_KEY"])

    options = if @platform == Settings.fcm.platform.web
                web_payload
              elsif @platform == Settings.fcm.platform.ios
                ios_payload
              elsif = @platform == Settings.fcm.platform.android
                android_payload
              end

    options.merge!(options: @opts) if @opts.present?
    fcm.send(@fcm_token, options) if @fcm_token.present?
  end
```

Bạn nhớ require thư viện "fcm" vào nhé! Mình giải thích qua như sau:

- content: nội dung notification gửi đi
- fcm_token: device token nhận notification
- platform: để check gửi tới Web client, iOS hay Android
- opts: các option thêm

### Send notification

Đầu tiên cần khởi tạo một class FCM mới với server key mình đã nói ở bước 2 (nên cho vào biến môi trường)

```ruby
fcm = FCM.new(ENV["FCM_SEVER_KEY"])
```

Notification gửi đi sẽ có dạng như sau:

```ruby
def web_payload
    {
      notification: {
        title: @content[:title],
        body: @content[:body],
        icon: @content[:icon],
        image: @content[:image],
        type: @content[:type],
        notificationId: @content[:notification_id]
      }
    }
  end
```

Gem fcm đã cung cấp sẵn 1 hàm send rất tiện

```ruby
fcm.send(@fcm_token, options) if @fcm_token.present?
```

Hàm này có 2 tham số:

- token là một array chứa device token, có thể gửi cho một hoặc tới nhiều device bằng cách truyền vào một array tokens up to lên đến 1000.
- options là cục data mình đã xử lý ở trên.

Ok rồi bây giờ test thử xem nào :))))

## Testing

Lấy token bằng cách truy cập web client

![Project]({{ site.baseurl }}/images/post_3/web_client.png)

Khởi động rails c

```ruby
rails c
```

Sau đó gán data cho các biến như sau:

```ruby
content = {
  title: "Manh say hello",
  body: "Push notification with FCM"
}

fcm_token = ["c0dnWjVyUryBFVKE7XHb8K:APA91bEN0kR9SSi1pw82fIe9TQUoyglfcS3Ho-qPpRpFGy-bdS3yG_UKXcvipdK6ocnn9NRW7UTAUMXTsNhYdZ2kJbmz7o_4iELQcf-7DuZpuB9BfuAZBgDAv4"]

platform = "web"
```
Và cuối cùng là
```ruby
PushNotificationService.new(content, fcm_token, platform).perform
```
Xem kết quả
```ruby
{:body=>
  "{\"multicast_id\":5245790373052475539,\"success\":1,\"failure\":0,\"canonical_ids\":0,\"results\":[{\"message_id\":\"0:1594827494666930%2fd9afcdf9fd7ecd\"}]}",
 :headers=>
  {"content-type"=>"application/json; charset=UTF-8",
   "date"=>"Wed, 15 Jul 2020 15:38:14 GMT",
   "expires"=>"Wed, 15 Jul 2020 15:38:14 GMT",
   "cache-control"=>"private, max-age=0",
   "x-content-type-options"=>"nosniff",
   "x-frame-options"=>"SAMEORIGIN",
   "content-security-policy"=>"frame-ancestors 'self'",
   "x-xss-protection"=>"1; mode=block",
   "server"=>"GSE",
   "alt-svc"=>
    "h3-29=\":443\"; ma=2592000,h3-27=\":443\"; ma=2592000,h3-25=\":443\"; ma=2592000,h3-T050=\":443\"; ma=2592000,h3-Q050=\":443\"; ma=2592000,h3-Q046=\":443\"; ma=2592000,h3-Q043=\":443\"; ma=2592000,quic=\":443\"; ma=2592000; v=\"46,43\"",
   "transfer-encoding"=>"chunked"},
 :status_code=>200,
 :response=>"success",
 :canonical_ids=>[],
 :not_registered_ids=>[]}
```
Vậy là đã push thành công, các bạn để ý status code là 200, response success.

Khi đó ngay trên browser sẽ xuất hiện một notification. Vậy là xong chức năng rồi đó ^^

![Project]({{ site.baseurl }}/images/post_3/notification.png)


## Cuối cùng

Cảm ơn vì các bạn đã đọc đến đây, xin chào và hẹn gặp lại trong số tiếp theo. ❤️ 🙇

source: Viblo, Google, Firebase docs
