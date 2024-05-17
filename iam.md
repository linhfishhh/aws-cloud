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

### Federated user
- Là những user thuộc các hệ thống AD hoặc web identity khác access vào aws resource thông qua dịch vụ Identity provider ( giao thức saml hoặc OIDC )

## Policy
- Định nghĩa User/Group/resource trong aws có thể làm gì với aws resource

ví dụ:
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

### Thành phần
- version: Phiên bản của policy
- Statement: mỗi policy đều có ít nhất 1 hoặc nhiều statement, statement dùng để chỉ định action nào được thực thi và tài nguyên nào được truy cập, bên trong stament gồm các thành phần:
* sid: chuỗi unique định danh statement
* Effect: chỉ định action được liệt kê (Allow/Deny)
* Principal: tài khoản/User/Role được cho phép (Allow) hoặc deny vào aws resource
* Resource: aws resource mà bạn muốn áp dụng những action trên
* condition: chỉ định điều kiện bắt buộc phải tuân theo khi áp dụng policy này (ví dụ: StringEquals...)


### Phân loại
#### Identity base policy
- Chính là những policy được đính kèm với User/Group/Role trong IAM, Chúng quy định những hành động được phép hoặc không được phép truy cập
##### Các Loại Identity base policy
- Managed policy: là những policy có sẵn do aws cung cấp
- Custom policy: là những policy do người dùng định nghĩa


#### Resource base policy
- Là policy được gắn liền với resource trong aws, ví dụ là chỉ định resource base policy vào S3, SQS... ta có thể chỉ định xem ai là người có quyền hoặc không có quyền access vào resource

#### In-line policy
là những policy do người dùng gán trực tiếp vào User/Role