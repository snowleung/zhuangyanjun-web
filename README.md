# 妆研君｜你的美妆行业 AI 搭档

中文响应式品牌官网。纯 HTML、CSS 和少量 JavaScript；零后端、零构建依赖。所有字体来自系统，所有图片与图标来自本地文件，无 CDN、广告或使用分析脚本。

## 当前状态

- 页面开发完成；服务领域为拟支持场景，Skill、MCP、AI Agent 均明确标为「规划中」。
- 使用用户 Mac 桌面原有的 `妆研君_WorkBuddy_头像.jpg`（768 × 768，96,787 字节）。
- 微信合作联系二维码待用户提供。没有虚构邮箱、二维码、客户案例、业务资质或在线提交功能。
- GitHub Pages 工作流已准备；尚未创建远端仓库、推送或启用 Pages，没有实际公开网址。
- 用户自行购买域名。目前没有 `CNAME` 文件、伪造 canonical 或域名解析配置。

## 项目文件

```text
zhuangyanjun-web/
├── index.html                   # 内容、SEO 基础信息、合作入口与声明
├── css/style.css                # 所有视觉与响应式样式
├── js/main.js                   # 手机导航与页脚年份
├── assets/
│   ├── images/zhuangyanjun-avatar.jpg
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

### 接入微信合作二维码

仅使用确认允许公开的业务联系人二维码，勿发布个人支付码。把二维码保存为 `assets/images/wechat-contact.png`，将 `index.html` 联系卡内的 `.qr-placeholder` 整块替换为：

```html
<img class="wechat-qr" src="./assets/images/wechat-contact.png"
     alt="妆研君合作联系人微信二维码，请使用微信扫一扫添加"
     loading="lazy">
```

把「合作联系渠道筹备中。二维码补充后，可扫码添加联系人。」改成「打开微信扫一扫，添加联系人。欢迎说明你的业务场景与合作想法。」；同步更新本文件的当前状态。手机端访客可保存二维码后在微信中识别。接入后应实际用微信验证能添加正确联系人，并定期确认二维码有效。

## GitHub Pages 部署

### 1. 远端发布前需确认

确认 GitHub 账号或组织、仓库名 `zhuangyanjun-web`、公开范围，以及是否允许推送和公开部署。GitHub 免费个人方案使用公开仓库；其他套餐支持的范围请查官方文档。二维码等业务联系方式一旦部署会公开可见。此项目未附加开源许可证，发布到公开仓库不等于授予开放源代码许可。

本次检查中，GitHub CLI 对账号 `snowleung` 的现有凭据报告无效。若由代理继续发布，先通过 GitHub 的正常登录流程恢复授权；不要把访问令牌发到聊天或写进项目。以下命令是**确认发布后的操作示例，本次没有执行**。

```bash
gh auth login --hostname github.com --web
gh auth status
cd ~/Desktop/workspace/zhuangyanjun-web
git add .
git commit -m "feat: add Zhuangyanjun static brand website"
gh repo create zhuangyanjun-web --public --source=. --remote=origin --push
```

若仓库已存在，先核对其内容与地址，不能直接覆盖或强制推送。独立的本地 git 初始化不会创建远端或自动发布。

### 2. 启用 Pages

打开该仓库 **Settings → Pages → Build and deployment → Source → GitHub Actions**。不要同时启用另一种发布来源。到 **Actions** 手动运行 `Deploy static website to GitHub Pages`；之后每次推送到 `main` 会自动更新。

工作流直接整理和发布静态文件，无安装或构建步骤。它只上传 `index.html`、`.nojekyll`、`css/`、`js/`、`assets/`，不把 README、git 元数据、工作记录等部署到网站。

工作流完成后，从 **Settings → Pages** 或工作流的 **github-pages** 环境链接取得真实 URL。项目站点通常是：

```text
https://<OWNER>.github.io/zhuangyanjun-web/
```

这里的 `<OWNER>` 必须替换为实际用户或组织。这个地址仅表示格式，当前不是已上线链接。默认仓库项目站点保留末尾 `/`，否则某些相对资源解析可能受影响。

### 3. 仓库子路径和自定义域名

所有页面资源使用 `./assets/...`、`./css/...`、`./js/...`，站内链接使用 `#section`。不使用 `/assets/...`，不写死仓库名或域名，不添加 `<base>`。因此同一份源码可部署于仓库子路径或自定义域名根目录，也可直接打开本地文件。

确定真实公开网址后，在 `index.html` 的 SEO 注释位置加入**真实绝对 URL**：

```html
<link rel="canonical" href="https://你的真实站点地址/">
<meta property="og:url" content="https://你的真实站点地址/">
<meta property="og:image" content="https://你的真实站点地址/assets/images/zhuangyanjun-avatar.jpg">
<meta property="og:image:alt" content="妆研君品牌虚拟研究员头像">
```

以上示例不能原样填写：若使用 GitHub 默认网址，三个地址都应带实际仓库子路径。`description`、Open Graph 文案、页面语言、标题、favicon 和 viewport 已配置。当前有意省略未确定的 canonical、分享图片绝对网址、站点地图与 robots.txt 域名信息。

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

本机网络测试只能证明当前网络访问情况。若面向中国大陆访客，应在不同运营商、不同地区和移动网络实际打开测试。绑定域名本身并不保证 GitHub Pages 在各地稳定连通；当前没有完成真实公开部署和跨地区连通性验证。

## 资料与隐私边界

网站只介绍品牌与规划，不提供配方安全、检测或法规结论，不声称拥有业务资质。法规与证照信息需以适用地区的有效官方材料为准，重要决定需专业人员复核。未来系统接入和产品的数据处理政策应在真实发布前另行明确。本页无在线资料收集功能，勿通过公开渠道发送未脱敏资料。

## 官方参考

- [GitHub Pages 自定义工作流](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages)
- [管理自定义域名：DNS 与 CNAME 发布方式区别](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)
- [验证自定义域名](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages)
- [GitHub Pages HTTPS](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)
