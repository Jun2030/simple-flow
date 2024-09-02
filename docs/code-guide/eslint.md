### 01、Eslint配置教程

过程不表，所需插件大致如下(`ts`项目)：

- `@typescript-eslint/eslint-plugin`
- `@typescript-eslint/parser`
- `eslint`
- `eslint-plugin-import` (`react`)
- `eslint-plugin-jsx-ally` (`react`)
- `eslint-plugin-react` (`react`)
- `eslint-plugin-react-hooks` (`react`)
- `eslint-plugin-vue` (`vue`)



!>`Eslint` 在vscode中：eslint保存自动格式化与编辑器自带的保存自动格式化问题，涉及两个配置选项：`editor.formatOnSave`， `editor.codeActionsOnSave`

**问题：**

1. 如果仅开启 `eslint.format.enable`，则保存时，只能对 `js/ts` 等文件进行 `eslint` 格式化，不能对 `html/json` 等文件格式化
2. 如果仅开启 `editor.formatOnSave`，则对所有文件进行编辑器自带的格式化规则格式化文件
3. 如果同时开启，则 `js/ts` 每次保存都需要格式化两遍，影响保存性能，且格式化顺序：`自带格式化规则` > `eslint` 

**解决：**也是同时开启，但是分别配置，配置如下(以 `vue` 项目为例)：

```json
// .vscode/setting.json
"volar.tsPlugin": true,
"volar.icon.preview": true,
"volar.icon.finder": true,
// eslint相关配置
"eslint.enable": true,
"eslint.format.enable": true,
"eslint.options": {
  "extensions": [
    ".vue"
  ]
},
// 编辑器相关配置
"editor.formatOnSave": true,
"editor.codeActionsOnSave": {
  "source.fixAll.eslint": true,
},
// 格式化相关配置，需配置"editor.formatOnSave": true
// !!注意
// vue文件是有2层格式化的，volor + eslint
// js/ts文件，eslint
// html/json/...默认格式化
"[vue]": {
  "editor.defaultFormatter": "vue.volar"
},
"[javascript]": {
  "editor.defaultFormatter": "dbaeumer.vscode-eslint"
},
"[typescript]": {
  "editor.defaultFormatter": "dbaeumer.vscode-eslint"
},
```



### 02、Eslint风格规则

```javascript
// eslint.js
rules: {
  // 'off'    -> 0 关闭规则;
  // 'warn'   -> 1 开启警告规则;
  // 'error'  -> 2 开启错误规则;
  /* **************************** */
  /* 符号规则                      */
  /* **************************** */
  // 强制使用单引号
  'quotes': [2, 'single', {
    // 允许字符串使用单引号或者双引号，只要字符串中包含了一个其他引号，否则需要转义
    'avoidEscape': true,
    // 允许字符串使用模板字符串
    'allowTemplateLiterals': true,
  }],
  // 强制所有控制语句使用一致的括号风格
  'curly': [2, 'multi-line'],
  // 强制在代码块中使用一致的大括号风格
  'brace-style': [2, '1tbs', { 'allowSingleLine': true }],
  // 强制在多行对象/数组中尾随逗号
  'comma-dangle': [2, {
    'arrays': 'always-multiline',
    'objects': 'always-multiline',
    'imports': 'never',
    'exports': 'never',
    'functions': 'ignore',
  }],
  // 强制换行时逗号在行尾
  'comma-style': [2, 'last'],
  // 强制语句尾随分号
  'semi': [2, 'always'],
  // 箭头函数参数括号按需
  'arrow-parens': [2, 'as-needed'],
  /* **************************** */
  /* 空格规则                      */
  /* **************************** */
  // 强制2个空格作为缩进
  'indent': [2, 2, { 'SwitchCase': 1, 
  'VariableDeclarator': 'first' }],
  // 强制函数花括号内有间距
  'block-spacing': [2, 'always'],
  // 强制在块之前使用一致的空格
  'space-before-blocks': [2, 'always'],
  // 强制在function的左括号之前不适用空格
  'space-before-function-paren': [2, {
    'anonymous': 'always',
    'named': 'never',
    'asyncArrow': 'always',
  }],
  // 强制在注释// 或/*使用一致的空格
  'spaced-comment': [2, 'always'],
  // 强制逗号后要有空格
  'comma-spacing': [2, { 'before': false, 'after': true }],
  // 强制对象中左右空格
  'object-curly-spacing': [2, 'always'],
  // 强制数组中左右禁止空格
  'array-bracket-spacing': [2, 'never'],
  // 允许在字符串和注释之外不规则的空白
  'no-irregular-whitespace': 0,
  // 强制箭头函数箭头左右空格
  'arrow-spacing': [2, { 'before': true, 'after': true }],
  // 强制操作符两边需要空格
  'space-infix-ops': 2,
  // 强制对象字面量属性中冒号后空格
  'key-spacing': [2, { 'beforeColon': false, 'afterColon': true }],
  // 强制关键字前后需要空格
  'keyword-spacing': [2, {
    'before': true,
    'after': true,
  }],
  /* **************************** */
  /* 语法规则                      */
  /* **************************** */
  // 禁止出现重复的case标签
  'no-duplicate-case': 2,
  // 禁止在return、throw、continue、break语句之后出现不可达代码
  'no-unreachable': 2,
  // 禁止function定义中出现重名参数
  'no-dupe-args': 2,
  // 禁止case语句落空
  'no-fallthrough': 2,
  // 禁止类成员中出现重复的名称
  'no-dupe-class-members': 2,
  // 禁止出现未使用的变量
  'no-unused-vars': [2, { 'varsIgnorePattern': '.*', 'args': 'none' }],
  // 禁用不必要嵌套块
  'no-lone-blocks': 2,
  // 强制禁用var
  'no-var': 2,
  // 强制禁止出现空函数
  'no-empty-function': 2,
  // 禁止不必要的括号
  'no-extra-parens': [2, 'functions'],
  // 强制使用 ===和 !==
  'eqeqeq': [2, 'always'],
  /* **************************** */
  /* TS规则                       */
  /* **************************** */
  '@typescript-eslint/ban-ts-ignore': 0,
  '@typescript-eslint/explicit-function-return-type': 0,
  '@typescript-eslint/no-explicit-any': 0,
  '@typescript-eslint/no-var-requires': 0,
  '@typescript-eslint/no-empty-function': 0,
  '@typescript-eslint/no-use-before-define': 0,
  '@typescript-eslint/ban-ts-comment': 0,
  '@typescript-eslint/ban-types': 0,
  '@typescript-eslint/no-non-null-assertion': 0,
  '@typescript-eslint/explicit-module-boundary-types': 0,
  '@typescript-eslint/no-unused-vars': [2, { varsIgnorePattern: '.*', args: 'none' }],
},
```

