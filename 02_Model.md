# 要做什麼
常常學東西時都從基礎開始, 基礎就是JavaScript, 但上完課是能寫出什麼東西呀? 我認為學開發要先廣而深, 所以我們先從要寫什麼東西開始, 再看看我們到底需要什麼技術, 再針對需要的技術深入研究, 所以在一開始就已經看到了JavaScript, NodeJS, Express, Gulp, Git, GitHub, Atom, 那第一支程式當然不該是Hello World, 而是資料庫的CRUD該如何實作, 接下來我們要從Model開始.
# MongoDB
我們資料庫選用的是MongoDB, 依官網安裝成Windows Service
# 命名規則
目錄名稱,檔案名稱全部小寫再加上特定字尾以區別,例如stockModel.js.
程式變數,型別全部小寫,但資料庫以除了_id外一律採Pascal命名
# 建立Model
`新增models/stockModel.js`
```javascrip
var mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/test', function(err){
  if(err) console.log('連線失敗');
  else console.log('連線成功');
});
module.exports = mongoose.model('Stock',{
  _id: {type: Number}  ,
  Name: {type: String}
});
```
```shell
>npm install --save mongoose
```
# 解釋
1. 資料庫要連線所以mogoose.connect()
2. 要建立Schema放到Model裡所以mongoose.model()
3. module.exports是NodeJS裡給require用的

# 建立Route實作REST進行CRUD
`新增routes/stockRoute.js`
```javascript
var express = require('express');
var stock = require('../models/stockModel');
var router = express.Router();
router.get('/api',function(req, res, next){
  stock.find(function(err, data){
    if(err) return next(err);
    res.json(data);
  });
});
module.exports = router;
```
# 設定route
`修改app.js`
```javascript
var stock = require('./routes/stockRoute');
app.use('/stock',stockRoute);
```
# 驗收
```shell
>curl http://localhost:3000/stock/api
```
# 解釋
1. route就是MVC架構裡的Controller, 所以要先建立stockRoute.js來處理get需求.
2. app.js是核心, 設定/stock的需求要由stockRoute來處理.
3. 沒資料, 結果應該是[]
