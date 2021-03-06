# APP导览子系统需求设计分析书

## 一、系统开发的背景和意义

略

## 二、系统需求分析

### 1.面向用户

app仅面向普通用户

### 2.实现功能

- 地图导览

  在地图上显示所有的博物馆位置，支持通过博物馆名称搜索，支持通过博物馆地图标记查看博物馆详细信息，以及从用户的当前定位位置到指定博物馆之间进行路径规划导航。

- 用户登陆注册

  支持用户的登陆、注册操作，以及用户对用户个人信息的维护操作

- 博物馆讲解

  支持用户对指定博物馆录制讲解视频并上传由后台审核，查看已经审核通过的讲解，查看自己上传的讲解视频的状态。

### 3.功能详细描述

#### (1)地图导览

在地图上标记所有博物馆的位置，同时点击标记可以展开博物馆信息，提供跳转到该博物馆详情信息、讲解视频查看页面以及展览信息的入口；同时提供搜索功能，通过搜索可以在地图上展示目标博物馆的标记。对用户定位，并规划从用户到目标博物馆的路线规划。

#### (2)用户注册登陆

用户可以注册帐号，注册帐号时需要填写用户名以及密码，或者选择登陆，登陆时需要填写用户名密码，同时记住登陆状态，登陆之后才有权限参与评论、讲解录制上传、打分等功能。

#### (3)博物馆讲解录制

用户可以查看已经审核通过的所有讲解，在该页面只展示缩略图以及讲解标题、发布时间信息，点击之后进入讲解详情页，可以播放讲解视频。同时提供上传讲解视频的页面入口，在该页面，可以现场录制或者上传讲解视频，讲解视频应该限制时长或者大小。用户查看自己已经上传的讲解的状态。

## 三、业务流程分析

### 1.通过地图查看博物馆详情流程

* 底部导航栏->地图页面->搜索博物馆->展示搜索结果列表以及地图标记->展开目标博物馆信息->进入具体信息查看页面
* 底部导航栏->地图页面->找到博物馆在地图上标记->展开目标博物馆信息->进入具体信息查看页面

### 2.用户注册(登陆)流程

* 我的页面->登陆页面->帐号注册(登陆)->填写用户名密码信息注册(登陆)
* 在将要执行需要用户权限的功能的页面->跳转到注册(登陆)页面->帐号注册(登陆)->填写用户名密码信息注册(登陆)

### 3. 博物馆导览流程

* 地步导航栏->地图页面->点击博物馆在地图上的标记->点击进行路线规划->定位并在地图上绘制路线

## 四、界面模块设计

### 1.界面模块示意图

![](https://z3.ax1x.com/2021/05/07/g3ZMND.png)

### 2.功能模块设计

#### (1) 地图页面

* 通过搜索框搜索指定的博物馆并显示在地图上
* 地图上标记点击展开博物馆信息卡片
* 通过卡片可以进入博物馆信息详情页面、讲解查看页面以及展览详情页面
* 展示所有博物馆在地图上的位置
* 根据定位展示该城市的博物馆

#### (2) 我的界面

* 用户登陆页面入口(若已经登陆，则为用户个人信息页面)
* APP设置页面入口
* 查看用户自己上传的讲解视频页面入口

#### (3) 用户个人信息页面

* 查看用户个人信息
* 编辑用户个人信息

#### (4) 登陆注册页面

* 可选择当前操作是登陆还是注册



