<p align="center">
  Padchat-PHP-Demo
</p>
<p align="center">微信IPAD协议对接websocket服务,主要依赖swoole异步客户端，进程管理等功能模块</p>

<p align="center">
  <a href="https://github.com/fastgoo/padchat-php"><img src="https://img.shields.io/badge/license-MIT-brightgreen.svg"></a> <a href="https://github.com/fastgoo/padchat-php"><img src="https://img.shields.io/badge/swoole-1.9+-brightgreen.svg"></a> 
  <a href="https://github.com/fastgoo/padchat-php"><img src="https://img.shields.io/badge/php->=7.0-brightgreen.svg"></a> <a href="https://github.com/fastgoo/padchat-php"><img src="https://img.shields.io/badge/server-windows-2077ff.svg"></a>
</p>

---
:heartpulse: **[安利一个新的ipadchat项目](https://github.com/fastgoo/ipadchat-api)：** 该项目是基于HTTP通讯协议开发，安装难度低，下载demo就可运行。

:zap: **[推荐--nodejs版本](https://github.com/binsee/padchat-sdk)：** padchat团队提供的nodesdk,本项目是参照该项目开发

:dart: **[Swoole](https://www.swoole.com/)：** 版本需要为1.9+，主要使用其定时器、异步websocket客户端、多进程管理等

:art: **[PHP7+](http://www.php.net/)：** PHP版本需要为7+，因为代码中使用PHP特有的行特性，低版本安装会出现异常

:wine_glass: **[Redis](https://redis.io/)：** 依赖redis扩展，二维码、状态、微信信息、好友列表等存储。如果不需要可以修改配置cache为false就可以了

## 更新日志
#### 2018-06-13
- 响应服务端心跳
#### 2018-06-08 
- 新增syncContact接口触发同步通讯录
- 新增getMyInfo接口获取当前连接的用户信息wxid、uin
- 新增syncMsg接口手动同步微信消息
- 发送语音消息新增time字段，控制时长

## 已实现功能
- 账号密码登录（多账号一键登录）
- 默认未设置账号会使用二维码扫码登录
- 二维码会显示在终端
- 扫码登录成功后会启动定时任务
- 登录成功用户数据会存入到redis缓存
- 好友列表、公众号列表、群列表存入到redis list
- 外部手动发送消息（redis队列 + swoole tick实现）
- 添加白名单机制，只有白名单的wxid才可以监听消息事件 (目前实现是写死代码)

## TODO
- 用户的个人微信二维码会存到redis 
- 添加 mysql服务，用户存储一些数据信息以及日志记录
- 用户登录成功后会通过redis获取到配置信息（白名单、指令、监听、好友申请、红包、收款、朋友圈等）
- 监听指定指令，通过不同指令做不同的操作（发送文字、图片、语音、文件、链接、名片，群邀请）
- 好友申请，用户好友申请备注信息匹配指令会自动通过好友申请，同时会做自动拉群的操作
- 红包，自动抢红包，自动抢指定群的红包
- 自动收款
- 发送朋友圈消息，自动定时发送（文字、图片、视频等）

## 安装说明

需要在window-server启动server.exe应用程序，该程序目前仅供学习参考。

- `git clone https://github.com/fastgoo/padchat-php.git` 克隆项目
- `cd padchat-php` 进入项目
- `composer install` 安装依赖包
- `php run.php` 开始服务

## 启动说明
在启动项目之前需要先配置配置文件，配置后才方可启动

```
    'debug' => [
        /** 请求记录debug */
        'request' => false,
        /** 响应数据记录debug */
        'response' => false,
        /** 在命令终端输出debug */
        'cmd' => true,
    ],
    'process' => [
        /** 启用多进程开启多个服务 */
        'status' => false,
        /** 最多同时启动的服务数量 */
        'count' => 1
    ],
    'server' => [
        'host' => '远程服务器ip,默认',
        'port' => 7777,
        'cache' => false,//是否开启缓存，redis缓存
        'is_account' => false,//是否通过账号配置登录
    ],
    'redis' => [
        'host' => '127.0.0.1',
        'port' => 6379,
        'auth' => '',
    ],
```
如需在生产环境运行，请关闭日志打印，以及终端输出。同时向保证进程稳定运行请使用进程守护工具守护进程，保证进程的正常运行。

## 项目简介
- 项目启动后会自动启动服务，生成二维码
- 二维码存放在runtime/qrcode/xxx.png（根据时间生成的）
- 可以通过配置配置请求写入日志，响应写入日志，或者直接输出在终端上
- 里面封装了大部分时间以及数据处理，后续会做持续更新

## 技术支持
- 服务支持：周先生 微信号 huoniaojugege
- 协议支持：大牙 QQ 51166611



