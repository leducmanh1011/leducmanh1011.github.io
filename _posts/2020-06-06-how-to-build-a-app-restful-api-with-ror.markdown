---
layout: post
title:  "How to build a app RESTful API with Ruby on Rails?"
date:   2020-06-06 19:03:36 +0530
image:  post_2/restful-json-api-in-ruby-on-rails.jpg
tags: RESTful API ROR Ruby
---
Hi các bạn, ở bài viết trước mình đã giới thiệt về RESTful API là gì rồi, hôm trước thì mình cũng được tham gia một buổi sharing kiến thức về cách build base api cho dự án. Vậy thì để tiếp nối bài viết trước hôm nay mình sẽ thử xây dựng một app RESTful API với Ruby on Rails.
Bài viết này do quá trình mình làm việc, học tập cộng với kiến thức tham khảo được muốn chia sẽ tới các bạn. Thanks you vì đã xem ❤️

## Lời nói đầu

Ở phiên bản Rails 5, thì gem rails-api đã được tích hợp vào phần core của Rails, vì vậy chúng ta có thể khởi tạo API trong Rails 1 cách dễ dàng và nhanh chóng. Trong bài viết này mình sẽ hướng dẫn cơ bản cho các bạn cách để tạo một API đơn giản, step by step trong Rails 5. Bài viết của mình có những mục sau:

- Chuẩn bị môi trường
- Tạo project API trong rails 5
- Add Rspec vào project
- Xây dựng API
- Serializing API Output
- Enabling CORS
- Phiên bản API
- Authentication API
- Viết document cho API sử dụng Swagger UI

## Chuẩn bị môi trường

Các bạn hãy setup môi trường local nhé, có thể tham khảo list sau của mình. ^^

- Ruby 2.6.3
- Rails 5.2.4.2

## Tạo project API trong rails 5

Đầu tiên, hãy chắc chắn rằng bạn đã setup xong step 1 (chuẩn bị môi trường) cài phiên bản Ruby 2.2.2 trở lên và Rails version 5. :D

Để tạo một API trong rails chỉ cần thêm mode --api phía sau câu lệnh khởi tạo project mới trong Rails.

```ruby
rails new my_project --api
```

Tiếp theo chúng ta chạy lệnh bundle để thực hiện cài đặt các gem mặc định và tiến hành cài đặt database trong thư mục chứa project.

```ruby
bundle install
```

## Add Rspec vào project

Sau khi cài đặt xong project, chúng ta tiến hành cài đặt RSpec để tiến hành việc testing cho API. Lý do tại sao chúng ta tiến hành cài đặt RSpec đầu tiên vì nó sẽ giúp chúng ta tiết kiệm thời gian bằng cách sử dụng RSpec, thì nó sẽ tiến hành tạo tự động các file test controller và model khi chúng ta tạo các model, controller

Để cài đặt, trong Gemfile.

```ruby
group :development, :test do
    gem "rspec-rails"
    gem "factory_girl_rails"
end
```

Sau đó chạy bundle install.

```ruby
bundle install
```

## Xây dựng API

Sau khi add Rpsec vào project thì bước tiếp theo, mình sẽ xây dựng API, cụ thể mình sẽ xây dựng API CRUD my blog. Sử dụng câu lệnh scaffold để khởi tạo nhanh model và controller tương ứng.

```ruby
rails g scaffold MyBlog title content description
```
Nó sẽ sinh ra các file có cấu trúc như sau:

```ruby
invoke  active_record
create    db/migrate/20200607162113_create_my_blogs.rb
create    app/models/my_blog.rb
invoke    test_unit
create      test/models/my_blog_test.rb
create      test/fixtures/my_blogs.yml
invoke  resource_route
route    resources :my_blogs
invoke  scaffold_controller
create    app/controllers/my_blogs_controller.rb
invoke    test_unit
create      test/controllers/my_blogs_controller_test.rb

```
Vì khi khởi tạo project với mode --api nên sẽ không có thư mục view tạo ra, các bạn chú ý.
Tiếp theo các bạn chạy migrate database và run sever nhé.

