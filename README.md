# 链家网爬虫
### 功能介绍
- 获取链家网小区房价数据。支持Python2和Python3，如果好用，请star。
- 城市 city, 区县 district, 板块 area, 小区 xiaoqu。
- 每个版块一个csv文件。
- 内容格式：采集日期,所属区县,板块名,小区名,挂牌均价,挂牌数
- 内容如下：20180221,浦东,川沙,恒纬家苑,32176元/m2,3套在售二手房
- 数据可以存入MySQL/MongoDB数据库，用于进一步数据分析，比如排序，计算区县和版块均价。
- MySQL数据格式: 城市 日期 所属区县 版块名 小区名 挂牌均价 挂牌数
- MySQL数据内容：上海 20180331 徐汇 衡山路 永嘉路621号 333333 0
- MongoDB数据内容: { "_id" : ObjectId("5ac0309332e3885598b3b751"), "city" : "上海", "district" : "黄浦", "area" : "五里桥", "date" : "20180331", "price" : 81805, "sale" : 11, "xiaoqu" : "桥一小区" }
- Excel数据内容：上海 20180331 徐汇 衡山路 永嘉路621号 333333 0

### 运行
- 将环境变量PYTHONPATH设置为当前目录
- python xiaoqu.py 根据提示输入城市代码，回车确认，开始采集数据到csv文件
```
hz: 杭州, sz: 深圳, dl: 大连, fs: 佛山
xm: 厦门, dg: 东莞, gz: 广州, bj: 北京
cd: 成都, sy: 沈阳, jn: 济南, sh: 上海
tj: 天津, qd: 青岛, cs: 长沙, su: 苏州
cq: 重庆, wh: 武汉, hf: 合肥, yt: 烟台
nj: 南京, 
```
- 修改 to_database.py 中的database变量，设置数据最终存入mysql/mongodb/Excel
- python to_database.py 根据提示将今天采集到的csv数据存入数据库

### 性能
- 300秒爬取上海市207个版块的2.7万条数据，平均每秒90条数据。
```
Total crawl 207 areas.
Total cost 294.048109055 second to crawl 27256 data items.
```

### 结果存储
- 根目录下建立data目录存放结果数据文件
- 存储目录为 data/lianjia/city/date
- MySQL数据库结构可以通过导入lianjia_xiaoqu.sql建立。

### 更新记录
- 2018/04/02 支持将采集到的csv数据导入Excel
- 2018/04/01 同时支持Python2和Python3
- 2018/04/01 支持将采集到的csv数据导入MongoDB数据库
- 2018/03/31 支持将采集到的csv数据导入MySQL数据库
- 2018/03/27 修复bug: 版块下只有一页小区数据时未能正确爬取 
- 2018/03/27 增加5个城市，现在支持21个城市的小区数据爬取
- 2018/03/10 自动获取城市的区县列表，现在支持16个城市小区数据爬取
- 2018/03/06 支持北京二手房小区数据采集
- 2018/02/21 应对链家前端页面更新，使用内置urllib2代替第三方requests库,提升性能，减少依赖
- 2018/02/01 支持上海二手房小区数据采集

