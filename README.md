# Aliyun OSS SDK for PHP

## 概述

阿里云对象存储（Object Storage Service，简称OSS），是阿里云对外提供的海量、安全、低成本、高可靠的云存储服务。用户可以通过调用API，在任何应用、任何时间、任何地点上传和下载数据，也可以通过用户Web控制台对数据进行简单的管理。OSS适合存放任意文件类型，适合各种网站、开发企业及开发者使用。


## 运行环境
- PHP 5.3+
- cURL extension

> 提示：
> - Ubuntu下可以使用apt-get包管理器安装php的cURL扩展 `sudo apt-get install php5-curl` 

## 安装方法
- 直接下载安装， SDK没有依赖其他三方库，可以直接使用sdk根目录的autoload.php
- 具体操作，请参考samples/目录的中的代码

## 快速使用

### 常用类

| 类名 | 解释 |
|:------------------|:------------------------------------|
|OSS\OssClient | OSS客户端类，用户通过OssClient的实例调用接口 |
|OSS\Core\OssException | OSS异常类，用户在使用的过程中，只需要注意这个异常|

### OssClient初始化

SDK的OSS操作通过OssClient类完成的，下面代码创建一个OssClient对象:

```php
<?php
$accessKeyId = "<您从OSS获得的AccessKeyId>"; ;
$accessKeySecret = "<您从OSS获得的AccessKeySecret>";
$endpoint = "<您选定的OSS数据中心访问域名，例如oss-cn-hangzhou.aliyuncs.com>";
try {
	$ossClient = new OssClient($accessKeyId, $accessKeySecret, $endpoint);
} catch (OssException $e) {
	print $e->getMessage();
}
```

### 文件操作

文件(又称对象,Object)是OSS中最基本的数据单元，您可以把它简单地理解为文件，用下面代码可以实现一个Object的上传：

```php
<?php
$bucket = "<您使用的Bucket名字，注意命名规范>";
$object = "<您使用的Object名字，注意命名规范>";
$content = "Hello, OSS!"; // 上传的文件内容
try {
	$ossClient->putObject($bucket, $object, $content);
} catch (OssException $e) {
	print $e->getMessage();
} 
```

### 存储空间操作

存储空间(又称Bucket)是一个用户用来管理所存储Object的存储空间,对于用户来说是一个管理Object的单元，所有的Object都必须隶属于某个Bucket。您可以按照下面的代码新建一个Bucket：
   
```php
<?php
$bucket = "<您使用的Bucket名字，注意命名规范>";
try {
	$ossClient->createBucket($bucket);
} catch (OssException $e) {
	print $e->getMessage();
}
```
	
### 返回结果处理

OssClient提供的接口返回返回数据分为两种：

* Put，Delete类接口，接口返回null，如果没有OssException，即可认为操作成功
* Get类接口，接口返回对应的数据，如果没有OssException，即可认为操作成功，举两个例子：

|接口 | 返回数据类型 |
|:----|:-----------|
|GetBucketCors|OSS\Model\CorsConfig|
|ListBuckets|OSS\Model\BucketListInfo|

    
### 运行Sample程序
	
1. 修改 `samples/Config.php`， 补充配置信息
2. 执行 `cd samples/ && php RunAll.php`

### 运行单元测试

1. 修改 `tests/OSS/Tests/Config.php`， 补充配置信息
2. 执行 `./vendor/bin/phpunit tests/OSS/Tests/`
    
### 生成API文档

1. 到根目录下，执行 `composer install`, 下载依赖的库
2. 执行`mkdir phpdoc && vendor/bin/phpdoc -d src -t phpdoc`，生成html格式的api文档在phpdoc目录中
3. 注意，需要php的版本是5.3，5.4，新版本的php不能正常使用phpdoc工具

## 联系我们

- [阿里云OSS官方网站](http://oss.aliyun.com)
- [阿里云OSS官方论坛](http://bbs.aliyun.com)
- [阿里云OSS官方文档中心](http://www.aliyun.com/product/oss#Docs)
- 阿里云官方技术支持：[提交工单](https://workorder.console.aliyun.com/#/ticket/createIndex)