```ruby
rails db:migrate
rails s
```

API của chúng ta bây giờ đã chạy ở địa chỉ https://localhost:3000. Tuy nhiên đây chưa phải là điều quan trọng nhất, vì tất cả chỉ dừng ở mức cơ bản, và chúng ta còn nhiều việc phải làm để tạo thành một API hoàn chỉnh.

## Serializing API Output Với Fast JSON API

Trong Gemfile add line:

```ruby
gem "fast_jsonapi"
```

Chạy bundle install để cài đặt gem. Sau đó mình sẽ tạo class serializer tương ứng với model, cụ thể ở đây là MyBlog.

```ruby
rails g serializer MyBlog title content description
```

Kết quả:

```ruby
create  app/serializers/my_blog_serializer.rb
```

```ruby
class MyBlogSerializer
  include FastJsonapi::ObjectSerializer
  attributes :title, :content, :description
end
```

Mỗi class serializer sẽ ánh xạ với một model trong database, để có thể chuyển dữ liệu từ database sang kiểu JSON để trả về cho phía front end sử dụng

## Enabling CORS

CORS là viết tắt của Cross-origin resource sharing, là một cơ chế đặc biệt cho phép resource đặt tại một domain này có thể được request từ một domain khác với domain đó, nghĩa là làm sao để có thể gửi và nhận dữ liệu giữa 2 server với nhau. Trong trường hợp bạn muốn public API của mình, thì enable CORS là việc cần làm nếu như bạn không muốn sử dụng JSONP, và hầu hết các trình duyệt hiện nay đều đã hỗ trợ CORS.

Để làm điều đó trong API của chúng ta, thì chỉ việc cài đặt gem rack-cors vào Gemfile:

```ruby
gem "rack-cors"
```

Chạy cập nhật bundle và thêm vào vài dòng code như ở dưới vào file config/application.rb. Ở ví dụ này, nó sẽ cho phép thực hiện các request như GET, POST hoặc bất cứ OPTIONS request nào khác từ bất kì đâu.

```ruby
module YourApp
    class Application < Rails::Application
    # ...
        config.middleware.insert_before 0, "Rack::Cors" do
            allow do
                origins \'*\'
                resource \'*\', headers: :any, :methods => [:get, :post, :options]
            end
        end
    end
end
```

## Quản lí version của api

Ở bài viết trước mình cũng đã nói qua về việc quản lí version cho API rồi.

Điều này sẽ giúp hệ thống sau khi nâng cấp lên version mới vẫn hộ trợ các api của version cũ, cũng như giúp việc bảo trì, sửa chữa dễ dàng hơn.

Có nhiều cách để chia version cho API, mình thường hay dùng như thế này =))

```ruby
Rails.application.routes.draw do
  root "application#root"

  namespace :api do
    namespace :v1, defaults: {format: :json} do
      resources :my_blogs
    end
  end
end
```

Lúc này chạy rails routes để xem end point như thế nào nhé. Đây là các API của mình.

```ruby
GET    /api/v1/my_blogs
POST   /api/v1/my_blogs
GET    /api/v1/my_blogs/:id
PATCH  /api/v1/my_blogs/:id
PUT    /api/v1/my_blogs/:id
DELETE /api/v1/my_blogs/:id
```

## Cuối cùng

Vì bài viết hơi dài, nên mình xin phép sẽ để dành Authentication API và Viết document cho API sử dụng Swagger UI vào bài viết tiếp theo. ^^

Cảm ơn vì các bạn đã đọc đến đây, hi vọng sẽ giúp ít cho các bạn mới tìm hiểu về RESTful API. ❤️ 🙇

source: Viblo, Google, Tech Blog
