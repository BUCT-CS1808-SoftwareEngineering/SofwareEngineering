## 后台管理子系统

### 1. 小组分工

| 姓名         | 任务                                                         |
| ------------ | ------------------------------------------------------------ |
| 陈琪（组长） | 用户管理部分，与其他小组沟通交互简要要求，并确保本小组项目进度按时完成 |
| 程尔聪       | 数据管理部分，与其他小组沟通并提供接口，并帮助其他组员解决技术问题 |
| 王佳琦       | 数据的备份以及后期管理呈现，并协助尚文达完成审核部分         |
| 尚文达       | 完成讲解审核部分，并设置合适的视频上传及审核后存储的方式     |
| 赛欣         | 完成每周记录和项目相关说明文档，并完成项目的测试和报告编写   |

### 2. 时间规划

暂定如下

| 时间     | 任务                                                         |
| -------- | ------------------------------------------------------------ |
| 第六周   | 学习GitHub及相关工具使用                                     |
| 第七周   | 搭建好环境，完成小组项目管理计划                             |
| 第八周   | 熟悉项目结构，完成需求规格说明书                             |
| 第九周   | 进行代码的编写，初步完成数据管理功能                         |
| 第十周   | 初步完成审核操作，实现服务器数据的获取、接口基本完成、实现数据库备份与恢复 |
| 第十一周 | 生成管理员日志、评论讲解的审核，完善之前的工作               |
| 第十二周 | 全班代码整合调试                                             |

### 

### 3. 需求列表

### 博物馆信息表：museum info table

地址

开闭馆时间

门票价格

博物馆类别

外文名

| 名称                       | 类型          | 空   | 默认值           |
| -------------------------- | ------------- | ---- | ---------------- |
| muse_ID(p_key)博物馆序列号 | int           | N    | <auto_increment> |
| muse_Name                  | varchar(50)   | N    |                  |
| muse_Intro                 | Long text     | N    |                  |
| muse_Location              | decimal(10,6) | N    |                  |
| muse_Address               | varchar(100)  | N    |                  |
| muse_Opentime              | varchar(50)   | N    |                  |
| muse_price                 | varchar(10)   | N    |                  |
| muse_class                 | varchar(50)   | N    |                  |
| muse_Ename                 | varchar(50)   | N    |                  |

### 藏品信息表：collection info table

去除年代

| 名称                    | 类型        | 空   | 默认值           |
| ----------------------- | ----------- | ---- | ---------------- |
| col_ID(p_key)藏品序列号 | int         | N    | <auto_increment> |
| muse_ID(f_key)          | int         | N    |                  |
| col_Name                | varchar(50) | N    |                  |
| col_Intro               | Long text   | N    |                  |
| col_Photo               | text        | N    |                  |

###教育活动表：education act table

时间

图片

url

| 名称           | 类型        | 空   | 默认值           |
| -------------- | ----------- | ---- | ---------------- |
| act_ID(p_Key)  | int         | N    | <auto_increment> |
| muse_ID(f_key) | int         | N    |                  |
| act_Name       | varchar(50) | N    |                  |
| act_Content    | Long text   | N    |                  |
| act_Time       | varchar(20) | N    |                  |
| act_Pic        | text        | N    |                  |
| act_Url        | text        | N    |                  |

### 展览信息表：exhibition info table

图片

| 名称            | 类型        | 空   | 默认值           |
| --------------- | ----------- | ---- | ---------------- |
| exhib_ID(p_key) | int         | N    | <auto_increment> |
| muse_ID(f_key)  | int         | N    |                  |
| exhib_Name      | varchar(50) | N    |                  |
| exhib_Content   | Long text   | N    |                  |
| exhib_Pic       | text        | N    |                  |

### 新闻信息表：news info table

| 名称           | 类型         | 空   | 默认值           |
| -------------- | ------------ | ---- | ---------------- |
| news_ID(p_key) | int          | N    | <auto_increment> |
| muse_ID(f_key) | int          | N    |                  |
| news_Name      | varchar(255) | N    |                  |
| news_Content   | Long text    | N    |                  |
| news_type      | int          | N    |                  |
| news_time      | DataTime     | N    |                  |
| news_source    | varchar(20)  | N    |                  |

### 评论表：comment table

时间

| 名称           | 类型      | 空   | 默认值           |
| -------------- | --------- | ---- | ---------------- |
| com_ID(p_key)  | int       | N    | <auto_increment> |
| user_ID(f_key) | int       | N    |                  |
| muse_ID(f_key) | int       | N    |                  |
| com_Info       | Long text | Y    |                  |
| com_Time       | DataTime  | N    |                  |
| com_IfShow     | boolean   | N    | false            |

### 用户表：user table

头像（默认头像）

| 名称           | 类型        | 空   | 默认值           |
| -------------- | ----------- | ---- | ---------------- |
| user_ID(p_key) | int         | N    | <auto_increment> |
| user_Name      | varchar(50) | N    |                  |
| user_Phone     | varchar(20) | N    |                  |
| user_Passwd    | varchar(20) | N    |                  |
| user_Email     | varchar(20) | N    |                  |
| user_Avatar    | text        | N    | 默认图片         |
| if_com         | boolean     | N    | True             |

### 管理员表：admin table

| 名称            | 类型        | 空   | 默认值           |
| --------------- | ----------- | ---- | ---------------- |
| admin_ID(p_key) | int         | N    | <auto_increment> |
| admin_Name      | varchar(50) | N    |                  |
| admin_Passwd    | varchar(20) | N    |                  |

### 审核视频表：review video table

| 名称              | 类型       | 空   | 默认值           |
| ----------------- | ---------- | ---- | ---------------- |
| video_ID(p_key)   | int        | N    | <auto_increment> |
| muse_ID(f_key)    | int        | N    |                  |
| user_ID(f_key)    | int        | N    |                  |
| video_Url         | text       | N    |                  |
| video_IfShow      | boolean    | N    | False            |
| video_Name        | vachar(50) | N    |                  |
| video_Time        | DataTime   | N    |                  |
| video_Description | Long text  | N    |                  |

### 反馈表：feedback table

| 名称             | 类型 | 空   | 默认值           |
| ---------------- | ---- | ---- | ---------------- |
| fdback_ID(p_key) | int  | N    | <auto_increment> |
| muse_ID(f_key)   | int  | N    |                  |
| user_ID(f_key)   | int  | N    |                  |
| env_Review       | int  | N    |                  |
| exhibt_Review    | int  | N    |                  |
| service_Review   | int  | N    |                  |



### 关注表：attention table

| 名称           | 类型 | 空   | 默认值           |
| -------------- | ---- | ---- | ---------------- |
| att_ID(p_key)  | int  | N    | <auto_increment> |
| muse_ID(f_key) | int  | N    |                  |
| user_ID(f_key) | int  | N    |                  |































