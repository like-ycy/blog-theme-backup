---
showonlyimage: true
title:      " 阿里云子账号权限策略 "
subtitle:   ""
excerpt: ""
description: ""
date:       2019-12-15
author:     "望翔"
image: "https://image.my-blog.wang/header/header.jpg"
published: true
tags:
    - Aliyun

categories: [ Tech ]
URL: "/2019/12/15/aliyun-policy/"

---

# 1、OSS读写权限

```json
{
    "Version": "1",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "oss:ListBuckets",
                "oss:GetBucketStat",
                "oss:GetBucketInfo",
                "oss:GetBucketTagging",
                "oss:GetBucketAcl"
            ],
            "Resource": "acs:oss:*:*:*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "oss:Get*",
                "oss:List*"
            ],
            "Resource": "acs:oss:*:*:oss名称"
        },
        {
            "Effect": "Allow",
            "Action": [
                "oss:Get*",
                "oss:List*",
                "oss:Put*",
                "oss:AbortMultipartUpload"
            ],
            "Resource": "acs:oss:*:*:oss名称/*"
        }
    ]
}
```

# 2、日志服务查看指定Project (只能创建，不能删除)

```json
{
    "Version": "1",
    "Statement": [
        {
            "Action": [
                "log:ListProject"
            ],
            "Resource": [
                "acs:log:*:*:project/*"
            ],
            "Effect": "Allow"
        },
        {
            "Action": [
                "log:Get*",
                "log:List*",
                "log:Create*",
                "log:Update*",
                "log:Post*"
            ],
            "Resource": "acs:log:*:*:project/project名称/*",
            "Effect": "Allow"
        }
    ]
}
```