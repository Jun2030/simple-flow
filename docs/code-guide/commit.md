### 01、Git提交规范作用

1. 修改文档、调整代码结构、性能优化，代码重构等信息一目了然
2. 提高合作开发的效率
3. 便于 **codereview** 及后续查阅、版本发布
4. 便于对自己的开发工作快速总结



### 02、提交消息格式规范

Commit message 一般包括三部分：标题(Header) + 正文(body) + 页脚(Footer)

```bash
[修改类型][(影响范围)]: [标题]

[正文]

[页脚]
```

!> 修改类型和标题是强制性的，但是标题的范围是可选的

1. **标题(Header):** `type(scope): subject`

   * `type`: 用于说明commit的类型，规定如下几种：
     * `feat`: 新增功能(feature)
     * `fix`: 修复bug
     * `docs`: 修改文档(documentation)
     * `style`: 调整代码格式，未修改代码逻辑（e.g.: 修改空格、格式化、缩进、分号、样式等）
     * `types`: 接口声明相关
     * `refactor`: 代码重构，没有添加新功能，也不是修复bug
     * `test`: 测试相关
     * `build`: 构建配置相关
     * `revert`: 回滚版本
     * `perf`: 性能优化，提高性能的代码更改
     * `merge`: 分支合并
     * `chore`: 对构建流程或辅助工具和依赖库（如文档生成，vconsole工具等）的更改
     * `ci`: 持续集成
   * `scope`: 可选。用于说明commit影响的范围，内容不固定，例如：
     * `route`: 路由模块
     * `view`: 页面模块
     * `api`: api模块
     * `component`: 组件模块
     * `utils`: 工具模块
     * `README`: 开发文档模块
     *  `*`: 多个模块
   * `subject`： 用于简短说明更新，结尾不要使用句号

2. **正文(Body)**

   可选。正文是对标题的补充。是commit的详细描述。如代码修改的动机，于修改前的代码对比等。

3. **页脚(Footer)**

   可选。页脚常用备注信息。比如

   1. 版本兼容性变动（需要相关描述）
   2. 关闭指定的Issue号（也适用于关闭的bug号）



### 03、校验/格式工具

* `commitlint`: 校验commit是否符合规范
* `husky`: git钩子
* `lint-staged`： 检测/格式化暂存区

项目中工具使用教程：

1. `pnpm install -D @commitlint/cli @commitlint/config-conventional husky lint-staged` 项目局部安装插件
2. 在项目根目录（.git同级目录）新建 `commitlint.config.js` 文件（文件内容如下），制定提交规范
3. `package.json` 中 `script` 写入下次运行命令
4. 命令行创建添加钩子,在根目录 `.husky` 目录中会新增 `commit-msg` , `pre-commit` 这两个文件
5. 分别在两个文件写入代码，并手动新增第三个检测规则文件 `lintstagedrc.js`

!> 如果在mac中检测报错，可将 `.husky` 目录的文件权限设置为 `chomd 777`，windows中也可通过右键属性设置权限，之后再上传即可

```javascript
// commitlint.config.js
module.exports = {
  ignores: [commit => commit.includes('init')],
  extends: ['@commitlint/config-conventional'],
  rules: {
    // 内容以空行开始
    'body-leading-blank': [2, 'always'],
    // 结尾以空行开始
    'footer-leading-blank': [2, 'always'],
    // 标题最大长度 72 个字符
    'header-max-length': [2, 'always', 72],
    // Scope 永远小写
    'scope-case': [2, 'always', 'lower-case'],
    // 不允许标题空着
    'subject-empty': [2, 'never'],
    // 不允许使用句号
    'subject-full-stop': [2, 'never'],
    // type 必须小写
    'type-case': [2, 'always', 'lower-case'],
    // type 不能为空
    'type-empty': [2, 'never'],
    // type 可选项
    'type-enum': [2, 'always',
      [
        'feat',     // 增加新功能
        'fix',      // 修复问题/BUG
        'docs',     // 文档/注释
        'style',    // 代码风格相关无影响运行结果的
        'types',    // 接口声明相关
        'refactor', // 重构
        'test',     // 测试相关
        'build',    // 构建配置相关
        'revert',   // 回滚某个更早之前的提交
        'perf',     // 优化/性能提升
        'merge',    // 分支合并
        'chore',    // 依赖更新/脚手架配置修改等
        'ci',       // 持续集成
      ],
    ],
  },
};
```

```json
// package.json
"scripts": {
	//...
  "prepare": "husky install"
},
```

```bash
# 创建钩子
npm set-script prepare "husky install"
npm run prepare
npx husky add .husky/commit-msg
npx husky add .husky/pre-commit
```

```bash
# commit-msg
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

# 提交记录检查
npx --no-install commitlint --edit $1
```

```bash
# pre-commit
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

npx lint-staged -c ./.husky/lintstagedrc.js
```

```javascript
// lintstagedrc.js
module.exports = {
  "src/**/*.{js,vue,ts,jsx,tsx}": ["eslint --fix"],
};
```



### 04、实例说明

```bash
feat(commit): 新增提交规范

1. 新增提交注释的项目安装步骤
2. 新增实例说明
```

更多可以查看本项目的提交



### 05、集成emoji

`devmoji`: 在提交时，可根据提交类型，自动添加 emoji 图标

项目中工具使用教程：

1. `pnpm install -D devmoji` 项目安装插件

2. `.husky/commit-msg` 文件最后新增一行，

   ```bash
   # commit-msg
   #!/bin/sh
   . "$(dirname "$0")/_/husky.sh"
   
   # 提交记录检查
   npx --no-install commitlint --edit $1
   # 根据提交类型自动添加gitmoji
   npx --no-install devmoji -e
   ```

3. 根目录下新建 `devmoji.config.js` 配置文件，调整并统一图标

   ```javascript
   // devmoji.config.js
   module.exports = {
     devmoji: [
       { code: 'docs', emoji: 'memo' },
       { code: 'types', emoji: 'label' },
       { code: 'test', emoji: 'white_check_mark' },
       { code: 'revert', emoji: 'rewind' },
       { code: 'merge', emoji: 'twisted_rightwards_arrows' },
     ],
   };
   ```

   

