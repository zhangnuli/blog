---
title: "使用eslint校验js语法"
date: 2019-07-16
permalink: "/webpack/使用eslint校验js语法"
meta:
  - name: description
    content: 一个热爱文学的伪程序猿，张努力，Node，webpack，JavaScript，爱好者，博客
  - name: keywords
    content: 一个热爱文学的伪程序猿，张努力，Node，webpack，JavaScript，爱好者，博客
---

# 使用eslint校验js语法

## 安装eslint和eslint-loader

- 要是用eslint，首先要安装eslint和eslint-loader插件

  `yarn add eslint eslint-loader -D`

- 在webpack.config.js里面增加一条规则

  ```javascript
  const path = require('path')
  const HtmlWebpackPlugin = require('html-webpack-plugin')
  const MiniCssExtractPlugin = require('mini-css-extract-plugin')
  const OptimizeCSSAssetsPlugin = require("optimize-css-assets-webpack-plugin")
  const UglifyJsPlugin = require('uglifyjs-webpack-plugin')
  
  module.exports = {
    optimization: {
      minimizer: [
        new OptimizeCSSAssetsPlugin(),
        new UglifyJsPlugin({
          cache: true,
          parallel: true,
          sourceMap: true
        }),
      ]
    },
    devServer: {
      contentBase: path.join(__dirname, 'dist'),
      compress: true,
      port: 3000,
      open: true,
      progress: true
    },
    entry: {
      index: './src/index.js'
    },
    output: {
      filename: '[name].js',
      path: path.resolve(__dirname, 'dist')
    },
  
    module: {
      rules: [
        {
          test: /\.css$/,
          use: [MiniCssExtractPlugin.loader, 'css-loader', 'postcss-loader']
        },
          //这是新增的规则
        {
          test: /\.js$/,
          exclude: /node_modules/,
          use: {
            loader: 'eslint-loader',
          }
        },
        {
          test: /\.js$/,
          exclude: /node_modules/,
          use: {
            loader: 'babel-loader',
          }
        }
      ]
    },
    plugins: [
      new MiniCssExtractPlugin({
        filename: "[name].css",
        chunkFilename: "[id].css"
      }),
      new HtmlWebpackPlugin({
        title: '测试',
        minify: false,
        template: path.resolve(__dirname, 'src/index.html'),
        chunks: ['index']
      })
    ]
  }
  ```



- 还可以写成这样

  ```javascript
  module.exports = {
    // ...
    module: {
      rules: [
        {
          test: /\.js$/,
          exclude: /node_modules/,
          use: ["babel-loader", "eslint-loader"]
        }
      ]
    }
    // ...
  };
  ```

  

- 安装好插件个配置好规则之后，我们还要在项目目录里创建一个**`.eslintrc.json`**文件

  ​	[**在线配置`.eslintrc.json地址**`](<https://cn.eslint.org/demo/>)

   - 示例`.eslintrc.json`

     ```javascript
     {
         "parserOptions": {
             "ecmaVersion": 5,
             "sourceType": "script",
             "ecmaFeatures": {}
         },
         "rules": {
             "no-useless-catch": 2,
             "no-useless-escape": 2,
             "no-with": 2,
             "require-atomic-updates": 2,
             "require-yield": 2,
             "use-isnan": 2,
             "valid-typeof": 2
         },
         "env": {}
     }
     ```

     

> 现在进行打包或者启动本地服务的时候，就会校验js语法了