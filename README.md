# 方图美妆智能

以 LIMS 与配方系统为业务底座的美妆行业智能服务官网。纯 HTML / CSS / 少量 JavaScript，无后端、无构建依赖，不使用在线字体、CDN 或访客追踪。

- 官网：https://snowleung.github.io/zhuangyanjun-web/
- 仓库：https://github.com/snowleung/zhuangyanjun-web
- 本地项目：`/Users/hans/Desktop/workspace/zhuangyanjun-web/`

仓库名与默认 Pages 子路径继续沿用，以保持已有链接可访问；展示品牌统一为「方图美妆智能」。

## 内容与事实边界

两位核心产品均使用「专家」命名，用户于 2026-10-30 确认暂未上线：

1. **方图智能实验室服务专家**：依托 LIMS，围绕委托、样品、任务和报告提供查询及业务协作介绍。读写能力受实际客户端、业务权限和确认要求约束。
2. **方图智能配方服务专家**：围绕配方系统、标准名称、配方资料与文件核对展示服务方向。具体能力与接入范围以正式发布及需求沟通为准。

两位专家都提供咨询入口，不展示虚假的安装、登录或产品体验网址。LIMS 内容依据用户给定的 [PR #371](https://github.com/snowleung/atlas_lims/pull/371) 中 README 与说明。源码交付不代表专家上架或完成真实业务验收。后续收到用户现成目录与专家描述后，可进一步细化文案。

独立工具「配方名称检查与勘误」保留已上线的 [WorkBuddy 分享入口](https://www.workbuddy.cn/share/asset?shareCode=xM1luM2P8OqMudIL4hFu3v&sig=taQ05wT5ztWrdfn9)。简介依据用户此前提供的方图配方云与 WorkBuddy AI 的 XLSX 文本、格式纠错说明。官网不安装工具，不接收配方文件，不声称已验证其实际纠错效果。

公司支持方：广东方图检测科技有限公司，https://www.atlaslabtest.com/ 。按用户既有要求，不展示资质证书栏、编号或认证标志。

英思美妆 INCILABS 用于参考行业业务场景与系统协作的呈现方式；本页不复制其图片、界面、客户、数据、功能或宣传承诺。所有业务面板标明为示意，不是软件截图，也不表示系统间已经实现自动流转。

## 文件结构

```text
index.html
css/style.css
js/main.js
assets/icons/favicon.svg
assets/images/wechat-contact.jpg
.github/workflows/pages.yml
.nojekyll
.gitignore
README.md
```

旧品牌头像已移出当前网站资源，不再发布；可在 git 历史中恢复。微信二维码保留用户提供的原始文件，页面仅通过 CSS 调整显示区域，不重绘或压缩二维码。

## 本机预览

可直接用浏览器打开 index.html。也可在项目目录执行：

```bash
python3 -m http.server 8080 --bind 127.0.0.1
```

访问 http://127.0.0.1:8080/ 。结束时按 Control+C。无需安装 npm 包。

## 维护要点

- 全站品牌、SEO、公司与产品介绍在 index.html 中维护；视觉变量在 CSS 文件开头。
- 专家真正发布后才更新「筹备中」标识，并配置用户确认的正式入口，不将 PR 或内部服务地址当作公众产品入口。
- 不要将访问凭据、真实业务数据或未脱敏文件写进官网。访问令牌仅在产品指定连接设置中填写。
- 修改微信图片时核对 `.wechat-qr-preview img` 的取景范围和识别白边；完整原图与保存入口指向同一文件。
- 外链使用 HTTPS 与 `rel="noopener"`；WorkBuddy 分享页保留完整 shareCode 和 sig，HTML 参数分隔符写为 `&amp;`。
- 保留历史锚点 `#products`、`#company`、`#expertise`、`#formula-skill`、`#contact`、`#about`。其中 `#expertise` 为接入说明，兼容既有帮助链接。
- 本页业务示意和介绍不是检测结论、配方安全评估或法规认可；实际业务需专业复核。

## 发布与验证

现有 GitHub Actions 工作流在 main 推送后自动发布，不需安装或构建。仅将 index.html、.nojekyll、css、js 和 assets 上传到 Pages，不发布 README 或 git 元数据。

```bash
git status
git add index.html css/style.css js/main.js assets README.md
git commit -m "Update Atlas Beauty Intelligence website"
git push origin main
```

发布前检查锚点和相对资源完整，手机到桌面无横向溢出，菜单、Escape、无脚本导航和微信图像正常；确认两个专家没有被误写为已上线。发布后检查最新 Actions 的提交和运行结果，并验证 HTTPS 首页与静态资源为最新版本。

## 子路径与自定义域名

资源使用 `./css/`、`./js/`、`./assets/`，兼容仓库子路径和自定义域名根目录。没有自定义域名，不创建 CNAME。现有 canonical 和 og:url 使用真实默认 Pages 地址；购买域名后同步替换为实际网址。

域名绑定顺序：默认网址部署成功 → GitHub 个人/组织 Pages 验证域名 TXT → 仓库 Pages 设置 Custom domain → 注册商 DNS → 等待验证与证书 → Enforce HTTPS。

主域名的四条 A 记录（记录名 @）：

```text
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

可选 IPv6，保留 A 的同时添加四条 AAAA：

```text
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```

www CNAME 记录指向 `snowleung.github.io`，不带协议、仓库名或路径。移除冲突的停放页 A/AAAA/CNAME，不改动无关邮件记录，不配置通配符 DNS。Actions 发布方式以 Pages 的 Custom domain 设置为准，不要求 CNAME 文件。

DNS 与证书准备可能需要等待。使用 dig 核对 A/AAAA/CNAME，再用浏览器与 curl 检查 HTTPS、重定向和页面资源。当前网络测试不等于中国大陆各地区、各运营商均可稳定访问。

- [GitHub Pages 自定义工作流](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages)
- [自定义域名与 DNS](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)
- [HTTPS](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)
