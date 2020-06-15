

[webapck]('https://www.webpackjs.com/')

## 安装

```javascript
mkdir project
cd project
npm init
npm install webpack webpack-cli --save-dev
```

Package.json

```javascript
{
  "name": "my-project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack"
     // 通过 npm run build 运行构建原理：模块局部安装会在 node_modules/.bin 目录创建软连接
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "webpack": "^4.43.0",
    "webpack-cli": "^3.3.11"
  }
}

```



## 核心概念

### entry

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

### output

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

### loaders

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

### plugins

> 插件用于bundle文件的优化，资源管理和环境变量的注入，作用于整个构建过程

| 名称                                                         | 描述                                  |
| ------------------------------------------------------------ | ------------------------------------- |
| [CommonsChunkPlugin]('https://www.webpackjs.com/plugins/commons-chunk-plugin') | 提取 chunks 之间共享的通用模块        |
| [ExtractTextWebpackPlugin](https://www.webpackjs.com/plugins/extract-text-webpack-plugin) | 从 bundle 中提取文本（CSS）到单独的文 |
| [`CopyWebpackPlugin`](https://www.webpackjs.com/plugins/copy-webpack-plugin) | 将单个文件或整个目录复制到构建目      |
| [`HtmlWebpackPlugin`](https://www.webpackjs.com/plugins/html-webpack-plugin) | 简单创建 HTML 文件，用于服务器访问    |

```javascript

```

### mode

> 指定当前构建环境是：production、development、 none
>
> 设置mode，可以使用webpack内置函数，默认是production

| 选项        | 描述                                                         |
| ----------- | ------------------------------------------------------------ |
| development | 会将 `process.env.NODE_ENV` 的值设为 `development`。启用 `NamedChunksPlugin` 和 `NamedModulesPlugin`。 |
| production  | 会将 `process.env.NODE_ENV` 的值设为 `production`。启用 `FlagDependencyUsagePlugin`, `FlagIncludedChunksPlugin`, `ModuleConcatenationPlugin`, `NoEmitOnErrorsPlugin`, `OccurrenceOrderPlugin`, `SideEffectsFlagPlugin` 和 `UglifyJsPlugin`. |
| none        | 不开启任何优化                                               |

## 常用的解析

- 解析es6

  > 使用babel-loader解析，babel的配置文件是.babelrc

  ```javascript
  npm i @babel/core @babel/preset-env babel-loader -D  // es6相关preset
  npm i react react-dom @babel/preset-react -D // react相关preset
  ```

  ```javascript
  .babelrc 文件
  {
    "presets" :[
      "@babel/preset-env"
    ]
  }
  ```

  ```javascript
  webpack.config.js 文件
  module: {
    rules: [
      {
        test: /.js$/,
        use: "babel-loader"
      }
    ]
  }
  ```

- 解析css,less和scss

  > css-loader用于加载css文件，并且转化成commonjs对象
  >
  > style-loader 将样式通过style标签插入到head中

  - 解析css

  > npm i css-loader style-loader -D

  ```javascript
  module: {
    rules: [
      {
        test: /.css$/,
        use: ['style-loader','css-loader']
      }
    ]
  }
  ```

  - 解析less

  > Nom i less less-loader -D

  ```javascript
  module: {
    rules: [
      {
        test: /.less$/,
        use: ['style-loader', 'css-loader', 'less-loader']
      }
    ]
  }
  ```

- 解析图片以及字体

  > file-loader, 用于处理文件
  >
  > Url-loader 也可以处理图片跟字体，可以设置较小资源，自动base64

  ```javascript
  // file-loader
  {
    test: /.(png|jpg|gif|jpeg)$/,
      use: 'file-loader'
  },
    {
      test: /.(woff|woff2|eot|ttf|otf)$/,
        use: 'file-loader'
    }
  // url-loader
  {
    test: /.(woff|woff2|eot|ttf|otf)$/,
      use: [
        {
          loader: 'url-loader',
          options: {
            limit: 10240 // limit: 资源大小限制，小于limit，会自动base64
          }
        }
      ]
  }
  ```
- 文件监听
> 文件监听是在发现源码发生变化时，自动重新构建出新的输出文件
>
> 缺陷：每次需要手动刷新浏览器
>
> 开启方式：
>
>  - 启动webpack命令时，带上--watch参数
>  - 在webpack.config.js中设置watch:true

​	原理分析

```javascript
// 轮询的判断文件最后的是修改时间是否发生变化，某个文件发生变化，并不会立即告诉监听者，而是先缓存起来，等aggregateTimeout,期间有别的文件发生改变，一起打包
module.export = {
  // 默认是false，不开启
  watch: true，
  watchOPtions:{
  	// 默认为空，不监听的文件或者文件夹
  	ignored: /node_modules/,
  	// 监听到变化后300ms后再去执行，默认时300
  	aggregateTimeout: 300,
    // 判断文件是否发生变化时通过不停询问系统指定文件有没有变化实现的，默认每秒1000次
  	poll: 1000
	}
}
```

- webpack热更新及原理

> 热更新(WDS)： webpack-dev-server，不刷新浏览器；不输出文件，而是放在内存中，使用HotModuleReplacementPlugin插件
>
> npm i webapck-dev-server -D

```javascript
// package.json
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack --watch",
    "dev": "webpack-dev-server --open"
  },
 // webpack.config.js
    const webpack = required('webpack')
    plugins: [
      new webpack.HotModuleReplacementPlugin()
    ],
    devServer: {
      contentBase: './dist',
      hot: true
    }
```

![热更新原理](https://qiniu-admin.51beauty.com.cn/1592106073803614)

- 文件指纹

> 对打包生成的静态资源进行版本的区分
>
> Hash:和整个项目的构建相关，只要项目有修改，整个项目构建的hash值就会更改
>
> Chunkhash:和webpack打包的chunk有关，不同的entry会生成不同的Chunkhash值
>
> Contenthash: 根据文件内容来定义hash，文件内容不变，则Contenthash值不变  一般用于css

| 占位符       | 含义                          |
| ------------ | ----------------------------- |
| [ext]        | 资源后缀名                    |
| [name]       | 文件名                        |
| [path]       | 文件路径                      |
| [folder]     | 文件所在的文件夹              |
| [contenhash] | 文件内容的hash，一般由md5生成 |
| [hash]       | 文件内容的hash，一般由md5生成 |
| [emoji]      | 一个随机指代文件内容的emoji   |

 1.为js设置hash,在output指定hash方式

```javascript
output: {
    path: path.join(__dirname, 'dist'),
    filename: '[name]_[chunkhash:8].js'   // chunkhash:8   chunkhash由md5生成32位字符， :8 取前8位
  },
```

2. 为图片等资源进行hash

   ```javascript
   {
     test: /.(png|jpg|gif|jpeg)$/,
       use: [
         {
           loader: 'file-loader',
           options: {
             name: '[name]_[hash:8].[ext]'
           }
         }
       ]
   },
   ```

3. 为css进行hash

   > 需要用到mini-css-extract-plugin 插件  作用：将css文件单独提取出来，需配置其laoder
   >
   > npm i mini-css-extract-plugin -D

   ```javascript
   const MiniCssExtrsctPligin = require('mini-css-extract-plugin')
   module: {
       rules: [
         {
           // style-loader 是将样式插入到head头部，与MiniCssExtrsctPligin.loader作用相悖
           test: /.css$/,
           use: [MiniCssExtrsctPligin.loader, 'css-loader']
         },
         {
           test: /.less$/,
           use: [MiniCssExtrsctPligin.loader, 'css-loader', 'less-loader']
         }
       ]
     },
   plugins: [
       new MiniCssExtrsctPligin({
         filename: '[name]_[contenthash:8].css'
       })
     ]
   ```

- 代码压缩

  > webpack内置了[`UglifyjsWebpackPlugin`](https://www.webpackjs.com/plugins/uglifyjs-webpack-plugin)插件，打包好的代码会自动压缩

  - css压缩

    ```javascript
    // 使用optimize-css-assets-webpack-plugin,同时使用cssnano
    // npm i optimize-css-assets-webpack-plugin -D
  // npm i cssnano -D
    const optimizeCssAssetsWebpackPlugin = require('optimize-css-assets-webpack-plugin')
  plugins: [
      new optimizeCssAssetsWebpackPlugin({
        assetNameRegExp: /\.css$/g,
        cssProcessor: require('cssnano')
      })
    ]
    ```
  
  - html压缩
  
    ```javascript
    // 使用html-webpack-plugin,设置压缩参数
    // npm i html-webpack-plugin
    new htmlWebpackPlugin({
      template: path.join(__dirname, 'src/index.html'), // 模版所在位置
      filename: "index.html", // 打包后的文件名
      chunks: ['index'], // 生成的html使用的chunk
      inject: true, // true/；打包生成的chunk自动注入html
      minify: {
        html5: true,
        collapseWhitespace: true,
        preserveLineBreaks: false,
        minifyCSS: true,
        minifyJS: true,
        removeComments: false
      }
    }),
    ```

## 进阶

- 自动清理构建产物

  > npm i clean-webpack-plugin -D

  ```javascript
  const {CleanWebpackPlugin} = require('clean-webpack-plugin');
  plugins: [
    new CleanWebpackPlugin()
  ]
  ```


- 自动补全css前缀

  > npm i postcss-loader autoprefixer -D

  ```javascript
  {
    test: /.less$/,
      use: [
        MiniCssExtrsctPlugin.loader,
        'css-loader', 
        'less-loader',
        {
          loader: 'postcss-loader',
          options: {
            plugins: () => [
              require('autoprefixer')({
                browsers: ['last 2 versions', '>1%', 'ios 7']
              })
            ]
          }
        }]
  },
  ```

  