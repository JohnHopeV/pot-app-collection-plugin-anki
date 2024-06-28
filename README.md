# Pot-App 生词本插件模板仓库 (以 [Anki](https://apps.ankiweb.net) 为例)

### 此仓库为模板仓库，编写插件时可以直接由此仓库创建插件仓库

## 插件编写指南

### 1. 插件仓库创建

- 以此仓库为模板创建一个新的仓库
- 仓库名为 `pot-app-collection-plugin-<插件名>`，例如 `pot-app-collection-plugin-anki`

### 2. 插件信息配置

编辑 `info.json` 文件，修改以下字段：

- `id`：插件唯一 id，必须以`plugin`开头，例如 `plugin.com.pot-app.anki`
- `homepage`: 插件主页，填写你的仓库地址即可，例如 `https://github.com/pot-app/pot-app-collection-plugin-template`
- `display`: 插件显示名称，例如 `Anki`
- `icon`: 插件图标，例如 `anki.svg`
- `needs`: 插件依赖，一个数组，每个依赖为一个对象，包含以下字段：
  - `key`: 依赖 key，对应该项依赖在配置文件中的名称，例如 `port`
  - `display`: 依赖显示名称，对应用户显示的名称，例如 `端口号`
  - `type`: 组件类型 `input` | `select`
  - `options`: 选项列表(仅 select 组件需要)，例如 `{"engine_a":"Engina A","engine_b":"Engina B"}`

### 3. 插件编写/编译

编辑 `main.js` 实现 `collection` 函数

#### 输入参数
```javascript
// config: config map
// detect: detected source language
// setResult: function to set result text
// utils: some tools
//     http: tauri http module
//     readBinaryFile: function
//     readTextFile: function
//     Database: tauri Database class
//     CryptoJS: CryptoJS module
//     cacheDir: cache dir path
//     pluginDir: current plugin dir 
//     osType: "Windows_NT" | "Darwin" | "Linux"
async function collection(source, target, options = {}) {
  const { config, utils } = options;
  const { http, readBinaryFile, readTextFile, Database, CryptoJS, run, cacheDir, pluginDir, osType } = utils;
  const { fetch, Body } = http;
}
```

#### 返回值

```javascript
return true;
```

### 4. 打包 pot 插件

1. 将`main.js`文件和`info.json`以及图标文件压缩为 zip 文件。

2. 将文件重命名为`<插件id>.potext`，例如`plugin.com.pot-app.anki.potext`,即可得到 pot 需要的插件。

## 自动编译打包

本仓库配置了 Github Actions，可以实现推送后自动编译打包插件。

每次将仓库推送到 GitHub 之后 actions 会自动运行，将打包好的插件上传到 artifact，在 actions 页面可以下载

每次提交 Tag 之后，actions 会自动运行，将打包好的插件上传到 release，在 release 页面可以下载打包好的插件
