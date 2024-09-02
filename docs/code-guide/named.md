### 01、复数命名方式

> - 驼峰（camel）命名法。e.g.: `thisIsAnApple`
> - 帕斯卡（pascal）命名法。e.g.: `ThisIsAnApple`
> - 下划线命名法。e.g.: `this_is_an_apple`
> - 中划线命名法。e.g.: `this-is-an-apple`（参照Github众多前端开源项目，本规范将推荐此命名法）


### 02、项目命名

采用中划线方式，多单词以下划线命名。

e.g.: `simple-flow`



### 03、目录命名

1. 优先单数形式，有复数结构时，采用复数命名法。

   e.g.: `utils`, `styles`, `images`, `views`, `components`, `assets`

2. 非组件父级，采用中划线命名法。

   比如，在项目中，不管是public静态目录下还是webpack/vite打包文件目录。

   e.g.: `static-images`, `global-styles`, `dist-alpha`

2. 组件直接父级，如果有，则采用pascal命名。

   e.g.：`components/UICardItem.vue`, `components/User/index.tsx`



### 04、Html文件命名

如果有多个单词，采用中划线命名法。

e.g.: `login-home.html`



### 05、Css文件命名

1. 如果有多个单词，采用中划线命名法。

   e.g.: `element-ui.scss`, `global-variables.scss`

2. 如果私有意义的，可采用下划线开始命名法。

   e.g.: `_varbile.less`, `_mixin.css`， `_mixin-flex.css`



### 06、Javascript文件命名

1. 如果有多个单词，非组件关联，采用中划线命名法。

   e.g.: `global-methods.js`, `global-const.js`

2. 如果有组件关联，采用Pascal命名法。

   e.g.: `Login.tsx`, `ForgetPassword.tsx`





### 07、组件命名

组件文件，如果有多个单词，采用pascal命名法。

e.g.: `MyComponent.vue`, `BaseButton.vue`

**需要注意的是：**

+ 基础组件文件。也就是样式类的，无逻辑，或无状态的组件。全部以一个特定的前缀开头。

  e.g.：`Base[xxx].tsx`, `UI[xxx].tsx` 等。

+ 单例组件文件。无数据交互的，每个页面只可能使用一次的，单例组件不接受任何 `prop`。组件名以 `The` 前缀命名。

  e.g.: `TheHeading.vue`, `TheSidebar.tsx` 等。

+ 紧密耦合组件文件。子组件命名以父组件名作为前缀命名。

  e.g.: `TodoList.tsx`, `TodoListItem.vue`, `TodoListItemButton.tsx` 等。

  

### 08、Markdow文件命名

1. 如果有多个单词，采用中划线命名法。

   e.g.: `code-guide.md`, `dev-document.md` 等。

2. 特殊的单词，以全部大写命名。

   e.g.: `README.md`, `CHANGELOG.md` 等。



### 09、图片命名

如果有多个单词，采用下划线命名法。一般携带图片类型信息。

e.g.: `icon/icon_avatar.jpg`, `header/bg_defalut.png` 等。



### 10、路由参数

如果有多个单词，采用驼峰命名法。

e.g.: `activityId`, `https://abc.com?userId=2&type=1`

