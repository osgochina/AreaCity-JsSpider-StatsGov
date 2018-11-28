# 省市区数据采集并标注拼音

## 采集环境

chrome控制台。


## 数据源

国家统计局 > 统计数据 > 统计标准 > [统计用区划和城乡划分代码](http://www.stats.gov.cn/tjsj/tjbz/tjyqhdmhcxhfdm/)


## 采集深度

- 2018文件夹采集了3层，省、市、区，[2017版数据](http://www.stats.gov.cn/tjsj/tjbz/tjyqhdmhcxhfdm/2017/index.html)。
- 2017文件夹采集了3层，省、市、区，[2016版数据](http://www.stats.gov.cn/tjsj/tjbz/tjyqhdmhcxhfdm/2016/index.html)。
- 2013文件夹采集了4层，省、市、区、镇，[2013版数据](http://www.stats.gov.cn/tjsj/tjbz/tjyqhdmhcxhfdm/2013/index.html)。


## 拼音标注

重庆能正常标注成`chong qing`。

从完整拼音中提取的拼音前缀，取的是第一个字前两个字母和后两个字首字母，意图是让第一个字相同名称的尽量能排序在一起。排序1：`黑龙江helj、湖北hub、湖南hun`；排序2：`湖北hb、黑龙江hlj、湖南hn`，排序一胜出。


## 数据问题

1. id编号和国家统计局的编号基本一致，方便以后更新，有很多网站接口数据中城市编号是和这个基本是一致的。

2. id重复项目前是没有（已优化过了），不过以前采集（2013版）后直接对统计局的编号进行简单缩短后会有重复现象（算是精度丢失）。

3. 因为区名字是直接去掉市、区等后缀，可能存在那么几对同一城市下但名字变得完全一样的~~（`622901000000: 临夏市, 622921000000: 临夏县, 653201000000: 和田市, 653221000000: 和田县, 654002000000: 伊宁市, 654021000000: 伊宁县`）（2017版已修复这几个）~~，如果发现，需要手动把市区后缀加上，不然会产生问题。

4. 2017版开始数据结尾添加了自定义编号的港澳台、海外数据。


## js使用方法

在chrome控制台内运行1、2、3打头的文件即可完成采集，前提是指定网页打开的控制台。这三个文件按顺序执行。

### 步骤1

1. 打开国家统计局任意页面，如：http://www.stats.gov.cn/tjsj/tjbz/tjyqhdmhcxhfdm/。
2. 执行`1_抓取国家统计局城市信息.js`内代码。
3. 采集完成自动弹出下载，保存得到文件`data.txt`。

### 步骤2

1. 打开拼音接口页面，具体看`2_抓取拼音.js`开头注释。
2. 复制`data.txt`内容到控制台执行，数据完成导入。
3. 执行`2_抓取拼音.js`内代码。
4. 拼音采集完成自动弹出下载，保存得到文件`data-pinyin.txt`。

### 步骤3

1. 任意页面，最好是第二步这个页面。
2. 复制`data-pinyin.txt`内容到控制台执行，数据完成导入。
3. 执行`3_格式化.js`内代码。
4. 格式化完成自动弹出下载，保存得到最终文件`ok_data.csv`。
