## 博物馆网站数据采集子系统

### 1. 小组分工

根据子系统的功能要求，大致分成需求分析、初步设计、设计细化、代码实现、测试完善这五个步骤。目前大家首先是协作完成需求分析和设计，这样能够让每个成员都能理解所要开发的系统。之后大家会针对性地学习项目技术知识，在代码实现、测试方面再进一步分工。贯穿整个过程的文档，会根据每个人的任务情况适当分工。

| 任务     | 负责人                |
| -------- | --------------------- |
| 文档编写 | 姚畅 纪鹏飞 袁鹏 何雨 |
| 编码     | 姚畅 郑博文 姜哲玺    |
| 测试     | 姚畅 郑博文           |

我们组内暂时不细分具体的任务，大家开始先学习python基础知识，4.19号之前完成该任务。4.19号之后看情况具体细分编程任务。周记的撰写，大家轮流。其他文档，看情况具体再分，大家协作完成。

### 2. 时间规划

暂定如下

| 时间     | 任务                                                 |
| -------- | ---------------------------------------------------- |
| 第六周   | 完成项目管理计划                                     |
| 第七周   | 完成需求分析，学习使用scrapy爬虫框架                 |
| 第八周   | 继续学习爬虫并且爬取数据，完成需求规格说明书         |
| 第九周   | 对爬取的数据进行情感分析和信息提取，完成设计报告初稿 |
| 第十周   | 将数据导入到数据库                                   |
| 第十一周 | 对系统进行优化                                       |
| 第十二周 | 子系统运行检查                                       |

### 3. 需求分析

博物馆新闻采集子系统，主要爬取目前几大主流新闻网站上的博物馆新闻信息，包括百度新闻、网易新闻、新浪新闻、澎湃新闻、凤凰网、搜狐新闻等，然后对爬取到的新闻内容进行情感分析，判断其褒贬性，将处理后的数据存入数据库中。

#### 功能需求：

- 数据获取功能
  - 数据
    - 主流新闻网站上的博物馆新闻信息，包括博物馆名称、新闻标题、新闻时间、新闻来源、新闻内容、新闻内容的褒贬性等。
  - 实现方法
    - python Scrapy框架进行数据爬取
    - python的情感分析库（可选项包括vader、jieba、NLTK）
- 数据加工功能
  - 加工要求
    - 对数据进行加工分析，去除不必要的信息，并且对新闻内容进行情感分析并且得出其褒贬性
  - 实现方法
    - python的情感分析库（可选项包括vader、jieba、NLTK、bixin、snownlp、cnsenti）
- 数据导入功能
  - 导入要求
    - 将加工筛选好的数据存入数据库，方便其他小组使用相关的信息。
  - 实现方法
    - Python-pymysql
    - MySQL
    - Scrapy框架
    - bixin
    - jieba
    - 部署到服务器

#### 性能需求

- 安全需求
  - 系统在传输数据时，必须保证数据的安全性。
  - 系统所提供的数据，必须符合道德伦理及法律要求。
- 可靠性需求
  - 支持大规模数据存储
  - 所有的数据都来自官方网站，以确保数据的正确性
- 开放性需求
  - 系统应具有十分的灵活性，以适应将来功能扩展的需求。
- 系统安全性需求
  - 系统有严格的权限管理机制，有权限者方能进入修改程序和数据。

### 4. 工程结构

```
│  .gitignore
│  README.md
│  scrapy.cfg
│
├─Document
└─NewsPro
    │  begin.py
    │  chromedriver.exe
    │  emo_an.py
    │  getsubstr.py
    │  get_muselist.py
    │  get_News_muse.py
    │  initial.json
    │  items.py
    │  middlewares.py
    │  muselist.xlsx
    │  pipelines.py
    │  processed_html.py
    │  requirements.txt
    │  settings.py
    │  time_process.py
    │  __init__.py
    │
    ├─spiders
    │  │  Baidu.py
    │  │  BaijiaHao.py
    │  │  latest_url.json
    │  │  NetEase.py
    │  │  Sina.py
    │  │  __init__.py
    │  │
    │  └─__pycache__
    │          Baidu.cpython-37.pyc
    │          BaijiaHao.cpython-37.pyc
    │          NetEase.cpython-37.pyc
    │          Sina.cpython-37.pyc
    │          __init__.cpython-37.pyc
    │
    └─__pycache__
            emo_an.cpython-37.pyc
            getsubstr.cpython-37.pyc
            get_muselist.cpython-37.pyc
            items.cpython-37.pyc
            middlewares.cpython-37.pyc
            pipelines.cpython-37.pyc
            processed_html.cpython-37.pyc
            settings.cpython-37.pyc
            time_process.cpython-37.pyc
            __init__.cpython-37.pyc
```
### 5.功能详细说明

