# 后台管理子系统

## 1. 小组分工

| 姓名         | 任务                                                         |
| ------------ | ------------------------------------------------------------ |
| 陈琪（组长） | 用户管理部分，与其他小组沟通交互简要要求，并确保本小组项目进度按时完成 |
| 程尔聪       | 数据管理部分，与其他小组沟通并提供接口，并帮助其他组员解决技术问题 |
| 王佳琦       | 数据的备份以及后期管理呈现，并协助尚文达完成审核部分         |
| 尚文达       | 完成讲解审核部分，并设置合适的视频上传及审核后存储的方式     |
| 赛欣         | 完成每周记录和项目相关说明文档，并完成项目的测试和报告编写   |

## 2. 时间规划

暂定如下

| 时间     | 任务                                                         |
| -------- | ------------------------------------------------------------ |
| 第六周   | 学习git及相关工具使用,确定人员分工                           |
| 第七周   | 确定技术栈并学习相关知识，完成小组项目管理计划               |
| 第八周   | 熟悉项目结构，确定数据库设计结构，完成需求规格说明书         |
| 第九周   | 进行代码的编写，初步完成接口管理功能（数据包括：博物馆信息、新闻信息、展览信息、藏品信息、评论信息、讲解信息） |
| 第十周   | 初步完成审核操作，实现服务器数据的获取、接口基本完成、实现数据库备份与恢复 |
| 第十一周 | 生成管理员日志、评论讲解的审核，完善之前的工作，开发前端界面 |
| 第十二周 | 全班代码整合调试，继续开发前端界面                           |

## 3. 需求列表

### 3.1 具体数据库表

#### 博物馆信息表：museum info table

> 地址
>
> 开闭馆时间
>
> 门票价格
>
> 博物馆类别
>
> 外文名

| 名称                       | 类型          | 空   | 默认值           | 说明           |
| -------------------------- | ------------- | ---- | ---------------- | -------------- |
| muse_ID(p_key)博物馆序列号 | int           | N    | <auto_increment> | 自增的ID       |
| muse_Name                  | varchar(50)   | N    |                  | 博物馆名称     |
| muse_Intro                 | Long text     | N    |                  | 博物馆信息     |
| muse_Location              | decimal(10,6) | N    |                  | 博物馆坐标     |
| muse_Address               | varchar(100)  | N    |                  | 博物馆地址     |
| muse_Opentime              | varchar(50)   | N    |                  | 博物馆开馆时间 |
| muse_price                 | varchar(10)   | N    |                  | 博物馆票价     |
| muse_class                 | varchar(50)   | N    |                  | 博物馆级别     |
| muse_Ename                 | varchar(50)   | N    |                  | 博物馆英文名   |

#### 藏品信息表：collection info table

> 去除年代

| 名称                    | 类型        | 空   | 默认值           | 说明         |
| ----------------------- | ----------- | ---- | ---------------- | ------------ |
| col_ID(p_key)藏品序列号 | int         | N    | <auto_increment> | 自增ID       |
| muse_ID(f_key)          | int         | N    |                  | 所属博物馆ID |
| col_Name                | varchar(50) | N    |                  | 藏品名       |
| col_Intro               | Long text   | N    |                  | 藏品描述     |
| col_Photo               | text        | N    |                  | 藏品图片     |

#### 教育活动表：education act table

> 时间
>
> 图片
>
> url

| 名称           | 类型        | 空   | 默认值           | 说明         |
| -------------- | ----------- | ---- | ---------------- | ------------ |
| act_ID(p_Key)  | int         | N    | <auto_increment> | 自增ID       |
| muse_ID(f_key) | int         | N    |                  | 所属博物馆ID |
| act_Name       | varchar(50) | N    |                  | 活动名称     |
| act_Content    | Long text   | N    |                  | 活动内容     |
| act_Time       | varchar(20) | N    |                  | 活动时间     |
| act_Pic        | text        | N    |                  | 活动图片     |
| act_Url        | text        | N    |                  | 活动URL      |

### 展览信息表：exhibition info table

> 图片

| 名称            | 类型        | 空   | 默认值           | 说明         |
| --------------- | ----------- | ---- | ---------------- | ------------ |
| exhib_ID(p_key) | int         | N    | <auto_increment> | 自增ID       |
| muse_ID(f_key)  | int         | N    |                  | 所属博物馆ID |
| exhib_Name      | varchar(50) | N    |                  | 展览名称     |
| exhib_Content   | Long text   | N    |                  | 展览内容     |
| exhib_Pic       | text        | N    |                  | 展览图片     |

