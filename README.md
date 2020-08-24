# AWS-IAM-Workshop

本範例提供常用的 AWS IAM Policy 參考練習用

### IAM 策略-限定特定IP登入AWS-console

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "*",
            "Resource": "*",
            "Condition": {
                "IpAddress": {
                    "aws:SourceIp": [
                        "允許的IP-1/子網路遮罩",
                        "允許的IP-2/子網路遮罩",
                        "允許的IP-3/子網路遮罩"
                    ]
                }
            }
        }
    ]
}
```

### IAM 策略-限制Region與只能開特定型號EC2

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": "ec2:*",
            "Resource": "*",
            "Condition": {
                "ForAllValues:StringLike": {
                    "ec2:InstanceType": [
                        "t2.mirco",
                        "t2.small"
                    ]
                },
                "ForAnyValue:StringEquals": {
                    "ec2:Region": "ap-northeast-1"
                }
            }
        }
    ]
}
```

### 結合上述的條件，修改成組合版本

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": "ec2:*",
            "Resource": "*",
            "Condition": {
                "ForAllValues:StringLike": {
                    "ec2:InstanceType": [
                        "t2.mirco",
                        "t2.small"
                    ]
                },
                "ForAnyValue:StringEquals": {
                    "ec2:Region": [
                        "ap-northeast-1",
                        "us-east-1"
                    ]
                },
                "IpAddress": {
                    "aws:SourceIp": "0.0.0.0/0"
                }
            }
        }
    ]
}


