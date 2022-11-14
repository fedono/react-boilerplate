# 关于 CSS 的技术选型

CSS 本身有不少缺陷，如书写繁琐（不支持嵌套）、样式易冲突（没有作用域概念）、缺少变量（不便于一键换主题）等不一而足

> less 和 sass 如果要比较区别，肯定不是写法，写法其实是比较不重要的一个环节，重要的是解决了什么问题，less 解决的问题，sass 不能解决，比如sass需要 node-sass 来编译，但是 node-sass 一直出问题，这个就是劣势，（但其实这也是很小的一个劣势，



能够选择的类型

- less
- scss
- [postcss](https://postcss.org/)
- [css module](https://github.com/css-modules/css-modules)
- css in js
- 

## 各选型的优劣
### css module

> A **CSS Module** is a CSS file in which all class names and animation names are scoped locally by default. All URLs (`url(...)`) and `@imports` are in module request format (`./xxx` and `../xxx` means relative, `xxx` and `xxx/yyy` means in modules folder, i. e. in `node_modules`).

**特性：**

- **作用域**：模块中的名称默认都属于本地作用域，定义在 `:local` 中的名称也属于本地作用域，定义在 `:global` 中的名称属于全局作用域，全局名称不会被编译成哈希字符串。
  - 将 css 代码模块化，可以避免本模块样式被污染。并且可以很方便的复用 css 代码。
- **命名**：对于本地类名称，CSS Modules 建议使用 camelCase 方式来命名，这样会使 JS 文件更干净，即 `styles.className`。
  但是你仍然可以固执己见地使用 `styles['class-name']`，允许但不提倡。🤪
- **组合**：使用 `composes` 属性来继承另一个选择器的样式，这与 Sass 的 `@extend` 规则类似。
- **变量**：使用 `@value` 来定义变量，不过需要安装 PostCSS 和 [postcss-modules-values](https://link.segmentfault.com/?enc=HURvIn54oEQ0RpoTNCE5VQ%3D%3D.RbfT6jmUFPVMhaREGevo1dSw0%2BqSoy3e48mgiFd%2ByoAS52Cz9P8DaT9JaFDwVVZjbeoWGqZdSDl%2FtKlG%2F%2BmudQ%3D%3D) 插件。



用法 

- 可以设置local scope 和 global scope

  ```css
  // global 
  .root :global .text {
    color: brown;
    font-size: 24px;
    font-family: helvetica, arial, sans-serif;
    font-weight: 600;
  }
  ```

- 可以从当前文件或者其他文件引入CSS

  ```css
  /* 从当前文件引入 */
  .className {
    color: green;
    background: red;
  }
  
  .otherClassName {
    composes: className; // 这个 className 就是上面的定义的 clas
    color: yellow;
  }
  
  /* 从其他文件引入 */
  .text {
    // 通过 composes 引入
    composes: heading from "shared/styles/typography.css";
    color: blue;
  }
  
  // shared/styles/typography.css
  .heading {
    font-size: 14px;
  }
  ```


### CSS-in-js

就是把 CSS 放到 JS 中来写 

- styled-components：[https://github.com/styled-com...](https://link.segmentfault.com/?enc=IAyihTHS%2BY5Px04CDRnFjA%3D%3D.gu2vV3BIoMoFf8MHT7E1349T9seWHjYZdFlLebObYCEehC4dc9sqt%2FqxXeZDQ9FS8uPh81w1bDCKkSeUP9ioJg%3D%3D) 33k（**推荐**）
- emotion：[https://github.com/emotion-js...](https://link.segmentfault.com/?enc=Uumv4MwldbUYOXcDhByJiA%3D%3D.p4tRRosNCfTE6238Fmc6KeWJyyCCQcVYHaD1FzTO7lqUUMEzWWH8aL8c05wNpVSE) 13k
- Radium：[https://github.com/Formidable...](https://link.segmentfault.com/?enc=n1zmFVUH8FY2kbyaJ%2Bb2OQ%3D%3D.rDuc5cFgcgqkWKrAcQI2xZJ%2F1RCMN2cdLF4zXvrUJuDGlq4CifMPb2tAf0S6CM1f) 7k（已不再维护）
- Styled System：[https://github.com/styled-sys...](https://link.segmentfault.com/?enc=GeJh7zGH%2B59ZDolqfyIt9A%3D%3D.XgfdW68ZpudJnukdipF1%2BcAlqERTP%2FsHU%2FM8VVsvIJ6BEh3pdJKF1N1v9Dr8364%2B) 7k
- styled-jsx：[https://github.com/vercel/sty...](https://link.segmentfault.com/?enc=qy4uhOcTRmGwwVHOsKJMtg%3D%3D.dyg1d8Oh9INESeEtbErP9dPHTpXAwp2%2FbTpdnDoVZG%2Ba6OjCxrMZ8fMGpFQSJQSc) 6k
- JSS：[https://github.com/cssinjs/jss](https://link.segmentfault.com/?enc=996tGZuSvrE1x04eR9Gk3w%3D%3D.gNIrnbjSJ3ubB7akkLmqIs34%2BDBvSTvfGFSp7rHjM40%3D) 6k



- antd@5 的版本使用了 css-in-js，但是做了非常多的自定义的功能开发，在 4 的版本的时候，所有的 css 都需要一次性的手动引入，不管该组件需不需要，都会引入，5的版本就可以按需引入了
- css  写在 js 中，就可以非常清晰的按照模块来划分了，因为写在了 js 里
  - css-module 也是按照模块来划分，可以 webpack 编译的时候就自定义
- 会有性能损耗，因为需要解析 CSS，而且还是动态的解析，所以就需要runtime的解析代码的引入，会增加几kb
- 对 react 的渲染会造成问题，请看 [精读《我们为何弃用 css-in-js》](https://mp.weixin.qq.com/s/SQZvAguGydMnFDBqf4U9uA)





#### styled-components

​	https://github.com/styled-components/styled-components

用法

```js
import React from 'react';

import styled from 'styled-components';

// Create a <Title> react component that renders an <h1> which is
// centered, palevioletred and sized at 1.5em
const Title = styled.h1`
  font-size: 1.5em;
  text-align: center;
  color: palevioletred;
`;

// Create a <Wrapper> react component that renders a <section> with
// some padding and a papayawhip background
const Wrapper = styled.section`
  padding: 4em;
  background: papayawhip;
`;

// Use them like any other React component – except they're styled!
<Wrapper>
  <Title>Hello World, this is my first styled component!</Title>
</Wrapper>
```

通过 styled.{HTML 元素} 来创建一个 react 的元素，这样就可以把

**优点：**

- 语义清晰，在使用 styled 的时候使用了 html 的元素，然后会将当前的元素命名为符合认知的名称，如上述的 Wrapper / Title，我们日常写代码会通过 className 来增加语义化，那么使用上述的写法，就可以再阅读的时候更好
- 可以通过插值的方式给样式组件传递参数（`props`），这在需要动态生成样式规则时特别有用。
- 可以通过构造函数 `styled()` 来继承另一个组件的样式。
- 其他小的优点
  - 使用 `createGlobalStyle` 来创建全局 CSS 规则。
  - styled-components 会为自动添加浏览器兼容性前缀。
  - styled-components 基于 [stylis](https://link.segmentfault.com/?enc=MJ8yf4eAz8CqEa1KVBfXWw%3D%3D.t%2FlaAZ%2F4PuO9LxYMYXX%2Ft987eCxSrlRfUnrhK159yNrrXYwv9tlA%2BK5hJGQE45Tz)（一个轻量级的 CSS 预处理器），你可以在样式组件中直接使用嵌套语法，就像在 Sass/Less/Stylus 中的那样

**缺点：**

- 逻辑和样式不好分离，因为习惯性的会把样式和JS逻辑性的代码分开作为不同的文件来管理，按照这种文件来写的话，就会非常容易快速的就把一个文件的行数增多，导致不好维护

  - 你也可以说，可以把样式的文件放到另外一个文件中，然后导入进来

    这样在阅读的时候，可能就不清楚这个是一个导入的样式节点，还是一个功能节点了

    > 其实是不是可以不用去区分是样式还是功能节点？你在阅读当前的逻辑 JS 的时候，就可以很清晰的阅读当前的逻辑，然后跳转到对应的组件去阅读另外一个组件的逻辑就可以，不用刻意的去区分功能还是样式节点？

### less / sass

- 从 [如何看待字节同时开源 Arco 和 Semi](https://www.zhihu.com/question/494652270) 中看到这么一段话

  > Ant Design 因为样式都是用的 Less 所以想做个 Dark Mode 成本很高，而 Semi 是基于 Sass + CSS Vars 的，做这种动态主题切换方案简单了很多。（据可靠消息 Ant Design 5 会支持更灵活的主题动态切换，可以期待下~）
  >
  > > 没想到 less / sass 会有这种区别
  > >
  > > 是不是 Less 不支持 CSS Vars ？
  > >
  > > > 对，就是，我猜到了， 「As we know, less function can't work with css variables」参考 [an idea to combine less function and css variable](https://github.com/less/less.js/issues/3600)
  > > >
  > > > 「目前 css variables 和 less variable、less function 存在的问题：less function 视野里没有 css variable 的值
  > > > 这就导致使用了 less function 的库，（例如 antd ），就没法用 css variable 来覆写 `@primary-color`这样的变量，进而失去了利用 css variables 动态切换主题方案的能力。」 - [让 less 变量可以无痛迁移到 css variable ](https://github.com/arvinxx/less-plugin-dynamic-variable/issues/1)
  > > >
  > > > 
  > > >
  > > > 但是这种问题还是可以解决的对不对，在做法务项目的时候，就是在本地自定义样式的变量，然后通过 webpack 的 less-loader 来将这些变量传入，来达到自定义变量的功能，但上面说的是 less function，这又是个啥概念
  > > >
  > > > 
  > > >
  > > > 好像还真的就是只是 less function 不支持 css variables，因为看到了这种文章 [Theming with React, Less and CSS variables](https://dev.to/ksankar/theming-with-react-less-and-css-variables-2pbg)  也就是 less 是支持 css variables 的，就是 less function 不支持
  > > >
  > > > 
  > > >
  > > > 答案找到了 「 is not possible to use css variables as parameters of less functions like `color: darken(var(--header-color), 50%)`.」 from  [Using CSS variables in LESS](https://stackoverflow.com/questions/54346729/using-css-variables-in-less) 
  > > >
  > > > 正常的使用 css variables 是可以的
  > > >
  > > > > LESS allows you to use normal CSS code, so use one option could be just use the variable as CSS:
  > > > >
  > > > > ```css
  > > > > @import "../variables.css";
  > > > > .header {
  > > > >    color: var(--header-color);
  > > > > }
  > > > > ```
  > > > >
  > > > > Also, you can save the css var to a LESS var:
  > > > >
  > > > > ```less
  > > > > @import "../variables.css";
  > > > > @header-color: var(--header-color);
  > > > > 
  > > > > .header {
  > > > >    color: @header-color;
  > > > > }
  > > > > ```

- 翻了好几篇 less / sass 的区别的文章，感觉要真正明白这两者的区别，还是得靠自己真正的用起来，翻遍文档，这样自己才能够知道他们的利弊

-  LESS is purely written in JavaScript.，sass needs a compiler written in C++

- less 使用 @ 作为变量，sass 使用 $ 来作为变量

- less no loop and conditionals block (这个是啥意思，没有循环和条件，sass 有吗)

- 参考

  - [less_vs_sass](https://www.slant.co/versus/763/764/~less_vs_sass)




### post css

一般直接使用 post css 的语法倒是相对少一点，但是 post css 用来做工具还是有非常多的案例
1. 直接在 webpack 打包 sass/less 的时候，也会使用 post css 来打包
2. 使用 postcss 来做编译工具，如使用 post css 来编译 less/sass 这些，然后生成 ast
    并且 postcss 来支持定义在 less/sass 中的注释，然后解析注释，这个在 fusion 中有作为核心库用到
    1. 用到 sass 的注释，其实就是 saddoc，类似jsdoc 一样，使用 js 的注释生成对应的文档，所以就需要解析JS的注释，然后可以生成变量
    2. 生成了变量之后，就可以使用建站的方式，将变量填充到建站的占位符中，这样就可以生成对应的文档，这也就是他们的原理，fusion 也是使用了这个原理来获取注释中的变量的
3. postcss  是 post processors，而 less/scss 则是 preprocessors 



## 参考

- [精读《我们为何弃用 css-in-js》](https://mp.weixin.qq.com/s/SQZvAguGydMnFDBqf4U9uA)