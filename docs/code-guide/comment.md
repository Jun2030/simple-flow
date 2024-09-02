### 01、注释规范

1. 注释符与注释内容之间要加一个空格。e.g.:

   ```javascript
   const a = b; // 大哥，这样写会报错的  √
   const c = d; //大哥，这样写会报错的   ×
   ```

2. 函数与别的代码要留有一空行

   ```javascript
   function funA () {
     console.log('hello world');
   }
   
   // 这是下面代码的注释
   funA();
   ```

3. 每个文件建议要加文档注释（文件内容说明、开发者、开发时间、重要修改或备注等信息）

4. js函数/方法建议需要注释
   + 必须包含函数的说明（推荐必须）
   + 有参数或有返回值时，必须有注释标志
   + 参数和返回值必须包含类型信息和说明



### 02、注释原则

> 1. 提高可读性和可维护性
> 2. 注释如果没有必要，就不要增加注释，如果注释有必要，就尽量详尽



### 03、释法语法

1. 行内注释
   + `// `: 	展示解析性注释
   + `// >`:   展示console的输出结果
   + `// =>`:  展示表达式结果
2. 单行注释
   + `//`: 表示注释文字
3. 多行注释
   + `/* */`: 表示多行注释文字



### 04、文件文档注释

Vscode编辑器推荐使用: `koroFileHeader` 这个插件，其配置文件（setting.js）推荐如下：

```javascript
// vscode/setting.js

// ------------------- koro1FileHeader插件相关配置 -------------------- //
// 头部注释
"fileheader.customMade": {
  "Overview": "Do not edit",
  "Author": "Zi Jun",
  "Email": "zijun2030@163.com",
  "Date": "Do not edit",
  "LastEditTime": "Do not edit",
  "LastEditors": "Zi Jun"
},
// 函数注释
"fileheader.cursorMode": {
  "Description": "",
  "param": "",
  "return": ""
},
// 插件配置项
"fileheader.configObj": {
  // 自动添加头部注释黑名单
  "prohibitAutoAdd": [
    "json",
    "md"
  ],
  // 头部注释等宽设置
  "wideSame": true,
  // 单个文件保存时进行diff检查
  "CheckFileChange": true,
},
```

e.g.: `js` 文件中注释为：

```html
/*
 * @Overview     : 文档注释
 * @Author       : Zi Jun
 * @Email        : zijun2030@163.com
 * @Date         : 2021-12-04 14:26:01
 * @LastEditTime : 2021-12-04 19:01:34
 * @LastEditors  : Zi Jun
 */
```



### 05、Html注释

+ 模块注释

  ```html
  <!-- Part: 标题模块 -->
  ```

  

### 06、Css注释

+ 区块与区块、子区块与子区块之间需要空行

  ```scss
  /* ==============================================
  Part1区块
  ===============================================*/
  .part1 {
    // Part1-1区块
    .part1-1 {}
    
    // Part1-2区块
    .part1-2 {}
  }
  
  /* ==============================================
  Part2区块
  ===============================================*/
  .part1-2 {}
  ```
  
  

### 07、Javascript注释

+ 单行注释

+ 多行注释

+ 函数（方法）注释

  + 包含函数的说明(推荐)
  + 有参数或有返回值时，有注释标志
  + 参数和返回值包含类型信息和说明

  ```javascript
  /**
   * 获取两数相加之值
   * @param p1 {Number} 加数1
   * @param p2 {Number} 加数2
   * @return {Number} 返回两数之和
   */
  function sum(p1, p2) {
    let result = p1 + p2;
    retrun result;
  }
  ```

  

### 08、逻辑模块注释

如果涉及逻辑处理，可用注释作为区隔

```typescript
/****************  登陆模块   *****************/
const loginParams: ILoginParams = {};
const login = (loginParams): void => {}

/****************  登出模块   *****************/
const logout = () => {}
```

