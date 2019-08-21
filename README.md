<h1 align="center"> Aliyun SLB SDK for Java </h1>

[![Build Status](https://travis-ci.com/lihangqi/aliyun-java-sdk-slb.svg?branch=master)](https://travis-ci.com/lihangqi/aliyun-java-sdk-slb)
[![codecov](https://codecov.io/gh/lihangqi/aliyun-java-sdk-slb/branch/master/graph/badge.svg)](https://codecov.io/gh/lihangqi/aliyun-java-sdk-slb)

阿里云负载均衡SDK

欢迎使用阿里云开发者工具套件（Alibaba Cloud SDK for Java）。Alibaba Cloud SDK for Java让您不用复杂编程即可访问云服务器、云数据库RDS、云监控等多个阿里云服务。本教程介绍如何安装并开始使用Alibaba Cloud SDK for Java。

## 前提条件
使用Alibaba Cloud SDK for Java，您需要一个阿里云账号和访问密钥（AccessKey）。 请在阿里云控制台中的[AccessKey管理页面](https://usercenter.console.aliyun.com/?spm=a2c4g.11186623.2.14.32f72c44JN1mCw#/manage/ak)上创建和查看您的AccessKey，或联系您的系统管理员。
使用Alibaba Cloud SDK for Java调用某个产品的API前，确保您已经在[阿里云控制台](https://home.console.aliyun.com/?spm=a2c4g.11186623.2.15.32f72c44JN1mCw)开通了该产品。
安装Java环境。Alibaba Cloud SDK for Java要求使用JDK1.6或更高版本。

## 安装Alibaba Cloud SDK for Java
您可以通过添加Maven依赖或下载Alibaba Cloud SDK for Java工具包的方式安装Alibaba Cloud SDK for Java，详情参见安装Alibaba Cloud SDK for Java。

您只需在pom.xml文件中添加以下依赖即可：

> **说明** 无论您要使用哪个产品的开发工具包，都必须安装Alibaba Cloud SDK for Java核心库。例如，如果要使用SLB的Java SDK，您需要[安装Alibaba Cloud SDK for Java](https://help.aliyun.com/document_detail/52740.html?spm=a2c4g.11186623.2.16.32f72c44JN1mCw#concept-mkk-vpj-zdb)核心库和ECS的Java SDK。

```java
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-java-sdk-core</artifactId>
    <version>3.7.0</version>
</dependency>
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-java-sdk-slb</artifactId>
    <version>3.2.2</version>
</dependency>
```

## 使用Alibaba Cloud SDK for Java
以下代码示例展示了调用Alibaba Cloud SDK for Java的三个主要步骤：

- 创建DefaultAcsClient实例并初始化。
- 创建API请求并设置参数。
- 发起请求并处理应答或异常。

```java
package com.testprogram;
import com.aliyuncs.profile.DefaultProfile;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.ecs.model.v20140526.*;
public class Main {
    public static void main(String[] args) {
         // 创建DefaultAcsClient实例并初始化
        DefaultProfile profile = DefaultProfile.getProfile(
            "<your-region-id>",          // 地域ID
            "<your-access-key-id>",      // RAM账号的AccessKey ID
            "<your-access-key-secret>"); // RAM账号AccessKey Secret
        IAcsClient client = new DefaultAcsClient(profile);
         // 创建API请求并设置参数
        DescribeInstancesRequest request = new DescribeInstancesRequest();
        request.setPageSize(10);
        // 发起请求并处理应答或异常
        DescribeInstancesResponse response;
        try {
            response = client.getAcsResponse(request);
            for (DescribeInstancesResponse.Instance instance:response.getInstances()) {
                System.out.println(instance.getPublicIpAddress());
            }
        } catch (ServerException e) {
            e.printStackTrace();
         } catch (ClientException e) {
            e.printStackTrace();
        }
    }
}
```
