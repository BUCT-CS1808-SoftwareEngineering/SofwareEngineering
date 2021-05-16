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