### 新闻信息表：news info table

| 名称           | 类型         | 空   | 默认值           | 说明         |
| -------------- | ------------ | ---- | ---------------- | ------------ |
| news_ID(p_key) | int          | N    | <auto_increment> | 自增ID       |
| muse_ID(f_key) | int          | N    |                  | 所属博物馆ID |
| news_Name      | varchar(255) | N    |                  | 新闻名称     |
| news_Content   | Long text    | N    |                  | 新闻内容     |
| news_type      | int          | N    |                  | 新闻类型     |
| news_time      | DataTime     | N    |                  | 新闻时间     |
| news_source    | varchar(20)  | N    |                  | 新闻来源     |

### 评论表：comment table

> 时间

| 名称           | 类型      | 空   | 默认值           | 说明         |
| -------------- | --------- | ---- | ---------------- | ------------ |
| com_ID(p_key)  | int       | N    | <auto_increment> | 评论ID       |
| user_ID(f_key) | int       | N    |                  | 评论者ID     |
| muse_ID(f_key) | int       | N    |                  | 评论博物馆ID |
| com_Info       | Long text | Y    |                  | 评论内容     |
| com_Time       | DataTime  | N    |                  | 评论时间     |
| com_IfShow     | boolean   | N    | false            | 是否显示     |

### 用户表：user table

> 头像（默认头像）

| 名称           | 类型        | 空   | 默认值           | 说明       |
| -------------- | ----------- | ---- | ---------------- | ---------- |
| user_ID(p_key) | int         | N    | <auto_increment> | 自增ID     |
| user_Name      | varchar(50) | N    |                  | 用户名     |
| user_Phone     | varchar(20) | N    |                  | 用户手机号 |
| user_Passwd    | varchar(20) | N    |                  | 用户密码   |
| user_Email     | varchar(20) | N    |                  | 用户邮箱   |
| user_Avatar    | text        | N    | 默认图片         | 用户头像   |
| if_com         | boolean     | N    | True             | 评论权限   |

### 管理员表：admin table

| 名称            | 类型        | 空   | 默认值           | 说明       |
| --------------- | ----------- | ---- | ---------------- | ---------- |
| admin_ID(p_key) | int         | N    | <auto_increment> | 自增ID     |
| admin_Name      | varchar(50) | N    |                  | 管理员姓名 |
| admin_Passwd    | varchar(20) | N    |                  | 密码       |

### 审核视频表：review video table

| 名称              | 类型       | 空   | 默认值           | 说明                       |
| ----------------- | ---------- | ---- | ---------------- | -------------------------- |
| video_ID(p_key)   | int        | N    | <auto_increment> | 自增ID                     |
| muse_ID(f_key)    | int        | N    |                  | 所属博物馆ID               |
| user_ID(f_key)    | int        | N    |                  | 上传用户ID                 |
| video_Url         | text       | N    |                  | 视频URL                    |
| video_IfShow      | boolean    | N    | False            | 视频是否展示（管理员审核） |
| video_Name        | vachar(50) | N    |                  | 视频名称                   |
| video_Time        | DataTime   | N    |                  | 上传时间                   |
| video_Description | Long text  | N    |                  | 视频描述                   |

### 反馈表：feedback table

| 名称             | 类型 | 空   | 默认值           | 说明         |
| ---------------- | ---- | ---- | ---------------- | ------------ |
| fdback_ID(p_key) | int  | N    | <auto_increment> | 自增ID       |
| muse_ID(f_key)   | int  | N    |                  | 所属博物馆ID |
| user_ID(f_key)   | int  | N    |                  | 反馈的用户ID |
| env_Review       | int  | N    |                  | 评分标准1    |
| exhibt_Review    | int  | N    |                  | 评分标准2    |
| service_Review   | int  | N    |                  | 评分标准3    |

### 关注表：attention table

| 名称           | 类型 | 空   | 默认值           | 说明           |
| -------------- | ---- | ---- | ---------------- | -------------- |
| att_ID(p_key)  | int  | N    | <auto_increment> | 自增ID         |
| muse_ID(f_key) | int  | N    |                  | 关注的博物馆ID |
| user_ID(f_key) | int  | N    |                  | 用户ID         |

### 3.2 E-R图

http://m.qpic.cn/psc?/V52rU8aH0iADSI1DfPCi3tyKFr3psVCQ/TmEUgtj9EK6.7V8ajmQrEI.p4EhOC9.v4NPc0k1umThajuK.fNrSh.Of1lyO4FiyIJMVY3Z4U829zjv2LZRd2Qymc.oE9ZEh40Ce9IasUR0!/b&bo=cAS9AgAAAAADF*k!&rf=viewer_4&t=5

