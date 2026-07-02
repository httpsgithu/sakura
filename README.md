# Sakura

一个 WebGL 樱花页面，用于 Cloudflare Workers 部署测试。

## 实现方法

这个仓库原来是纯静态页面，入口文件是 `bg.html`。为了适配 Cloudflare Workers，我把页面文件整理到了 `public/` 目录，并把入口改成 `public/index.html`。Wrangler 会把 `public/` 当作静态资源目录上传，访问根路径 `/` 时就会返回这个页面。

保留了旧路径：

- `/bg`
- `/bg.html`

这两个路径会通过 `public/_redirects` 跳回 `/`，旧链接还能继续用。

## 文件结构

```text
public/
  index.html
  _redirects
  css/
  js/
wrangler.jsonc
package.json
```

`wrangler.jsonc` 里只做了静态资源配置：

```jsonc
{
  "name": "sakura",
  "compatibility_date": "2026-07-02",
  "assets": {
    "directory": "./public",
    "html_handling": "auto-trailing-slash"
  }
}
```

## 本地预览

```bash
npm install
npm run dev
```

默认会启动 Wrangler 本地服务。打开终端里显示的 localhost 地址就能预览。

## 部署

先做一次检查：

```bash
npm run check
```

确认没问题后部署：

```bash
npm run deploy
```
