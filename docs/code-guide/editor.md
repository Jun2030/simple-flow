### 01、编码风格意义

* `Editorconfig` 可以帮助开发人员定义和维护编码的一致性
* 不同编辑器和IDE之间的编码风格共享(vscode需搭配插件 `EditorConfig for VS Code` )



### 02、编码风格规范

文件位于项目根目录下，`.editorconfig` 文件：

```bash
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

[*.md]
trim_trailing_whitespace = false

[*.{js,jsx,ts,tsx}]
insert_final_newline = false
```