### 3.3 功能设计

#### 实现功能

- 用户管理：管理后台用户信息
- 讲解审核：审核用户上传的讲解视频
- 数据管理：管理整个系统涉及到的所有数据
- 数据库的备份和恢复：实现数据库的定时备份，可以实现对历史版本的恢复

#### 功能详细描述

- 登录验证功能

- 用户管理

  实现修改用户信息、添加用户、删除用户等操作

- 讲解审核

  用户上传内容管理员进行审核，审核通过后再上传到仓库

- 数据管理

  - 查看所有博物馆信息
    - 查看所选博物馆的详细信息
    - 新建博物馆
    - 修改博物馆
    - 删除博物馆
  - 查看展览信息
    - 查看所选展览的详细信息
    - 新建展览
    - 修改展览
    - 删除展览
  - 藏品信息
    - 查看藏品详细信息
    - 新建藏品信息
    - 修改藏品信息
    - 删除藏品信息
  - 新闻信息
    - 查看新闻详细信息
    - 新建新闻信息
    - 修改新闻信息
    - 删除新闻信息
  - 讲解信息
    - 新建新闻信息
    - 修改新闻信息
    - 删除新闻信息
  - 查看所有评论信息
    - 隐藏评论
    - 删除评论
  - 数据库操作日志
    - 查看数据库的所有日志

* 数据备份和恢复

  * 数据库定时备份

    每周周二周五零点定时备份

  * 数据库恢复

  * 选择数据库历史版本

* 新增需求
  * 设计新增用户时不允许重名
  * 超时自动注销
  * 按博物馆评分排序
  * 允许用户上传修改头像
  * 其他

### 4.部分接口设计

| 接口名称             | 接口描述                                                     |
| -------------------- | ------------------------------------------------------------ |
| POST museum          | 新建博物馆信息                                               |
| GET museum           | 获取博物馆信息                                               |
| DEL museum           | 删除博物馆信息                                               |
| POST museum_news     | 新建博物馆新闻                                               |
| GET museum_news      | 获取博物馆新闻                                               |
| DEL museum_news      | 删除博物馆新闻                                               |
| GET comment          | 获取用户评论                                                 |
| POST comment         | 新建用户评论                                                 |
| PUT comment          | 隐藏/恢复用户评论                                            |
| DEL comment          | 删除用户评论                                                 |
| POST collection      | 新建展品                                                     |
| GET collection       | 获取展品                                                     |
| DEL collection       | 删除展品                                                     |
| POST education       | 新建教育活动                                                 |
| GET education        | 获取教育活动                                                 |
| DEL education        | 删除教育活动                                                 |
| POST exhibition      | 新建展览活动                                                 |
| GET exhibition       | 获取展览活动                                                 |
| DEL exhibition       | 删除展览活动                                                 |
| POST feedback        | 新建反馈信息                                                 |
| GET feedback         | 获得反馈信息                                                 |
| GET feedback_average | 获取博物馆平均反馈                                           |
| PUT feedback         | 修改评价                                                     |
| POST attention       | 新建关注                                                     |
| GET attention        | 获得关注                                                     |
| DEL attention        | 取消关注                                                     |
| GET user             | 获得用户                                                     |
| POST user            | 新建用户                                                     |
| DEL user             | 删除用户                                                     |
| PUT user             | 修改用户                                                     |
| GET admin            | 获得管理员                                                   |
| POST admin           | 新建管理员                                                   |
| DEL admin            | 删除管理员                                                   |
| PUT admin            | 修改管理员                                                   |
| GET video            | 获得视频                                                     |
| DEL video            | 删除视频                                                     |
| PUT video            | 修改视频                                                     |
| POST video           | 新建视频                                                     |
| GET login            | 用户登录时，验证其用户名和密码是否匹配，正确即返回success（用于后台使用） |
| POST login           | 前端发送用户登录请求，在用户名和密码正确的情况下返回token，时效为0.5小时 |
| GET loginInfo        | 接到token后，解码信息并返回用户名，ID，头像（用于前端调用）  |
| GET backlogin        | :管理员登录时，验证其管理员名和密码是否匹配，正确即返回success（用于后 台使用） |
| POST backlogin       | 前端发送管理员登录请求，在管理员名和密码正确的情况下返回token，时效为 0.5小时 |
| GET backloginInfo    | 接到token后，解码信息并返回管理员名和ID（用于前端调用）      |

