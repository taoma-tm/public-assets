# public-assets

对外公开的个人静态资源仓库。当前用途：为会议 Program Committee 页面提供头像图片直链。

## 目录结构

```
public-assets/
├── README.md
├── .gitignore
└── images/
    ├── tao-ma-headshot.jpg          # 竖版原图 1279×1724
    └── tao-ma-headshot-square.jpg   # 1:1 头肩裁切 1279×1279
```

## 一、放照片

把头像放到 `images/tao-ma-headshot.jpg`。

命名规范：全小写、英文、连字符分隔。不要用中文或空格——URL 里会被转义成 `%E9%A9%AC...`，部分会议投稿系统处理不了。

以后换照片**沿用同一文件名**，已发出去的链接就不用改。换图后记得同步重出方形版。

## 二、生成链接

用 jsDelivr CDN：

```
https://cdn.jsdelivr.net/gh/taoma-tm/public-assets@main/images/tao-ma-headshot.jpg
```

**更稳的做法：打 tag，用 tag 代替分支名。** 分支引用（`@main`）在 CDN 侧有缓存，换图后不会立即生效；tag 和 commit SHA 是不可变引用，适合交给会议方长期挂载。

```bash
git tag v1
git push origin v1
```

对应链接：

```
https://cdn.jsdelivr.net/gh/taoma-tm/public-assets@v1/images/tao-ma-headshot.jpg
```

### 方形版

委员会页面若按正方形或圆形展示头像，用这张：

```
https://cdn.jsdelivr.net/gh/taoma-tm/public-assets@v1/images/tao-ma-headshot-square.jpg
```

### 为什么不用 raw.githubusercontent.com

2026-11-12 从本机实测：

| 地址 | 结果 |
| --- | --- |
| `cdn.jsdelivr.net` | HTTP 200，0.85s |
| `raw.githubusercontent.com` | 连接超时，15s 无响应 |

raw 链接在国内网络下不可靠。会议方多半在海外能打开，但你自己验证不了，发出去心里没底。jsDelivr 两边都通。

## 三、照片规格

- 比例：正方形 1:1（多数委员会页面会裁成圆形）
- 尺寸：≥ 1200×1200
- 格式：JPG，建议 < 2MB
- 内容：正面免冠、纯色浅背景、商务着装、肩部以上
- 不要水印、logo、边框

当前两个文件：竖版原图 1279×1724、270KB；方形版 1279×1279、127KB。方形版为顶部对齐裁切，保留完整头顶与头肩，底边落在交叉手臂处；不要直接拉伸变形。

## 四、发布前验证

链接必须是**图片直链**：浏览器打开直接显示照片，而不是下载页、登录页或分享页。

```bash
curl -sI "https://cdn.jsdelivr.net/gh/taoma-tm/public-assets@v1/images/tao-ma-headshot.jpg"
```

期望看到 `HTTP/2 200` 和 `content-type: image/jpeg`。

再用浏览器无痕窗口打开一次，确认不登录也能看到图。

## 五、许可

**不加 LICENSE 文件。** 没有许可证即默认保留所有权利，这正是肖像想要的状态；套 MIT / CC-BY 等于允许任何人复用你的照片。

授权范围：仅允许会议方在指定的 Program Committee 页面展示。如需书面授权，单独发函，不在仓库里放宽松许可证。

## 六、发布 checklist

- [x] 照片放入 `images/tao-ma-headshot.jpg`（1279×1724，270KB）
- [x] 方形裁切版 `images/tao-ma-headshot-square.jpg`（1279×1279，127KB）
- [x] 链接用户名已填为 `taoma-tm`（账号存在、仓库名未占用，均已核实）
- [x] 许可：不加 LICENSE，保留所有权利
- [ ] 在 GitHub 建**公开**仓库并推送
- [ ] 打 tag `v1` 并推送
- [ ] curl + 无痕窗口双重验证直链
- [ ] 把链接发给会议方