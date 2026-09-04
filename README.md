# myou.dxtools.top — 宣传站

MYOU网络情报分析师 的单页宣传网站。纯静态（HTML + 少量原生 JS），无任何构建步骤、无外部依赖、无 CDN 引用，可直接上传任何静态主机。

## 目录结构

```
myou.dxtools.top/
├── index.html      # 单页站点（自我介绍/安装/使用/案例占位/合作二维码）
├── qrcode.png      # 微信公众号「莫说闲话」搜一搜横幅（162KB）
├── cases/          # 常规案例 PDF 存放处（当前为空，见 cases/README.md）
└── README.md       # 本文件（部署说明）
```

## 本地预览

```bash
cd myou.dxtools.top
python3 -m http.server 8000
# 打开 http://localhost:8000
```

## 上线 myou.dxtools.top

已确认：`dxtools.top` 目前在 **Cloudflare**（NS = ricardo/sandy.ns.cloudflare.com），且 `myou.dxtools.top` **还没有任何 DNS 记录**（dig 无返回），需要新建记录。

### 方案 A：Cloudflare Pages（推荐，免费、免备案，域名已在 CF，5 分钟）

1. Cloudflare Dashboard → **Workers & Pages** → **Create** → **Pages** → **Upload assets**；
2. 项目名如 `myou`，把本目录所有文件（index.html、qrcode.png、cases/）拖进去 → **Deploy**；
3. Pages 项目页 → **Custom domains** → **Add custom domain** → 输入 `myou.dxtools.top`；
4. Cloudflare 自动在 DNS 里创建 `CNAME myou → <pages 域名>`，等几分钟生效。

### 方案 B：阿里云 OSS 静态网站托管（国内访问快，但需 ICP 备案）

1. OSS 建 Bucket（如 `myou-dxtools`）→ 开启「静态网站托管」（首页 index.html）；
2. 上传本目录全部文件；
3. OSS 控制台 → **域名管理** → 绑定自定义域名 `myou.dxtools.top`（需该域名已在阿里云备案，`.top` 备案需 1-2 周）；
4. 阿里云 DNS/Cloudflare DNS 加 `CNAME myou → <OSS Bucket 默认域名>`。

### 方案 C：已有服务器（nignx 或 Caddy）

上传目录到服务器后，nginx 配置示例：

```nginx
server {
    listen 80;
    server_name myou.dxtools.top;
    root /var/www/myou.dxtools.top;
    index index.html;
    location / { try_files $uri $uri/ =404; }
}
```

然后在 Cloudflare DNS 添加：`A 记录 myou → <服务器 IP>`（后续可开代理加 HTTPS）。

## 上线后自查

```bash
dig +short myou.dxtools.top     # 应返回解析结果
curl -I https://myou.dxtools.top   # 应返回 200，Content-Type: text/html
```

## 内容更新提示

- 案例上架：见 `cases/README.md`；
- 二维码更换：直接覆盖 `qrcode.png`（建议宽 ≥ 800px 的 PNG/JPG）。
