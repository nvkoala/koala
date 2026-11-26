# koala 日程工作台 · iPhone 部署与安装指南

纯静态站点（零后端、零构建），部署后 iPhone 的 Safari 即可「添加到主屏幕」，像原生 App 一样全屏、离线运行。

## 一、部署上线（拿到 https 链接）

> 任选一种，得到 https 链接即可。

### 方式 A：Vercel（最快，推荐）

1. 打开 https://vercel.com ，用 GitHub / 邮箱登录
2. 首页点 **Add New → Project**
3. 直接把本地 `daybook` 文件夹**拖拽**进页面（或 Import Git 仓库）
4. 框架选 **Other**，点 **Deploy**
5. 约 30 秒得到链接：`https://你的项目.vercel.app`

### 方式 B：GitHub Pages（免费、稳定）

1. 登录 https://github.com → **New repository**，命名如 `koala-daybook`（选 Public）
2. 把本目录全部文件上传到仓库根目录：
   - **网页上传**：仓库页 → Add file → Upload files → 拖入 `daybook` 整个文件夹 → Commit
   - **命令行**（本目录已初始化 git）：
     ```bash
     cd /Users/shihaijuan_1/WorkBuddy/2026-11-27-00-45-54/daybook
     git remote add origin https://github.com/你的用户名/koala-daybook.git
     git push -u origin main
     ```
3. 仓库 **Settings → Pages → Source** 选 `main` 分支根目录 → **Save**
4. 等 1–2 分钟，得到链接：`https://你的用户名.github.io/koala-daybook/`

## 二、iPhone 安装成 App

1. iPhone 用 **Safari** 打开上面的 https 链接
2. 点底部 **分享按钮**（方形带↑箭头）→ 向下滑找到 **「添加到主屏幕」**
3. 右上角点 **添加**
4. 桌面出现 koala 图标，点开即全屏运行、离线可用（无 Safari 地址栏）

> 若「添加到主屏幕」后仍想更新，重新打开 https 链接即可获取最新版。

## 目录清单

```
daybook/
├── index.html          # 应用主文件（日程+周报+待办）
├── manifest.json       # PWA 清单（名称/图标/独立模式）
├── sw.js               # 离线缓存
├── .nojekyll           # 让 GitHub Pages 跳过 Jekyll 处理
├── .gitignore
├── DEPLOY.md
└── assets/             # 应用图标
    ├── icon-192.png
    ├── icon-512.png
    └── apple-touch-icon.png   # iOS 主屏幕图标（180×180）
```

## 注意事项

- 数据存手机本地（localStorage），**不跨设备同步**；换手机/清 Safari 缓存会丢数据
- 更新代码后重新部署即可；`sw.js` 里的 `CACHE` 版本号（如 `v1`→`v2`）需递增以强制刷新缓存
