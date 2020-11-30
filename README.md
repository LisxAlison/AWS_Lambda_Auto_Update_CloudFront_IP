# AWS_Lambda_Auto_Update_CloudFront_IP
使用AWS lambda + SNS自动更新ALB 负载均衡器中cloudfront的inbound IP

参考：
https://github.com/aws-samples/aws-cloudfront-samples/tree/master/amazon-cloudfront-staging-to-production
https://github.com/wangerzi/aws-cloudfront-samples/blob/master/update_security_groups_lambda/update_security_groups.py

以下介绍修改的内容：
1. 不指定区域，更新所有cloudfront IPV4
2. 同时更新两组、四个安全组，每组IP 相同
3.60个IP一组
