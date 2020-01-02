（基于大牛的程序 https://github.com/moshang-xc/lottery.git 修改版: 新增启动图特效与结束图/新增2种抽奖特效/抽奖结果多行排列(最多50人)/增加奖品项/中间隐式抽取现金红包奖）
# 抽奖程序

年会抽奖程序，3D 球体抽奖，支持奖品信息配置，参与抽奖人员信息`Excel`导入，抽奖结果`Excel`导出

> github 地址： [https://github.com/wackyJ/3Dlottery.git](https://github.com/wackyJ/3Dlottery.git)

## 技术

技术：Node + Express + Three.js

后台通过`Express`实现

前端抽奖界面通过`Three.js`实现 3D 抽奖球，引用了`Three.js`的官方 3D 示例

## 功能描述：

1. 可将抽奖结果进行保存实时下载到 excel 中(修改excel表中结果为奖品名,方便后续核对分发)
2. 已抽取人员不在参与抽取，抽中的人员不在现场可以重新抽取
3. 刷新或者关掉服务器，会保存当前已抽取的数据，不会进行数据重置，只有点击界面上的重置按钮，才能重置抽奖数据
4. 每次抽取的奖品数目可配置
5. 抽取完所有奖品后还可以继续抽取特别奖(例如：现在抽取红包，追加的奖品等)，此时默认一次抽取一个
6. 启动图动态特效,结束图点击"结束"按钮全屏显示,双击隐藏
7. 抽奖结果修改为每10个显示一行,目前最多支持单次50人
8. 抽奖奖项中间穿插隐式奖项
9. 在球体与表格特效基础上新增helix/grid特效
10. 增加键盘事件:
        "+"     导出抽奖结果
        "-"      展示结束图
        "space"   保存当前抽奖结果
        "enter"   抽奖


## 预览

![lottery.gif](https://user-gold-cdn.xitu.io/2019/12/21/16f28430af77f511?imageslim)

![f.jpg](https://user-gold-cdn.xitu.io/2019/12/21/16f28467c001de03?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

![s.jpg](https://user-gold-cdn.xitu.io/2019/12/21/16f28469503664c1?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

![t.jpg](https://user-gold-cdn.xitu.io/2019/12/21/16f2846b50983782?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

## 安装

```
git clone https://github.com/wackyJ/3Dlottery.git

cd lottery

# 服务端插件安装
cd server
npm install

# 前端插件安装
cd ../product
npm install

# 打包
npm run build

# 运行
npm run serve

# 开发调试
npm run dev

```

## 目录结构

```
Lottery
├── product
│   ├── src
│   │   ├── lottery
│   │   │   └── index.js
│   │   ├── lib
│   │   ├── img
│   │   ├── css
│   │   └── data
│   ├── package.json
│   └── webpack.config.js
├── server
│   ├── config.js
│   ├── server.js
│   └── package.js
```

> 1. product 为前端页面目录
> 2. package.josn web 项目配置文件
> 3. webpack.config.js 打包配置文件
> 4. server 为服务器目录
> 5. config 为奖品信息的配置文件

## 配置信息

1. 抽奖用户信息，按指定的格式填写在`server/data/user.xlsx`文件中，不能修改文件名

2. 奖品的配置信息填写在`server/config.js`文件中，不能修改文件名

```js
// 奖品信息，第一项为预留项不可修改，其他项可根据需要修改
let prizes = [{
        type: 0,
        count: 1000,
        title: '特别奖',
        img: ''
    }, {
        type: 1,
        count: 1,
        title: '华为Mate 20X',
        img: '../img/huawei.png'
    }
    ...
];

/**
 * 一次抽取的奖品个数
 * 顺序为：[特别奖，一等奖，二等奖，三等奖，四等奖，五等奖]
 */
const EACH_COUNT = [1, 1, 1, 1, 1, 5];
// 公司名称，用于显示在抽奖名单的title部分
const COMPANY = 'MoShang';
```
