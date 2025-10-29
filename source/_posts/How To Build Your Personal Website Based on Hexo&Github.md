---
title: 如何基于Hexo和Github搭建个人网站
date: 2025-10-29 09:29:13
tags: [Hexo, GitHub, Personal Website, Technological Tutorial, Static Blogs]
categories: [Blogs]
description: 从环境准备到上线访问，手把手教你用Hexo+GitHub免费搭建可自定义的个人网站，适合新手入门，步骤清晰无冗余。
---

# 如何基于Hexo和GitHub搭建个人网站
Hexo（轻量静态博客框架）+ GitHub Pages（免费静态托管服务）的组合，无需服务器、零成本，还能灵活自定义风格，是新手搭建个人网站的首选方案。以下是完整实现步骤，全程约30分钟可完成。


## 一、前期准备：安装必备工具
搭建前需准备3个核心工具，确保环境兼容（重点注意Node.js版本，避免后续报错）。

### 1. 安装Node.js（Hexo运行依赖）
- **下载地址**：访问[Node.js官网](https://nodejs.org/)，选择**LTS长期支持版**（推荐v20.19.0及以上，与Hexo 8.x+兼容）；
- **安装注意**：Windows用户勾选“Add to PATH”（自动配置环境变量），Mac用户默认配置即可；
- **验证安装**：打开终端（Windows用Git Bash，Mac用终端），输入以下命令，显示版本号即成功：
  ```bash
  node -v  # 示例输出：v20.19.0
  npm -v   # 示例输出：10.8.1（npm随Node.js自带）
  ```

### 2. 安装Git（版本控制与GitHub交互）
- **下载地址**：访问[Git官网](https://git-scm.com/)，按系统选择对应版本安装；
- **验证安装**：终端输入`git --version`，显示版本号即成功（示例：`git version 2.45.1`）。

### 3. 准备GitHub账号与仓库
- **注册账号**：访问[GitHub官网](https://github.com/)，注册一个账号（已有账号跳过）；
- **创建网站仓库**：  
  点击GitHub右上角“+”→“New repository”，填写仓库信息：
  - Repository name（必填）：格式为`用户名.github.io`（例如你的`fwang-0406.github.io`），这是GitHub Pages的固定命名规则，否则无法正常访问；
  - Visibility（必填）：选择“Public”（私有仓库无法启用GitHub Pages）；
  - 其他选项默认，点击“Create repository”完成创建。


## 二、初始化Hexo项目（本地搭建博客框架）
Hexo项目是存放网站源文件（文章、配置、主题）的核心，需在本地完成初始化。

### 1. 安装Hexo脚手架（全局工具）
终端输入以下命令，全局安装Hexo命令行工具：
```bash
npm install -g hexo-cli
```
- 验证安装：输入`hexo -v`，显示Hexo版本信息即成功（示例：`hexo-cli: 4.3.0`）。

### 2. 创建并初始化Hexo项目
- **新建项目目录**：选择一个本地文件夹（例如`D:/hexo-blog`），终端进入该目录：
  ```bash
  cd D:/hexo-blog  # Windows路径示例
  # cd ~/Documents/hexo-blog  # Mac路径示例
  ```
- **初始化项目**：执行以下命令，Hexo会自动创建基础目录结构（`source/`、`themes/`、`_config.yml`等）：
  ```bash
  hexo init my-site  # “my-site”是项目名，可自定义
  cd my-site         # 进入项目目录
  npm install        # 安装项目依赖（生成node_modules文件夹）
  ```

### 3. 本地预览初始效果
初始化完成后，启动本地服务器预览默认博客：
```bash
hexo server  # 简写：hexo s
```
- 终端显示`INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.`时，打开浏览器访问`http://localhost:4000`，能看到Hexo默认首页（含一篇“Hello World”测试文章），说明项目初始化成功。
- 停止预览：按`Ctrl+C`关闭本地服务器。


## 三、主题配置：自定义网站风格（以Cactus为例）
Hexo默认主题（Landscape）风格简单，本网站使用的是**Cactus主题**（简洁优雅，支持深色模式、评论系统）。

### 1. 安装Cactus主题
在Hexo项目目录（`my-site`）下，执行命令下载Cactus主题到`themes/cactus`目录：
```bash
git clone https://github.com/probberechts/hexo-theme-cactus.git themes/cactus
```

### 2. 启用Cactus主题
- 打开Hexo项目根目录的`_config.yml`文件（全局配置文件），找到`theme`字段，将默认值改为`cactus`：
  ```yaml
  # theme: landscape  # 注释默认主题
  theme: cactus  # 启用Cactus主题
  ```
- **注意**：YAML文件对缩进敏感，`theme: cactus`前需保留2个空格，否则会报错。

### 3. 主题个性化配置
Cactus主题的导航由`themes/cactus/_config.yml`控制，打开该文件，修改相应字段。  
不同主题的个性化设置步骤和内容可能不同，需要根据主题的GitHub仓库README页面指导进行。  
例如，本网站使用的Cactus主题，可访问其官方仓库获取详细配置说明：[hexo-theme-cactus 主题官方仓库](https://github.com/probberechts/hexo-theme-cactus.git)

## 四、内容创建：添加“关于页”与第一篇文章
Hexo的内容分为“页面（Page）”和“文章（Post）”，前者用于独立页面（如About），后者用于博客文章，两者创建方式不同（呼应你之前的疑问）。

### 1. 创建“关于页”（Page类型）
执行以下命令，创建独立的“关于我”页面：
```bash
hexo new page about  # “about”是页面名，对应导航的“about: /about/”
```
- 该命令会在`source/about/`目录下生成`index.md`文件，用Markdown编辑器（如VS Code、Typora、最新的Windows记事本）打开，编辑内容：
  ```markdown
  ---
  title: 关于我
  date: 2025-10-29 10:00:00
  ---
  大家好，我是Rachel，一名技术爱好者。  
  这个网站基于Hexo+GitHub搭建，用于分享技术笔记、学习心得和生活感悟。  
  欢迎通过GitHub或者邮箱与我交流！
  ```

### 2. 创建第一篇技术文章（Post类型）
执行以下命令，创建博客文章（会自动放入`source/_posts/`目录）：
```bash
hexo new post "如何基于Hexo和Github搭建个人网站"  # 文章标题
```
- 打开`source/_posts/如何基于Hexo和Github搭建个人网站.md`，补充文章内容。


## 五、部署上线：将本地网站推送到GitHub Pages
完成内容与配置后，需将Hexo生成的“静态文件”部署到GitHub仓库的`main`分支，GitHub Pages会自动加载该分支的文件并展示网站。

### 1. 安装Hexo-Git部署插件
在Hexo项目目录下，执行命令安装部署插件（用于连接GitHub）：
```bash
npm install hexo-deployer-git --save
```

### 2. 配置GitHub部署信息
打开Hexo根目录的`_config.yml`，找到`deploy`字段（若没有则新增），填写你的GitHub仓库信息：
```yaml
deploy:
  type: git
  repo: git@github.com:name/name.github.io.git  # 你的仓库SSH地址
  branch: main  # 部署到main分支（GitHub Pages默认读取该分支）
```
- **获取仓库SSH地址**：进入你的GitHub仓库（`name.github.io`），点击“Code”→选择“SSH”→复制地址（格式为`git@github.com:用户名/仓库名.git`）。

### 3. 解决GitHub SSH权限问题（关键步骤）
若直接部署提示“权限不足”，需配置GitHub SSH密钥（让本地与GitHub建立信任）：
- **生成SSH密钥**：终端输入以下命令（替换为你的GitHub邮箱），按3次回车（无需设置密码）：
  ```bash
  ssh-keygen -t ed25519 -C "name@email"
  ```
- **添加密钥到GitHub**：  
  1. 打开生成的密钥文件（Windows路径：`C:/Users/你的用户名/.ssh/id_ed25519.pub`；Mac路径：`~/.ssh/id_ed25519.pub`），复制全部内容；  
  2. 登录GitHub→点击头像→“Settings”→“SSH and GPG keys”→“New SSH key”；  
  3. Title随便填（如“Hexo-PC”），Key粘贴刚才复制的内容，点击“Add SSH key”。
- **验证SSH连接**：终端输入`ssh -T git@github.com`，出现`Hi name! You've successfully authenticated...`即成功。

### 4. 执行部署命令
在Hexo项目目录下，执行以下命令，一键生成静态文件并推送到GitHub：
```bash
hexo clean && hexo generate && hexo deploy
# 简写：hexo cl && hexo g && hexo d
```
- 命令解析：  
  - `hexo clean`：清除旧的静态文件（避免缓存干扰）；  
  - `hexo generate`：生成新的静态文件（输出到`public/`目录）；  
  - `hexo deploy`：将`public/`目录的文件推送到GitHub`main`分支。


## 六、验证与后续维护
### 1. 访问个人网站
部署完成后，等待1-2分钟（GitHub需缓存更新），打开浏览器访问：  
`https://name.github.io`（格式：`https://用户名.github.io`）  
- 若能看到你的网站首页、导航正常、文章可访问，说明搭建成功！
- 若页面无变化：按`Ctrl+F5`（Windows）或`Cmd+Shift+R`（Mac）强制刷新浏览器，清除本地缓存。

### 2. 后续维护操作
- **新增文章**：`hexo new post "文章标题"`→编辑内容→`hexo cl && hexo g && hexo d`；  
- **修改配置**：修改主题或根目录`_config.yml`后，需重新执行部署命令生效；  
- **备份源文件**：将Hexo项目（`my-site`）推送到GitHub仓库的`source`分支（避免本地文件丢失）：
  ```bash
  git init
  git remote add origin git@github.com:name/name.github.io.git
  git checkout -b source  # 创建source分支存放源文件
  git add . && git commit -m "备份Hexo源文件"
  git push -u origin source
  ```


## 常见问题排查
1. **部署后GitHub Pages显示404**：  
   - 检查仓库名是否为`用户名.github.io`（大小写敏感）；  
   - 确认部署到`main`分支，且分支下有`index.html`文件。  
2. **本地预览正常，部署后样式错乱**：  
   - 检查根目录`_config.yml`的`url`字段是否正确（应为`https://name.github.io`），避免资源路径错误。  
3. **Hexo命令报错“ERR_REQUIRE_ESM”**：  
   - 升级Node.js到v20.19.0及以上，或降级Hexo到7.x版本（`npm install hexo@7.3.0`）。

通过以上步骤，你已拥有一个完全自定义的个人网站