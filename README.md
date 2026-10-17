# 妆研君｜你的美妆行业 AI 搭档

中文响应式品牌官网。纯 HTML、CSS 和少量 JavaScript；零后端、零构建依赖。所有字体来自系统，所有图片与图标来自本地文件，无 CDN、广告或使用分析脚本。

## 当前状态

- 页面开发完成；AI 服务领域为拟支持场景，Skill、MCP、AI Agent 均明确标为「规划中」。
- 已加入方图检测公司介绍、专业服务与公司主页入口；页脚展示「专业支持方：广东方图检测科技有限公司」。按用户要求不展示资质证书栏、证书编号或认证标志。
- 使用用户 Mac 桌面原有的 `妆研君_WorkBuddy_头像.jpg`（768 × 768，96,787 字节）。
- 已接入用户提供的微信合作联系二维码（联系人 HHans），支持查看原图与保存图片。未虚构邮箱、客户案例、业务资质或在线提交功能。
- 远端仓库：[snowleung/zhuangyanjun-web](https://github.com/snowleung/zhuangyanjun-web)。
- 默认官网地址：[https://snowleung.github.io/zhuangyanjun-web/](https://snowleung.github.io/zhuangyanjun-web/)。发布结果以 [Pages 工作流](https://github.com/snowleung/zhuangyanjun-web/actions/workflows/pages.yml) 的最新运行和实际访问结果为准。
- 用户自行购买域名。目前没有自定义域名或 `CNAME` 文件；canonical 和分享信息使用真实的 GitHub Pages 项目网址。

## 项目文件

```text
zhuangyanjun-web/
├── index.html                   # 内容、SEO 基础信息、合作入口与声明
├── css/style.css                # 所有视觉与响应式样式
├── js/main.js                   # 手机导航与页脚年份
├── assets/
│   ├── images/zhuangyanjun-avatar.jpg
│   ├── images/wechat-contact.jpg # 用户提供的原始二维码图片
│   └── icons/favicon.svg        # 本地矢量品牌标识
├── .github/workflows/pages.yml  # 只发布网页和公开资源
├── .gitignore
├── .nojekyll
└── README.md
```

## 本地预览

直接用浏览器打开 `index.html` 即可查看。推荐用本地 HTTP 服务检查真实地址与图片加载（Mac 已安装 Python 3 时）：

```bash
cd ~/Desktop/workspace/zhuangyanjun-web
python3 -m http.server 8080 --bind 127.0.0.1
```

访问 `http://127.0.0.1:8080/`，结束时在启动服务的终端按 `Control+C`。这只是本机预览，不是互联网公开访问地址，不需要安装 npm 包。

## 日常维护

- 内容与产品状态：编辑 `index.html`；只有确实上线的能力才能改成可用，并补充真实使用入口。
- 颜色与间距：编辑 `css/style.css` 开头的 CSS 变量。
- 头像：替换 `assets/images/zhuangyanjun-avatar.jpg`，保持方形；更改格式时同时修改页面中两处头像地址。
- favicon：替换 `assets/icons/favicon.svg`；它是可维护的简洁分子标识。
- 不要加入未证实的功效、成功率、客户、资质、证照编号或上线时间。

### 维护微信合作二维码

当前使用用户提供的 `IMG_6799.JPG`，逐字节复制为 `assets/images/wechat-contact.jpg`（888 × 1191）。文件没有裁剪、压缩或重绘；网页通过 CSS 突出显示二维码区域并保留白色边距，查看原图和下载始终使用完整原始图片。

更新二维码时，替换该文件，并核对联系人名称、图片尺寸与 CSS 中 `.wechat-qr-preview img` 的取景位置。如果换成四周已有白色边距的方形二维码，可将该选择器改为 `position: static; width: 100%; max-width: 100%; height: auto;`，同时更新 HTML 图片的 width/height。保留完整二维码与识别所需的白色边距，不要拉伸或重绘。

手机端可点击「保存二维码」，在微信中识别所存图片；若浏览器改为直接打开图片，可长按保存。上线前仍应实际用微信确认能添加正确联系人，并定期确认二维码有效。本次仅验证文件、网页展示和原图/下载入口，不声称已经在微信中完成扫码添加。

## GitHub Pages 部署

### 1. 已有远端仓库

本项目使用公开仓库 `snowleung/zhuangyanjun-web`，本地 `main` 对应远端 `origin/main`。无需再次创建仓库。公开仓库内的源码与业务二维码可被互联网访客访问；网站只发布页面及公开资源。

确认更改后，在项目目录提交并推送即可触发部署：

```bash
cd ~/Desktop/workspace/zhuangyanjun-web
git status
git add index.html css/style.css js/main.js assets README.md .github/workflows/pages.yml
git commit -m "Update website content"
git push origin main
```

若出现登录问题，先执行 `gh auth status`；网络受限也可能导致认证检查失败，应确认网络连接后再判断凭据状态。确需重新登录时，使用 `gh auth login --hostname github.com --web`，不要把访问令牌发到聊天或写进项目。不要覆盖或强制推送其他人的提交。

### 2. 启用 Pages

本仓库使用 **Settings → Pages → Build and deployment → Source → GitHub Actions**。每次推送到 `main` 自动发布；需要时也可以在 **Actions** 手动运行 `Deploy static website to GitHub Pages`。不要同时启用另一种发布来源。

工作流直接整理和发布静态文件，无安装或构建步骤。它只上传 `index.html`、`.nojekyll`、`css/`、`js/`、`assets/`，不把 README、git 元数据、工作记录等部署到网站。

工作流完成后，可从 **Settings → Pages** 或 **github-pages** 环境链接打开网站：

```text
https://snowleung.github.io/zhuangyanjun-web/
```

保留项目网址末尾 `/`，确保相对资源正确解析。若页面尚不可访问，先检查最新部署运行，不要仅凭 URL 格式认定上线成功。

### 3. 仓库子路径和自定义域名

所有页面资源使用 `./assets/...`、`./css/...`、`./js/...`，站内链接使用 `#section`。不使用 `/assets/...`，不写死仓库名或域名，不添加 `<base>`。因此同一份源码可部署于仓库子路径或自定义域名根目录，也可直接打开本地文件。

目前 `index.html` 的 canonical、og:url 和 og:image 已使用默认 Pages 网址。将来绑定自定义域名后，将这些值一起改成**新的真实绝对 URL**：

```html
<link rel="canonical" href="https://你的真实站点地址/">
<meta property="og:url" content="https://你的真实站点地址/">
<meta property="og:image" content="https://你的真实站点地址/assets/images/zhuangyanjun-avatar.jpg">
<meta property="og:image:alt" content="妆研君品牌虚拟研究员头像">
```

以上示例不能原样填写。GitHub 默认网址的三个地址均带 `/zhuangyanjun-web/` 子路径；自定义域名通常使用根目录。`description`、Open Graph 文案、页面语言、标题、favicon 和 viewport 已配置。当前没有生成站点地图或包含自定义域名信息的 robots.txt。

## 域名选择

按品牌一致性优先查询：

| 候选 | 适用理由 |
| --- | --- |
| `zhuangyanjun.com` | 完整品牌拼音，首选，便于长期使用 |
| `cosmejun.com` | 字符更短，兼顾美妆与品牌感 |
| `zyjun.com` | 简短，但需要额外解释与品牌关联 |
| `zhuangyanjun.cn` | 中文品牌导向的备选 |

未确认注册可用性、价格或商标权利；以注册商实时查询与续费报价为准。不要仅为低首年价格忽略续费成本。绑定哪个域名，应以用户实际购买并确认的域名为准。

## 购买后绑定 DNS 与 HTTPS

以下 DNS 值在 2026-10-14 对照 GitHub 官方资料核实；实际操作前可再次核查文末官方链接。`example.com` 仅为示例，不能写进当前项目。

### 推荐顺序

1. 先让默认 GitHub Pages 网址部署成功。
2. 在 GitHub **个人或组织 Settings → Pages** 添加并验证域名，按页面返回的名称和值创建 TXT 记录。保留 TXT 记录；不要猜测验证令牌。
3. 在**仓库 Settings → Pages → Custom domain** 填写已购买的首选域名并保存。
4. 再到域名注册商添加网站 DNS 记录，避免域名先指向 GitHub 却没有绑定到自己的仓库。
5. 等待 GitHub DNS 检查与证书准备完成，再启用 **Enforce HTTPS**，并测试主域和 www 的访问与重定向。DNS 传播及 HTTPS 选项准备可能需要等待至 24 小时。

### 主域名（例如 example.com）

在 DNS 中添加四条 `A`，记录名均为 `@`：

```text
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

需要 IPv6 时，额外添加四条 `AAAA`，记录名均为 `@`；同时保留上面的 IPv4 `A` 记录：

```text
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```

TTL 可先使用注册商默认值。不要保留指向停放页或其他服务器的冲突 A/AAAA 记录，也不要改动正常使用的邮件 MX/TXT 等无关记录。

### www 子域名

添加一条 `CNAME`：

| 类型 | 记录名 | 记录值 |
| --- | --- | --- |
| CNAME | `www` | `<OWNER>.github.io` |

值只包含实际 GitHub 用户或组织的主机名；**不带 `https://`、仓库名、斜杠或路径**。www 不应同时存在冲突的 A/AAAA 记录。两者都配置正确时，GitHub 可在主域和 www 之间重定向，以 Pages 设置中的 Custom domain 为首选。

### 关于 CNAME 文件

本项目默认使用 GitHub Actions 发布。官方文档说明：这种发布方式以 Pages 设置的 Custom domain 为准，`CNAME` 文件不必创建，存在时也被忽略。因此购买域名后也不必为了 Actions 部署生成 `CNAME`。

只有日后主动改用 **Deploy from a branch** 时，才应在真实域名确定后由 Pages 设置创建或维护 `CNAME`，文件只写一行已购买域名。不配置通配符 DNS（如 `*`）。

## 上线验证清单

### 默认网址

- Actions 运行成功，Pages 设置显示实际部署地址。
- 首页、CSS、JS、头像和 favicon 均返回 200，且没有浏览器控制台错误。
- 在桌面和 320–430px 手机宽度检查文字、导航、微信二维码及所有锚点，无横向溢出。
- 禁用 JavaScript 时，全部内容和导航仍可访问。
- 未准备好上线的产品继续标为「规划中」，联系二维码实际指向正确联系人。

### 自定义域名

购买后替换示例域名再运行：

```bash
dig example.com A +short
dig example.com AAAA +short
dig www.example.com CNAME +short
curl -I https://example.com/
curl -I https://www.example.com/
curl -I http://example.com/
```

核对 A/AAAA/CNAME 与上文一致。HTTPS 首页应成功响应，www 与主域按首选域名重定向，HTTP 在强制 HTTPS 后重定向到 HTTPS。再打开页面检查安全锁、资源和微信联系入口；不要只看 DNS 命令成功。

本机网络测试只能证明当前网络访问情况。若面向中国大陆访客，应在不同运营商、不同地区和移动网络实际打开测试。绑定域名本身并不保证 GitHub Pages 在各地稳定连通；本机网络检查不能替代跨地区连通性验证；未完成中国大陆多地区、多运营商访问测试。

## 资料与隐私边界

网站介绍 AI 品牌与规划，以及专业支持方的业务信息；不直接提供配方安全、检测或法规结论，也不展示业务资质声明。法规与证照信息需以适用地区的有效官方材料为准，重要决定需专业人员复核。未来系统接入和产品的数据处理政策应在真实发布前另行明确。本页无在线资料收集功能，勿通过公开渠道发送未脱敏资料。

## 官方参考

- [GitHub Pages 自定义工作流](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages)
- [管理自定义域名：DNS 与 CNAME 发布方式区别](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)
- [验证自定义域名](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages)
- [GitHub Pages HTTPS](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)

## 公司介绍维护

专业支持方为广东方图检测科技有限公司，官网为 [方图检测](https://www.atlaslabtest.com/)。公司全称与基础介绍于 2026-10-17 对照官网核对；申报、出口合规等服务文案依据用户提供的信息。页面使用「专业支持方」标注，不推定品牌法律归属。按用户最新要求，不加入 CNAS/CMA 证书展示、编号或认证标志。公司介绍放在「认识妆研君」和「服务领域」之间，锚点为 `#company`；AI 产品继续明确标为「规划中」。更新时同步检查页脚的主体名称与链接，不复制公司网站的备案号到本网站。
