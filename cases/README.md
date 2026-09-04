# 常规案例（PDF 存放处）

本目录存放「常规案例」PDF 文件，网站「案例」区块上线后逐一在此挂载。

## 命名约定

`{品类}-{话题}-{日期}.pdf`，例如：

- `3C-小米YU7舆情追踪-20260901.pdf`
- `消费-某美妆品牌发布会监测-20260915.pdf`
- `金融-某上市公司单品追踪-20261001.pdf`

## 如何让案例显示在网站上

1. 把 PDF 文件放进本目录；
2. 编辑上一级 `index.html` 的案例区块（`<section id="cases">`）：
   - 删除 `<div class="cases-empty">…</div>` 占位块；
   - 换成案例卡片列表，链接用相对路径：`cases/xxx.pdf`。

示例（3 个卡片）：

```html
<div class="grid" style="grid-template-columns:repeat(3,1fr)">
  <a class="card" href="cases/3C-小米YU7舆情追踪-20260901.pdf" target="_blank">
    <div class="ico">🚗</div>
    <h3>3C · 小米 YU7 舆情追踪</h3>
    <p>发布前 30 天 → 发布后 30 天完整监测，含评论区情绪演变与危机预警复盘（PDF）</p>
  </a>
  <!-- 更多案例卡片... -->
</div>
```

> 手机端样式已内置响应式：`grid-template-columns` 在窄屏自动折叠为 1 列，无需额外处理。
