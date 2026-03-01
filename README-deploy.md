# AI焦虑指数测试 H5 — 部署教程

## 项目概述

一个基于 Swiper.js 的全屏滑动式心理测试 H5 页面，纯前端项目（无后端），可直接部署为静态站点。

### 文件说明

```
AI焦虑指数测试H5/
├── index.html          ← 主版本（部署此文件）
├── index-小红书版.html   ← 小红书版（备用，暂不部署）
├── 策划案.md            ← 策划文档
└── README.md           ← 本文件
```

### 外部依赖（全部通过 CDN 加载，无需安装）

| 依赖 | 用途 | CDN |
|------|------|-----|
| Swiper 11 | 全屏滑动交互 | jsDelivr |
| html2canvas 1.4.1 | 结果卡片截图保存 | jsDelivr |
| Google Fonts | Space Grotesk + Noto Sans SC 字体 | Google Fonts |

---

## 部署方案：Vercel

### 前置条件

1. 一个 [GitHub](https://github.com) 账号
2. 一个 [Vercel](https://vercel.com) 账号（用 GitHub 登录即可）

### 第一步：创建 GitHub 仓库

1. 打开 https://github.com/new
2. 仓库名：`ai-anxiety-test`（或你喜欢的名字）
3. 选择 **Private**（私有）
4. 点击 **Create repository**

### 第二步：上传文件到 GitHub

**方式 A：命令行（推荐）**

打开终端，执行：

```bash
# 进入项目目录
cd "/Users/jameezhao/Documents/AI工作流/加米实验室/02-创作区/00-创作中/AI焦虑指数测试H5"

# 初始化 Git
git init
git add index.html

# 提交
git commit -m "初始版本：AI焦虑指数测试H5"

# 关联远程仓库（替换成你的 GitHub 用户名）
git remote add origin https://github.com/你的用户名/ai-anxiety-test.git
git branch -M main
git push -u origin main
```

**方式 B：GitHub 网页上传**

1. 进入刚创建的仓库页面
2. 点击 **Add file → Upload files**
3. 拖入 `index.html`
4. 点击 **Commit changes**

### 第三步：Vercel 部署

1. 打开 https://vercel.com/new
2. 点击 **Import Git Repository**
3. 选择刚才创建的 `ai-anxiety-test` 仓库
4. 配置页面保持默认即可：
   - **Framework Preset**: `Other`
   - **Build Command**: 留空
   - **Output Directory**: 留空（默认 `.`）
5. 点击 **Deploy**
6. 等待 10-30 秒，部署完成

### 第四步：获取访问链接

部署成功后，Vercel 会分配一个域名：

```
https://ai-anxiety-test.vercel.app
```

访问地址：

```
https://你的项目名.vercel.app/
```

即 `index.html`，Vercel 会自动识别为首页。

### 第五步（可选）：绑定自定义域名

1. 在 Vercel 项目面板 → **Settings → Domains**
2. 添加你的域名，如 `test.jamstudio.co`
3. 按提示在域名 DNS 中添加 CNAME 记录：
   - 类型：`CNAME`
   - 名称：`test`（或你想要的子域名）
   - 值：`cname.vercel-dns.com`
4. 等待 DNS 生效（通常几分钟，最长 48 小时）

---

## 更新部署

每次修改文件后，只需重新推送到 GitHub，Vercel 会自动重新部署：

```bash
cd "/Users/jameezhao/Documents/AI工作流/加米实验室/02-创作区/00-创作中/AI焦虑指数测试H5"
git add .
git commit -m "更新内容"
git push
```

大约 10-30 秒后新版本自动上线。

---

## 桌面端兼容性说明

项目原本为手机端设计（全屏竖屏滑动），桌面浏览器打开时会出现以下问题：

### 当前问题

1. **内容拉伸变形** — 宽屏下内容区域过宽，留白不自然
2. **滑动交互不直觉** — PC 用户习惯滚轮滚动，不习惯"整屏滑动"
3. **字体比例失调** — `clamp()` 值针对手机优化，桌面上偏小

### 已添加方案：手机模拟框（无需额外操作）

两个 HTML 文件已内置桌面端适配 CSS，桌面端打开会自动用 iPhone 造型的手机框居中展示，深色背景，手机端完全不受影响。

---

## CDN 加速说明

### Vercel 自带 CDN

Vercel 默认通过其 Edge Network 全球分发静态文件，**国际访问**速度已经很好，不需要额外配置 CDN。

### 中国大陆加速

Vercel 的 CDN 节点不在中国大陆，国内用户访问可能偏慢（1-3秒）。如需优化：

**方案 1：Cloudflare 免费加速（推荐）**

1. 注册 [Cloudflare](https://cloudflare.com)（免费）
2. 将你的域名 DNS 转入 Cloudflare
3. 添加 CNAME 记录指向 `cname.vercel-dns.com`
4. 开启 Cloudflare 代理（橙色云朵图标）
5. Cloudflare 会自动缓存静态文件，国内有节点加速

**方案 2：国内云服务部署**

如果主要受众在国内，可以考虑：
- **腾讯云 COS + CDN**：将 HTML 文件上传到 COS 存储桶，开启 CDN 加速
- **阿里云 OSS + CDN**：类似方案
- **Netlify**：也有免费静态托管，但和 Vercel 类似，节点不在国内

> 对于测试链接的场景（短时间内集中访问），Vercel + Cloudflare 通常够用。

### 外部资源 CDN 情况

页面依赖的外部资源全部来自 jsDelivr 和 Google Fonts：

| 资源 | 国内可用性 |
|------|-----------|
| jsDelivr（Swiper、html2canvas） | 国内有节点，速度良好 |
| Google Fonts | 国内可能较慢或偶尔不可用 |

**如果 Google Fonts 加载慢**，可以替换为国内镜像，在两个 HTML 文件中将：

```html
https://fonts.googleapis.com
https://fonts.gstatic.com
```

替换为：

```html
https://fonts.googleapis.cn
https://fonts.gstatic.cn
```

（googleapis.cn 是 Google 提供的中国大陆加速域名）

---

## 测试清单

部署成功后，用手机和电脑分别打开链接，检查：

- [ ] 封面页正常显示，点击「开始测试」可进入
- [ ] 8道题依次滑动，题号和进度条正确（1/8 → 8/8）
- [ ] 选择选项后自动滑到下一题
- [ ] Loading 动画正常播放
- [ ] 结果页显示：分数、人物名称、金句、SVG 火柴人
- [ ] 雷达图正常渲染
- [ ] 冷知识页显示 4 条数据
- [ ] 分享卡片包含截图金句（tagline）
- [ ] 「保存图片」按钮可下载 PNG
- [ ] 「再测一次」回到封面，选项重置
- [ ] 桌面端显示手机模拟框（已内置）

---

## 常见问题

**Q: 部署后页面空白？**
A: 检查 Vercel 的 Output Directory 是否为空（默认根目录），确保 `index.html` 在仓库根目录下。

**Q: 字体加载慢/不显示？**
A: Google Fonts 在国内偶尔不稳定，替换为 `googleapis.cn` 镜像即可。

**Q: 保存图片功能不工作？**
A: html2canvas 在部分浏览器（尤其微信内置浏览器）可能受限，会 fallback 显示「长按卡片即可保存」的提示。

