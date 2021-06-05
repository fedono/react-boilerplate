# 关于 CSS 的技术选型

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

  

