## 核心概念

1. entry

   > 指定webpack打包的入口

   ```javascript
   // 单入口
   module.exports = {
   	entry:'./src/main.js'
   } 
   // 多入口
   module.exports = {
       entry:{
           app:'./src/app.js',
           app1:'./src/app1.js',
       }
   } 
   ```

2. output

   > 指定打包的输出

   ```javascript
   const path = require('path')
   module.exports = {
       entry:{
           app:'./src/app.js',
           app1:'./src/app1.js',
       },
       output:{
           path:path.resolve(__dirname + '/dist'),  // 要求是绝对路径
           filename:'[name].js', // [name] -> 占位符,多个入口为避免文件名重复，用占位符来保证文件名不重复
           publicPath:'./dist/'
     },
   } 
   ```

3. loaders

   > webpack只支持js,json，loaders将其他类型的文件转化为有效的模块

   ```javascript
   module:{
       rules:[
           {
               test: /\.css$/, // 解析css文件的loader
               // css-loader 只负责css文件加载，不负责渲染页面
               // style-loader 负责将css添加到dom
               // webpack 使用多个loader时，从右往左读取
               use: ['style-loader','css-loader']
         },
       ]
   }
   ```

   

4. plugins

5. mode