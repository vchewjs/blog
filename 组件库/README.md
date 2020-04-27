## UI组件库开发

### 目录
- [起步](#起步)
-- [安装Vue-cli](#全局安装-vue-cli)
-- [创建webpack模板](#创建一个基于-webpack-模板的新项目)
-- [安装依赖](#安装依赖)

### 起步
vue官方的脚手架

#### 全局安装 vue-cli

```
$ npm install --global vue-cli
```

#### 创建一个基于 webpack 模板的新项目

```
$ vue init webpack my-project
```

#### 安装依赖
```
$ cd my-project
```

```
$ npm install
```

```
$ npm run dev
```

目录结构,需要有一个目录存放组件，有一个目录存放示例。要对vue-cli 生成的项目结构改造：

```
.
...
|-- examples      // 原 src 目录，改成 examples 用作示例展示
|-- packages      // 新增 packages 用于编写存放组件
...
.
```
需要再把webpack配置文件稍作一下调整，把原先的编译指向src的目录改成examples，为了 npm run build 能正常编译 packages 需要为 babel-loader 增加一个编译目录：

```
{
   test: /\.js$/,
   loader: 'babel-loader',
   include: [resolve('examples'), resolve('test'), resolve('packages')]
}
```

如何编写文档,推荐使用 [VuePress](https://www.vuepress.cn/) 编写文档 按照官方文档配置相关的插件信息：

##### 现有项目
如果你想在一个现有项目中使用 VuePress，同时想要在该项目中管理文档，则应该将 VuePress 安装为本地依赖。作为本地依赖安装让你可以使用持续集成工具，或者一些其他服务（比如 Netlify）来帮助你在每次提交代码时自动部署。

```
# 将 VuePress 作为一个本地依赖安装
yarn add -D vuepress # 或者：npm install -D vuepress

# 新建一个 docs 文件夹
mkdir docs

# 新建一个 markdown 文件
echo '# Hello VuePress!' > docs/README.md

# 开始写作
npx vuepress dev docs
```

接着，在 package.json 里加一些脚本:

```
{
  "scripts": {
    "docs:dev": "vuepress dev docs",
    "docs:build": "vuepress build docs"
  }
}
```

然后就可以开始写作了:

```
yarn docs:dev # 或者：npm run docs:dev
要生成静态的 HTML 文件，运行：

yarn docs:build # 或者：npm run docs:build
```

默认情况下，文件将会被生成在 .vuepress/dist，当然，你也可以通过 .vuepress/config.js 中的 dest 字段来修改，生成的文件可以部署到任意的静态文件服务器上。

