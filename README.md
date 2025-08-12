# AYW-OJ - 在线编程评测系统

<div align="center">

![Vue.js](https://img.shields.io/badge/Vue.js-3.2.13-4FC08D?style=flat-square&logo=vue.js)
![TypeScript](https://img.shields.io/badge/TypeScript-4.5.5-3178C6?style=flat-square&logo=typescript)
![Vue Router](https://img.shields.io/badge/Vue%20Router-4.0.3-4FC08D?style=flat-square&logo=vue.js)
![Vuex](https://img.shields.io/badge/Vuex-4.0.0-4FC08D?style=flat-square&logo=vue.js)
![Monaco Editor](https://img.shields.io/badge/Monaco%20Editor-0.41.0-007ACC?style=flat-square&logo=visual-studio-code)

**基于 Vue 3 + TypeScript 的现代化在线编程评测系统前端**

[在线演示](#) | [后端项目](#) | [项目文档](#)

</div>

## 📖 项目简介

AYW-OJ 是一个功能完整的在线编程评测系统，为编程学习者和教育机构提供专业的代码评测服务。系统支持多种编程语言，具备实时编译、安全沙箱执行、智能评测等核心功能。

### ✨ 核心特性

- 🚀 **现代化技术栈** - 基于 Vue 3 + TypeScript 构建，性能优异
- 💻 **智能代码编辑器** - 集成 Monaco Editor，支持语法高亮、自动补全
- 🔒 **安全代码执行** - 自主研发代码沙箱，确保系统安全
- 📊 **实时评测反馈** - 即时编译执行，详细评测报告
- 👥 **用户权限管理** - 完善的用户角色和权限控制系统
- 📱 **响应式设计** - 支持多端访问，移动端友好
- 🎨 **美观界面** - 基于 Arco Design Vue 组件库，界面简洁美观

## 🛠️ 技术栈

### 前端技术
- **框架**: Vue 3.2.13
- **语言**: TypeScript 4.5.5
- **路由**: Vue Router 4.0.3
- **状态管理**: Vuex 4.0.0
- **UI组件库**: Arco Design Vue 2.49.1
- **代码编辑器**: Monaco Editor 0.41.0
- **Markdown编辑器**: ByteMD 1.21.0
- **HTTP客户端**: Axios 1.4.0

### 开发工具
- **构建工具**: Vue CLI 5.0
- **代码规范**: ESLint + Prettier
- **包管理**: Yarn 1.22.22
- **API生成**: OpenAPI TypeScript Codegen

## 🚀 快速开始

### 环境要求

- Node.js >= 14.0.0

### 安装依赖

```bash
# 克隆项目
git clone https://github.com/Ei-Ayw/ayw-oj-frontend.git

# 进入项目目录
cd ayw-oj-frontend

# 安装依赖
npm install
```

### 开发运行

```bash
# 启动开发服务器
npm run serve

# 访问 http://localhost:8080
```

## 📁 项目结构

```
ayw-oj-frontend/
├── public/                 # 静态资源
├── src/
│   ├── access/            # 权限控制
│   ├── assets/            # 资源文件
│   ├── components/        # 公共组件
│   │   ├── CodeEditor.vue    # 代码编辑器
│   │   ├── GlobalHeader.vue  # 全局头部
│   │   ├── MdEditor.vue      # Markdown编辑器
│   │   └── MdViewer.vue      # Markdown查看器
│   ├── layouts/           # 布局组件
│   ├── plugins/           # 插件配置
│   ├── router/            # 路由配置
│   ├── store/             # 状态管理
│   ├── views/             # 页面组件
│   │   ├── question/         # 题目相关页面
│   │   └── user/             # 用户相关页面
│   └── main.ts            # 入口文件
├── generated/             # 自动生成的API代码
└── package.json          # 项目配置
```

## 🎯 功能模块

### 用户功能
- 🔐 **用户注册/登录** - 支持邮箱注册，安全登录
- 👤 **个人中心** - 个人信息管理，提交历史查看
- 📝 **题目浏览** - 分类浏览，搜索筛选题目
- 💻 **在线编程** - 集成代码编辑器，支持多种语言
- 📊 **提交评测** - 实时编译执行，查看评测结果

### 管理员功能
- 📋 **题目管理** - 创建、编辑、删除编程题目
- 👥 **用户管理** - 用户信息查看，权限管理
- 📈 **数据统计** - 系统使用情况统计
- ⚙️ **系统配置** - 评测参数配置

### 开发配置

项目使用 Vue CLI 进行构建，主要配置文件：

- `vue.config.js` - Vue CLI 配置
- `tsconfig.json` - TypeScript 配置
- `.eslintrc.js` - ESLint 配置

## 🤝 贡献指南

我们欢迎所有形式的贡献，包括但不限于：

1. 🐛 **Bug 报告** - 提交 Issue 报告问题
2. 💡 **功能建议** - 提出新功能想法
3. 🔧 **代码贡献** - 提交 Pull Request
4. 📖 **文档完善** - 改进项目文档

### 开发流程

1. Fork 本仓库
2. 创建功能分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 创建 Pull Request

## 📄 开源协议

本项目采用 [MIT License](LICENSE) 开源协议。

## 🙏 致谢

感谢以下开源项目的支持：

- [Vue.js](https://vuejs.org/) - 渐进式 JavaScript 框架
- [Arco Design Vue](https://arco.design/vue/) - 企业级设计系统
- [Monaco Editor](https://microsoft.github.io/monaco-editor/) - 代码编辑器
- [ByteMD](https://github.com/bytedance/bytemd) - Markdown 编辑器

## 👨‍💻 关于作者

**Ei-Ayw** - 全栈工程师 | AI研究员

专注于 Java/SpringBoot、Vue 和 PyTorch 深度学习技术栈。作为数据科学与大数据技术专业人才，致力于构建健壮的全栈系统和推进深度学习研究。

### 🏆 特色项目
- **cangqiongzhijian-frontend** - 基于Vue的复杂前端应用，具备丰富的交互功能
- **ayw-oj** - 全栈在线评测平台，Java/SpringBoot后端 + Vue前端
- **zhimianyun** - 集成AI用户行为分析的云桌面解决方案

### 📚 技术分享
- [CSDN博客](https://blog.csdn.net/2301_79433391?type=blog)：20+ 技术文章，涵盖AI竞赛和研究项目经验
- 开源贡献：积极参与开源项目，推动技术社区发展

## 📞 联系我们

- 🔗 **GitHub**: [Ei-Ayw](https://github.com/Ei-Ayw)
- 💬 **讨论区**: [GitHub Discussions](#)
- 🐛 **问题反馈**: [GitHub Issues](#)

---

<div align="center">

**如果这个项目对你有帮助，请给个 ⭐️ 支持一下！**

Made with ❤️ by [Ei-Ayw](https://github.com/Ei-Ayw)

</div>
