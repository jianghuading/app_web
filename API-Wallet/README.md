# API Wallet 官网页面

API 钱包（API Wallet）的产品落地页 / App Store 支持页。纯静态单页，无需构建工具。

## 文件结构

```
API-Wallet/
├── index.html          # 页面本体（脚本与默认中英文案内嵌）
├── css/
│   └── style.css       # 样式表
├── image/
│   └── icon.png        # App 图标
└── i18n/
    └── locales.csv     # 多语言文案表（key, zh_CN, en_US）
```

## 多语言说明

- 语言代码使用 `xx_XX` 下划线格式，目前支持 `zh_CN`（简体中文，默认）与 `en_US`。
- **页面会直接读取 `i18n/locales.csv`**：部署到服务器后，改 CSV 重新上传即可生效（浏览器不缓存，`cache: no-store`）。
- CSV 第一列固定为 `key`，其余每列是一种语言，列名即语言代码。
- **新增语言 = 在 CSV 里加一列**（如 `ja_JP`），刷新后语言切换器会自动出现该语言。
- `index.html` 内嵌了同样的默认文案，因此直接双击打开（file:// 协议，无法 fetch CSV）也能正常显示两种语言。

### 本地预览（让 CSV 生效）

```bash
cd API-Wallet
python3 -m http.server 8080
# 浏览器打开 http://localhost:8080
```

### 更新文案的正确姿势

1. 只改 `i18n/locales.csv`，不要动 `index.html`；
2. 若在本地 file:// 下预览，需走上面的本地服务器方式；
3. 把 `index.html`、`i18n/locales.csv`、`icon.png` 一起上传到服务器。

> 注意：`index.html` 内嵌文案是 CSV 的兜底副本。若长期只改 CSV，建议偶尔用 CSV 内容同步回内嵌 JSON（保持两者一致），避免某台设备缓存旧 CSV 时显示旧文案。

## 常用配置

- **App Store 链接**：在 `index.html` 搜索 `APP_STORE_URL`（脚本开头），填入商店链接；留空时按钮显示「即将上线 App Store」。
- **隐私政策**：页脚指向 `../Privacy/privacy_zh_CN.html` / `privacy_en_US.html`（App_Web/Privacy 目录下的通用隐私协议，随站点结构一起部署）。
- **更换图标**：替换 `image/icon.png` 后，记得把 `index.html` 里的 `image/icon.png?v=2` 同步改成 `?v=3`、`?v=4`……（三处：favicon、导航、页脚），否则访问过旧页面的浏览器会继续显示缓存的旧图标。

## 联系方式（页面内已使用）

- 技术支持 / 建议：support@suzatei.com
- 合作 / 投资：contact@suzatei.com

© 2026 Suzatei. All rights reserved.
