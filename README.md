### 简介
目前，这是一个**微信推送生日信息**的项目，每早7.30扫描最近7天过生日的好友并进行微信推送。

![微信推送][1]

迫于有时自己生日别人会来电、短讯之类，别人生日自己却记不住，十分恼火。

之前用的 **生日某家app** 还算能满足需求，但是后面强行上电商、资讯这些玩意，而且经常 **推送辣鸡广告**，原本的生日推送都不能正常使用 本末倒置，索性关闭推送，当记事本用了。

想到自己每天都在用微信，弄个微信推送生日信息应该就能提前看到了~

### 用到的东西
主要使用： Node + [Server酱][2]，建议搭配pm2来使用

注册Server酱账号、扫码绑定微信号、关注接收消息的公众号、**获取发送消息的url**
### 使用方法
#### 步骤1
```
git clone https://github.com/LonHon/birth-manage.git
```
#### 步骤2
data/ 下添加data.json，格式如下(type:0或空为农历，1为公历)：
```
[
    {"name":"女朋友A","birth":"2000/9/8", "type": 1},
    {"name":"女朋友B","birth":"2000/9/9"},
    {"name":"女朋友C","birth":"2000/9/10", "type": 0}
]
```
#### 步骤3
func/scaner.js 中添加Server酱发送消息的url

#### 步骤4
```
npm install

node index.js
```
这里可以先在index.js中注释关闭定时器，检测是否能正常发送消息.

#### 项目代码主要功能：
1. data/data.json 提供生日数据
2. func/scaner.js 扫描生日数据，提取7天内过生日的数据。
![scaner][3]
3. func/senter.js 调用Server酱，实现消息发送
4. index.js 开启定时任务，每天早上7.30扫描并推送

#### Server酱主要功能
提供微信推送功能，这样就不用自己去搞一个公众号再配置了.

### 最后

> 车遥遥，马憧憧，君游东山东复东。

可以提供免费挂服务，限10位，需要的可以把Server酱的key和data.json发到我的邮箱 lonhontop@gmail.com

TODO：
* [x] 1. 目前只有农历生日判断，需添加一个公历生日的判断
* [ ] 2. 做个分级？比如A级，提前7天提醒，B级提前3天，C级当天提醒。


  [1]: https://i.loli.net/2018/10/19/5bc979a5a5253.png
  [2]: https://sc.ftqq.com/3.version
  [3]: https://i.loli.net/2018/10/19/5bc989a14e9f5.png