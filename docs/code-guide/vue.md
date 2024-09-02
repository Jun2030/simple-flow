### 01、命名规范

1. Vue文件，如果有多个单词，采用pascal命名法。

   e.g.: `MyComponent.vue`, `BaseButton.vue`

2. 基础组件文件。也就是样式类的，无逻辑，或无状态的组件。以一个特定的前缀开头。

   e.g.：`Base[xxx]`, `UI[xxx]`

3. 单例组件文件。无数据交互的，每个页面只可能使用一次的，单例组件不接受任何 `prop`。组件名以 `The` 前缀命名。

   e.g.: `TheHeading.vue`, `TheSidebar.vue` 

4. 紧密耦合组件文件。子组件命名可以以父组件名作为前缀命名。

   e.g.: `TodoList.vue`, `TodoListItem.vue`, `TodoListItemButton.vue`

5. 公共组件与页面组件 `class` 名必须加以区分。

   e.g.: `<div class="view-login"></div>`, `<div class="component-btn"></div>`

6. `props` 、 `data/setup` 中变量名，均采用驼峰命名法。

   e.g.: `tableData`, `titleText`

7. Vue2中 `computed` 、`methods`、`watch` 中的方法名，全部采用驼峰命名法。

   e.g.: `getTableList(){}`

8. 函数名均采用驼峰命名法，并且前缀为动词。

   e.g.: `function getListData() {}`
   
   * 常用动词推荐：`can`， `is`, `has`, `get`, `set`, `load`, `open`, `close`, `jump`, `computed`
   * 触发为事件型动词推荐：`on`, `handle`
   
9. 函数参数，路由参数全部采用驼峰命名法。

   e.g.: `userId`
   
   

### 02、注释规范

1. 建议文件顶部写入文件信息注释。具体注释和其他注释可参照【[注释规范](/code-guide/comment?id=_04、文件文档注释)】
2. 公共组件必要注释使用说明
3. 复杂的业务逻辑处理须注释说明



### 03、语法规范

1. `template` 中组件标签渲染须采用中划线形式

2. `template` 中模块之间建议注释处理。

3. `template` 中建议不要写死数据，建议用变量替代，数据写在 `data/setup` 中。

4. `template` 中多个属性建议换行处理，增强可读性。

5. `template` 中如果涉及复杂的逻辑表达式，可以放入 `computed` 或者 `methods` 中，以函数形式 `return` 给出。

6. `template` 中涉及引号，优先使用双引号。

   e.g.: `<app-title :style="{ width: titleWidth + 'px' }"></app-title>`

7. `v-for` 和 `:key` 须配合使用。

8. `v-if` 和 `v-for` 不要同时用在同一个DOM上。

9. `props` 中数据尽量采用详尽模式。

   ```javascript
   props: {
       status: {
           type: String | Number,
           required: true,
           default: 0
       }
   }
   ```

10. 使用字符串模块来进行字符串拼接。

12. 公共组件统一放在 `components` 文件夹下。

13. 公共方法、全局常量、请求封装、分享封装放在 utils 文件夹下。

14. 路由模块工程化处理，自动化导入，精简代码。

15. 页面组件的样式/公众组件的样式/全局的样式，推荐单独放置到 `styles` 文件下内。

16. 静态文件统一放在 `assets` 文件夹下，需要绝对路径的静态文件统一放到 `public` 文件夹下。

17. 接口文件统一方法 `api` 文件夹下。

18. 特殊常量（微信appID等）统一放在 `.env` 环境配置中。



### 04、Vue2选项式顺序规范

1. `name: `
2. `components: {}`
3. `props: {}`
4. `data(){}`
5. `computed: {}`
6. `created() {}`
7. `mounted() {}`
8. `methods: {}`
9. `watch: {}`



### 05、Vue3规范建议

在 `Vue2`的基础上，新增：

1. 优先使用 `setup` 语法
2. 数据在使用时才定义，不要有 `Vue2` 定义 `state` 数据的思维
3. 数据信息建议抽离成独立文件，在引入使用
4. 如果单个组件内业务量比较大，可拆分成独立的组合式文件



### 06、Volar(>0.34.xx)升级教程

1. 安装（升级）插件最新版（`Vue Language Features (Volar)`）

2. 改用接管模式

   1. 删除插件（`TypeScript Vue Plugin (Volar)`），如果之前有使用的话
   2. 插件搜索 `@builtin` -> 选择 `JavaScript 和 TypeScript 的语言功能` -> 右键 -> 禁用（工作区）
   3. 重启 `vscode` 编辑器

3. 插件已更名为 `Vue.volar`，（2022-05-05号已改名）涉及到的修改为

   1. ```json
      // .vscode/extension.json
      {
        "recommendations": [
          "vue.volar",
          // ...
        ]
      }
      ```

   2. ```json
      // .vscode/setting.json
      {
        "volar.tsPlugin": true,
        "volar.icon.preview": true,
        "volar.icon.finder": true,
        "eslint.enable": true,
        "eslint.format.enable": true,
        "eslint.options": {
          "extensions": [
            ".vue"
          ]
        },
        "editor.formatOnSave": true,
        "editor.codeActionsOnSave": {
          "source.fixAll.eslint": true
        },
        "[vue]": {
          "editor.defaultFormatter": "vue.volar"
        },
        "[javascript]": {
          "editor.defaultFormatter": "dbaeumer.vscode-eslint"
        },
        "[typescript]": {
          "editor.defaultFormatter": "dbaeumer.vscode-eslint"
        }
      }
      ```

   

4. 解决新版本 `template` 中html一行过长自动格式化问题，（这里沿用之前 `eslint` + `volar` 的格式规范，当然也可使用 `prettier` 插件处理 ）

   1. 安装插件：`pnpm add @volar-plugins/prettyhtml -D`

   2. 插件设置：项目根目录新增 `volar.config.js` 文件

      ```javascript
      // volar.config.js
      const prettyhtml = require('@volar-plugins/prettyhtml');
      
      module.exports = {
        plugins: [
          prettyhtml({ printWidth: 100 }),
        ],
      };
      ```

   3. 重启 `vscode` 编辑器
