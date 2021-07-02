# AWS_Lambda_Auto_Update_CloudFront_IP
使用AWS lambda + SNS自动更新ALB 负载均衡器中cloudfront的inbound IP

参考：

https://aws.amazon.com/cn/blogs/security/how-to-automatically-update-your-security-groups-for-amazon-cloudfront-and-aws-waf-by-using-aws-lambda/
https://github.com/aws-samples/aws-cloudfront-samples/tree/master/amazon-cloudfront-staging-to-production
https://github.com/wangerzi/aws-cloudfront-samples/blob/master/update_security_groups_lambda/update_security_groups.py

以下介绍修改的内容：

1. 不指定区域，更新所有cloudfront IPV4
2. 同时更新两组、四个安全组，每组IP 相同
3. 60个IP一组

步骤：

step 1. 

先按照以下url内容创建好policy和role

https://aws.amazon.com/cn/blogs/security/how-to-automatically-update-your-security-groups-for-amazon-cloudfront-and-aws-waf-by-using-aws-lambda/

step 2. 

在美国东部 (弗吉尼亚北部)us-east-1区创建lambda函数：auto-update-security-group-lambda
执行时间设为60s
将创建好的role附加到lambda

step 3.

添加测试事件，其中md5可能会更新，若更新，控制台会打印出最新md5，但sns里带的md5一般是最新的，参考：

https://github.com/LisxAlison/AWS_Lambda_Auto_Update_CloudFront_IP/blob/main/lambda%E6%B5%8B%E8%AF%95%E4%BA%8B%E4%BB%B6

step 4.

配置SNS创建订阅：
arn:aws:sns:us-east-1:806199016981:AmazonIpSpaceChanged
终端节点设为lambda。

step 5.

配置alb安全组标签如下：

web1安全组

Key | value

AutoUpdate | true

Name | cloudfront_web1

Protocol | https

web2 安全组

Key | value

AutoUpdate | true

Name | cloudfront_web1

Protocol | https
