# TVBox 点播源配置

个人用的点播源分发仓，供「影视盒」（鸿蒙智慧屏）与安卓影视仓导入。

## 文件

| 文件 | 内容 | 适用 |
|---|---|---|
| `4kvm-sites.json` | 4K影视站群，4 个镜像域名（网页规则 type=9） | 鸿蒙「影视盒」、Kazumi |
| `tvbox4k-fish.json` | 第三方 4K 合集，111 个 spider 站（type=3） | 仅安卓影视仓；鸿蒙端会全部过滤 |

## 导入

把 raw 地址粘到 App 的「点播源」输入框即可：

```
https://raw.githubusercontent.com/cubacupa/tvbox-sites/main/4kvm-sites.json
```

```
https://raw.githubusercontent.com/cubacupa/tvbox-sites/main/tvbox4k-fish.json
```

raw 地址两个注意点：

- 必须是 `raw.githubusercontent.com`，换成 `github.com/.../blob/...` 拿到的是网页 HTML，导入会失败
- 仓库必须是 public。私有仓的 raw 要带 token，App 拉不到

## 说明

**`4kvm-sites.json`** — 4 个域名同一套规则，`4K影视` / `②` / `③` / `④`：

- 主站 `www.4kvm.tv`，备用 `www.4kvm.me`、`www.4kvm.net`、`www.4kvms.com`
- 网页规则站不参与聚合搜索（单站搜才出结果），所以 4 条并存不会把搜索结果刷成 4 份
- 播放地址由页面内嵌的 wasm 模块计算，客户端需要支持 wasm 播放页解析
- 免费线路以 1080 为主；4K 线路多为会员，游客看不到

**`tvbox4k-fish.json`** — 原样归档的第三方合集：

- 111 个站全部是 `type: 3` 加密 spider（`csp_KaiFan` 等），依赖 jar + ARM native 库
- 鸿蒙端无法执行，导入后站点会被全部过滤，只有直播源部分可用
- 留着是给安卓盒子上的影视仓用，或单纯做为备份
