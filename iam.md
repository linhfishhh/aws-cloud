# IAM là gì?
- kiểm soát truy cập và định danh vào các tài nguyên aws

## User
- Cung cấp long term credential access api của aws
- Chứa thông tin chúng thực bao gồm username, password để login vào web console
- Cung cấp định danh thể gọi API thông qua cli bằng access key và secret key
- Bảo mật user với Authenicator
### Root user
- là user khi đăng ký với aws
- Là user có quyền cao nhất
```bestpractice
Best pratice: không nên sử dụng user root cho hoạt động hằng ngày trên aws vì có thể dẫn tới những rủi do về bảo mật
```
### IAM user
- Là những user do root user tạo ra

## Policy
- Định nghĩa User/Group/resource trong aws có thể làm gì với aws resource
### Thành phần

ví ụ:
```sample
{
      "Version": "2012-10-17",
      "Statement": [
        {
          "Sid": "Stmt1571666184581",
          "Action": [
            "elasticbeanstalk:CreateApplication"
          ],
          "Effect": "Allow",
          "Resource": "arn:aws:elasticbeanstalk:ap-southeast-1:1234567:application/staging",
          "Condition": {
            "DateGreaterThan": {
              "aws:CurrentTime": "2019/10/18"
            }
          }
        }
      ]
    }
```