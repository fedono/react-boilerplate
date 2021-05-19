# 如何做好一个项目的技术选型

> 这个 repo 主要是以 React 为核心，开始往周边拓展库的一个项目启动\
> 不同的技术方案，可以通过 Branch 来进行管理
> 参考 [awesome-react-boilerplate](https://linghucong.js.org/awesome-react-boilerplate/)

技术选型选好之后，可以建立一个 cli 的形式，通过选取每个方向对应的库来自动拉去npm包，这样就可以快速初始化了
包括 `.gitignore` 也可以自动生成，通过`fs`来写入文件生成嘛

## 主要的技术选项
- 编写JavaScript 选型：React
- 使用 TypeScript
- 接口请求 Axios
- 路由 react-router  
- 打包工具 Webpack 
- CSS 的选型
  - POST-CSS 好像用的挺少的
  - Less
  - SCSS
- 组件库 
  >需要调研一下，如何做数据验证，如何主题自定义，是否支持分包加载
  - antd 
- 数据管理
    - Mobx 
    - Redux + thunk
- 是否需要使用模板
- 是否需要使用后端渲染，如果需要，那么如何选择框架？Next？
- 常用的库，如 lodash / hooks相关的库  
- 设置代码规范 eslint
- 代码提交规范前检测 husky
- 文件目录规范