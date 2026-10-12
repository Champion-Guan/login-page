# Champion 登录页

一个带角色动效的单页登录界面，基于 Next.js 16、React 19 和 Tailwind CSS 4 构建。

这个项目目前专注做一件事：在当前页面内完成密码验证和登录状态展示，不跳转路由，不写入 浏览器 Cookie，也不引入额外后端服务。

## 当前特性

- 四个角色会跟随鼠标移动，并在输入密码、查看密码时做出不同反馈
- 支持浅色和深色模式切换
- 登录区域已适配桌面端和移动端
- 底部装饰元素在桌面端和移动端都会显示
- 密码校验走服务端接口，环境变量只使用 `Pwd`

## 技术栈

- Next.js 16
- React 19
- TypeScript
- Tailwind CSS 4
- Base UI
- shadcn/ui
- lucide-react

## 快速开始

1. 安装依赖

```bash
npm install
```

2. 新建 `.env.local`

```bash
Pwd=请替换为你的密码
```

3. 启动开发环境

```bash
npm run dev
```

4. 打开浏览器访问

```text
http://localhost:3000
```

## 环境变量

项目只读取一个密码环境变量：

```bash
Pwd=请替换为你的密码
```

说明：

- `Pwd` 只在服务端读取
- 前端提交密码到 `/api/login`
- 如果没有配置 `Pwd`，页面会提示“请先配置 Pwd。”

## 登录流程

1. 用户在首页输入密码并提交
2. 前端将密码发送到 `POST /api/login`
3. 服务端读取 `process.env.Pwd` 进行比对
4. 密码正确时在当前页面显示登录成功状态
5. 退出登录只清理当前页面状态

## 可用脚本

```bash
npm run dev
npm run build
npm run start
npm run lint
```

## 项目结构

```text
src/app/layout.tsx             全局布局与页面元信息
src/app/page.tsx               登录页界面、角色动画与交互逻辑
src/app/api/login/route.ts     服务端密码校验接口
src/app/全局样式.css            全局样式与主题变量
src/组件/界面/按钮.tsx         按钮组件
src/组件/界面/输入框.tsx       输入框组件
src/组件/界面/标签.tsx         标签组件
src/工具/工具.ts               通用工具函数
```

## 部署说明

可以部署到 Vercel 或其他支持 Next.js 的平台。

部署前请确认：

- 已配置环境变量 `Pwd`
- 目标平台允许 Next.js App Router 的服务端路由运行

## 校验命令

提交前建议运行：

```bash
npm run lint
npm run build
```

## 中文化范围与英文文件名保留原因

项目中的界面文案、错误提示、可读说明、源码目录、组件文件名和样式文件名均已使用中文。以下文件仍保留英文或字母数字名称，这是运行环境的识别约定，不能只改文件名而不破坏项目：

| 文件 | 不能直接改名的原因 |
| --- | --- |
| `.gitignore` | Git 只会自动读取根目录的这个固定文件名；改名后忽略规则不会生效，依赖目录和构建产物可能被误提交。 |
| `package.json` | npm、Next.js 和部署平台通过这个固定文件名读取项目脚本、依赖和项目信息；改名后无法正常安装或构建。 |
| `package-lock.json` | npm 用它锁定依赖版本和完整性校验；改名后 `npm install` 不会自动读取锁定结果。 |
| `tsconfig.json` | TypeScript 默认只自动发现这个配置文件；改名后类型检查、路径别名和 JSX 编译配置不会生效。 |
| `next.config.ts` | Next.js 只会自动加载约定的配置文件名；改名后框架无法读取配置。 |
| `postcss.config.mjs` | PostCSS 和 Tailwind CSS 通过这个约定名称加载处理配置；改名后样式构建会失败。 |
| `eslint.config.mjs` | ESLint 9 默认查找这个配置文件；改名后代码检查无法加载项目规则。 |
| `components.json` | shadcn/ui 等组件工具通过这个文件定位样式、别名和组件目录；改名后组件生成和配置读取会失效。 |
| `src/app/page.tsx` | Next.js App Router 把 `page.tsx` 识别为页面入口；改名后首页路由不再生成。 |
| `src/app/layout.tsx` | Next.js 把 `layout.tsx` 识别为根布局；改名后全局布局和元信息不再加载。 |
| `src/app/api/login/route.ts` | Next.js 把 `route.ts` 识别为接口处理器；改名后 `/api/login` 接口不存在。 |
| `src/app/favicon.ico` | 浏览器和 Next.js 会自动寻找这个固定资源名；改名只会让默认网站图标失效。 |

`src/app` 和 `src/app/api/login` 也是 Next.js 的路由目录约定。它们如果改成中文目录，必须额外改造框架配置，且会改变或破坏路由识别，因此保留原目录名。代码中的 `React`、`Next.js`、`TypeScript`、`Tailwind CSS`、包名、HTTP 方法、JSON 字段和环境变量 `Pwd` 同样属于程序接口标识，翻译后会造成构建或调用失败。

这些保留项之外，仓库中的自然语言内容和可自由命名的文件、目录已经完成中文化。
