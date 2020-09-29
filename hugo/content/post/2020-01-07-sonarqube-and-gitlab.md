---
showonlyimage: true
title:      " sonarqube 搭配gitlab-ci "
subtitle:   ""
excerpt: ""
description: ""
date:       2020-01-07
author:     "望翔"
image: "https://image.my-blog.wang/header/header.jpg"
published: true
tags:
    - Gitlab

categories: [ Tech ]
URL: "/2020/01/07/sonarqube-and-gitlab/"


---

1、项目文件中创建sonar-project.properties 文件

```bash
#项目的key
sonar.projectKey=admin
#sonarqube的主机地址
sonar.host.url=https://192.168.1.6:9000
#项目的名字（这个名字在sonar界面显示的,此处根据项目名称修改）
sonar.projectName=sonar-test
#项目的版本（这个名字在sonar界面显示的,根据项目版本修改）
sonar.projectVersion=1.0
#需要分析源码的目录，多个目录用英文逗号隔开（根据需要修改）
sonar.sources=./
#编码格式
#sonar.sourceEncoding=UTF-8
#项目所用语言
sonar.language=java
#登录账号
sonar.login=admin
#登录密码
sonar.password=admin
#包含与源文件对应的已编译字节码文件 (如果没编译可以不写,默认创建target/sonar目录)
sonar.java.binaries=target/sonar
```

例如：如下图

![](https://img-blog.csdnimg.cn/20190917181444209.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dhbmc5MDE5,size_16,color_FFFFFF,t_70)

2、修改项目.gitlab-ci.yml文件，在首部添加如下：

```yaml
sonar_preview:
  stage: test
  script:
    - /usr/local/sonar-scanner/bin/sonar-scanner
  except:
    - master
  tags:
    - sonar
```

例如：如下图

![](https://img-blog.csdnimg.cn/20190917181327753.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dhbmc5MDE5,size_16,color_FFFFFF,t_70)

3、修改完成后，分支用户每次commit都会触发进行代码检测（没有触发请手动）