# 如何做好一个项目的技术选型

> 这个 repo 主要是以 React 为核心，开始往周边拓展库的一个项目启动\
> 不同的技术方案，可以通过 Branch 来进行管理
> 参考 [awesome-react-boilerplate](https://linghucong.js.org/awesome-react-boilerplate/)

技术选型选好之后，可以建立一个 cli 的形式，通过选取每个方向对应的库来自动拉去npm包，这样就可以快速初始化了
包括 `.gitignore` 也可以自动生成，通过`fs`来写入文件生成嘛ls

## 主要的技术选项
- 编写JavaScript 选型：React

    - 选型 React 和 VUE 的区别

- 使用 TypeScript

- 接口请求 Axios

- 路由 react-router  

- 打包工具 Webpack 

- CSS 的选型

  > 说一下 less / css-in-js / css module 的区别

  - POST-CSS 好像用的挺少的
  - Less
  - SCSS
  

- 组件库 
  >需要调研一下，如何做数据验证，如何主题自定义，是否支持分包加载
  > 1. 是否长期维护，提交频率是否频繁
  > 2. 组件是否完善
  > 3. 自定义程序是否完善
  > 4. 是否支持分包，主题自定义
  > 5. 
  - antd 
  
- 数据管理
    - Mobx 
    - Redux + thunk / saga
    
- 是否需要使用模板

- 是否需要使用后端渲染，如果需要，那么如何选择框架？Next？

- 常用的库，如 lodash / hooks相关的库  

- 设置代码规范 eslint

- 代码提交代码规范前检测 husky

- 代码提交的commit 检测 [commitlint](https://github.com/conventional-changelog/commitlint)

- 文件目录规范

- npm 的开发规范

    - init 初始化项目
    - Compile 编译
    - start 启动项目
    - Docs 项目文档
    - test 测试
    - publish 发布

- 还有什么最佳实践可以看看
- 代码提交规范前检测 husky

- 文件目录规范



## 哪些配置是和业务选型有关的，哪些是和业务类型无关的

- 和业务类型有关
  - 是否采用 服务端渲染
  - 组件库选型