#### 数据爬虫：

- Baidu.py ->百度新闻爬虫：
  - 可链接到澎湃新闻、腾讯新闻、搜狐新闻、网易新闻、凤凰新闻等多个平台[百度资讯搜索_博物馆 (baidu.com)](https://www.baidu.com/s?ie=utf-8&medium=1&rtt=1&bsst=1&rsv_dl=news_t_sk&cl=2&wd=博物馆&tn=news&rsv_bp=1&tfflag=0)
  - 爬取的数据包括：新闻标题、新闻URL、新闻时间、新闻来源、新闻内容、新闻主体源代码
- BaijiaHao.py ->百度百家号爬虫：
  - 对百度新闻的百家号模块进行数据爬取[百度资讯百家号搜索_博物馆 (baidu.com)](https://www.baidu.com/s?ie=utf-8&medium=2&rtt=1&bsst=1&rsv_dl=news_t_sk&cl=2&wd=博物馆&tn=news&rsv_bp=1&tfflag=0)
  - 爬取的数据包括：新闻标题、新闻URL、新闻时间、新闻来源、新闻内容、新闻主体源代码
- NetEase.py —>网易新闻爬虫：
  - 网易新闻的博物馆页面新闻爬取[越艺术 悦生活_网易艺术 (163.com)](https://art.163.com/museum)
  - 爬取的数据包括：新闻标题、新闻URL、新闻时间、新闻来源、新闻内容、新闻主体源代码
- Sina.py —>新浪新闻爬虫[新闻中心首页_新浪网 (sina.com.cn)](https://news.sina.com.cn/)
  - 新浪新闻的博物馆页面新闻爬取
  - 爬取的数据包括：新闻标题、新闻URL、新闻时间、新闻来源、新闻内容、新闻主体源代码

#### 数据处理：

- time_process.py ->对爬取到的时间信息进行处理

  - 澎湃新闻、腾讯新闻、搜狐新闻、网易新闻、凤凰新闻、百家号、新浪新闻的时间格式各有不同
  - 通过正则表达式对时间格式进行处理

- processed_html.py ->新闻网页源代码内容的处理文件

  - 由于要保存新闻网页原本图片与内容的相对格式，我们爬取的是新闻网页的主体HTML代码

  - 由于新闻HTML代码主体内容中存在多种标签，前端不方便使用，我们可以将带有文字的标签改成P标签，供前端统一调试css样式
  - 使用正则表达式替换标签供前端使用

- get_muselist.py ->获取博物馆列表文件

  - 读取博物馆excel列表，形成博物馆列表

- getsubstr.py ->处理url获取子串文件

  - 通过观察网页中爬取到的URL可能含有多余信息，使用该函数可得到所需子串

- emo_an.py —>新闻文本情感分析文件

  - 对爬取到的新闻内容和新闻标题进行情感分析
  - 新闻包括消极、积极和中性三种

#### 数据持久化存储：

- pipelines.py ->管道文件
  - 进行数据库的连接以及数据的存入
  - 在测试时可使用管道文件将数据存储到本地txt或者json文件中

#### 其他：

- middlewares.py ->scrapy 中间件文件
  - 通过观察，我们发现网页中存在Ajax动态加载网页，查询后可使用selenium Web自动化工具进行数据获取
  - 我们可使用scrapy的中间件中的下载中间件对特定请求进行拦截、使用chromeDriver进行模拟访问，返回响应

