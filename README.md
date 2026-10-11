# 隐私币导航 · 维护说明

单文件静态站（`index.html` 内联 CSS/JS，无构建步骤），可直接部署到 GitHub Pages。

## 文件结构

```
privacy-nav/
├── index.html            # 主页面（全部内容）
├── data/
│   └── listings.json     # 上架状态数据源（每周人工更新）
├── robots.txt
├── sitemap.xml           # 上线后把域名换成实际地址
├── llms.txt
└── README.md
```

## 每周更新上架状态

1. 打开各交易所官网（或公告页），核对 ZEC / XMR / DASH 的上架情况。
2. 编辑 `data/listings.json`：
   - `status` 可选值：`listed`（上架）/ `delisted`（已下架）/ `restricted`（地区限制）/ `unknown`（待核实）
   - **无法核实的单元格一律填 `unknown`，不要猜测。**
   - `n` 字段写备注（如"2026-11-03 公告下架"）。
   - 把顶部的 `updated` 改成当天日期。
3. 同步修改 `index.html` 里的两处：
   - 内联兜底数据 `FALLBACK_LISTINGS`（与 listings.json 保持一致；它是 JSON 被拦截/本地 file:// 打开时的备份）
   - 看板下方的「数据更新于 2026-10-11」字样和页脚日期。
4. 重新部署（git push）即可，无需构建。

## 推广位（邀请链接）

- 币安邀请链接（**原文照用，不要改动**）：
  `https://account.binance.com/register?ref=WBBI3YKV&?registerChannel=user_center`
  出现位置：页眉 CTA、Hero、看板 Binance 行（ZEC/DASH）、对比区 CTA、XMR 指南步骤 1、NU7 区 CTA。
- 欧易：仅以文字展示邀请码 `欧易邀请码：3417211`，**不要编造欧易邀请链接**。
- 统一话术：`通过邀请链接注册，最高享40%手续费减免（以币安官方页面为准）`

## 部署（GitHub Pages）

```bash
cd ~/workspace/privacy-nav
git init && git add . && git commit -m "隐私币导航 v1"
# 建空仓库后：
git remote add origin https://github.com/jxsite/privacy-nav.git
git push -u origin main
# 仓库 Settings → Pages → Deploy from branch → main / (root)
```

上线后把 `sitemap.xml`、`robots.txt` 和 `index.html` 里 JSON-LD 的
`https://jxsite.github.io/privacy-nav/` 换成实际域名（如有变动）。

## 注意事项

- XMR 相关内容必须保持"两步走"口径：**绝不暗示 XMR 可在币安直接购买**（2024-02-20 已下架）。
- 欧盟 AMLR 2027-07-01 生效后，需复核全站合规表述。
- NU7 倒计时目标为 2026-11-05，到期后页面会自动显示提示文案；升级完成后可将该模块替换为下一热点。
