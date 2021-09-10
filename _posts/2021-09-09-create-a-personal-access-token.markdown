---
layout: post
title:  "What is PAT? How to create a personal access token?"
date:   2021-09-09 10:42:10 +0530
tags: Grep Linux Command
image: post_7/github.jpg
---

Có thể các bạn đã biết hay chưa biết hoặc sắp biết thì bắt đầu từ ngày 13 tháng 8 năm 2021, Github không còn chấp nhận mật khẩu toàn khoản khi xác thực các hoạt động Git trên Github.com nữa và thay thế bằng giải pháp là sử dụng PAT. Vậy thì PAT là gì? Làm cách nào để tạo PAT thì mới các bạn đọc hết bài viêt này của mình^^! 

## PAT là gì?

```
Personal access tokens (PATs) are an alternative to using passwords for authentication to GitHub when using the GitHub API or the command line
```


PAT là viết tắt của Personal access tokens, nó là một giải pháp thay thế  cho việc sử dụng mật khâu để xác thực cho GitHub khi sử dụng API GitHub hoặc dòng lệnh.

Để phòng ngừa bảo mật, GitHub tự động xóa các mã thông báo truy cập cá nhân không được sử dụng trong một năm. Để cung cấp bảo mật bổ sung, bạn có thể thêm ngày hết hạn vào mã thông báo truy cập cá nhân của mình.

## Tạo một mã PAT như thế nào?

Về cách tạo mã PAT khá là đơn giản, sau đây là hướng dẫn step by step cách tạo mã PAT.

### 1. Xác minh địa chỉ email của bạn
Nếu email đăng kí tài khoản github của bạn chưa được [xác minh](https://docs.github.com/en/get-started/signing-up-for-github/verifying-your-email-address), thì cần xác minh trước khi tạo mã PAT.

### 2. Vào phần cài đặt account GitHub của bạn

![Project]({{ site.baseurl }}/images/post_7/step2.png)

### 3. Ở menu phía bên trái, chọn Developer settings

![Project]({{ site.baseurl }}/images/post_7/step3.png)

### 4. Ở menu phía bên trái, chọn Personal access tokens

![Project]({{ site.baseurl }}/images/post_7/step4.png)

### 5. Nhấn button Developer settings

Ở đây mình có tạo từ trước nên có thêm button revoke all

![Project]({{ site.baseurl }}/images/post_7/step5.png)

### 6. Thêm mô tả cho mã PAT

![Project]({{ site.baseurl }}/images/post_7/step6.png)

### 7. Thời gian hết hạn mã PAT

Mặc định khi tạo sẽ là 30 ngày.

![Project]({{ site.baseurl }}/images/post_7/step7.png)

### 8. Set quyền cho mã PAT

Github define khá nhiều quyền cho mã PAT, lưu ý để dùng mã PAT access repositories from the command line bạn phải chọn repo

![Project]({{ site.baseurl }}/images/post_7/step8.png)

### 9. Tạo mã PAT

![Project]({{ site.baseurl }}/images/post_7/step9.png)

### 10. Lưu ý

Xem mã PAT như mật khẩu và lưu giữ bí mật, cẩn thận. Khi làm việc với API hãy sử dụng qua biến môi trường thay vì set cứng và chia sẽ public
## Sử dụng mã PAT với command line

Khi đã có mã PAT, nhập mã PAT thay cho mật khẩu khi thực hiện các hoạt động Git qua giao thức HTTPS.
Ví dụ khi bạn clone một repo.

```
$ git clone https://github.com/username/repo.git
Username: your_username
Password: your_token
```


## Lời kết
Thanks for reading. Hy vọng bài viết giúp mình cho các bạn :D

Bài viết có tham khảo:
[GitHub Docs - Create a personal access token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token),
[GitHub Blog - Token authentication requirements for Git operations](https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/)
