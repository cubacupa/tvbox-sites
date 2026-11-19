# TVBox 点播源配置

个人用的点播源分发仓，供「影视盒」（鸿蒙智慧屏）导入。

## 文件

| 文件 | 内容 | 用在哪 |
|---|---|---|
| `4kvm-rule.json` | 4K影视 单条规则（主站 4kvm.tv） | 设置 → Kazumi 规则站（**推荐**） |
| `4kvm-rule-me.json` / `-net` / `-s` | 同上，备用域名 .me / .net / 4kvms.com | 同上，主站打不开时换一条 |
| `4kvm-sites.json` | 4 个域名打包成一份配置 | 点播源地址（会替换整个站点列表） |
| `tvbox4k-fish.json` | 第三方 4K 合集，111 个 spider 站 | 仅安卓影视仓 |

## 方式一：Kazumi 规则站（推荐）

设置页 →「Kazumi 规则站」输入框 → 粘贴下面这条地址 → 回车。

```
https://raw.githubusercontent.com/cubacupa/tvbox-sites/main/4kvm-rule.json
```

这条路径是**增量添加**：站点进「我的站点」，暴风、醉影等现有站点不受影响，随时可删。App 也会自动在 raw 与 jsDelivr 之间来回试，raw 不通会自己换。

站点按 api 去重，所以重复粘贴不会加出多个。主站域名失效时，换下面三条之一：

```
https://raw.githubusercontent.com/cubacupa/tvbox-sites/main/4kvm-rule-me.json
https://raw.githubusercontent.com/cubacupa/tvbox-sites/main/4kvm-rule-net.json
https://raw.githubusercontent.com/cubacupa/tvbox-sites/main/4kvm-rule-s.json
```

## 方式二：点播源地址

设置页 →「点播源」输入框 → 粘贴 → 载入。

```
https://cdn.jsdelivr.net/gh/cubacupa/tvbox-sites@main/4kvm-sites.json
```

一次拿到 4 个域名，但**会替换当前站点列表**（暴风、醉影会从列表里消失，切回内置 Default 才回来）。只有想整体换一套源时才用这条。

## 地址选择的注意点

- `raw.githubusercontent.com` 在国内常被阻断，电视上更明显；`cdn.jsdelivr.net` 一般更稳，但要等它的缓存刷新（提交后几分钟到几十分钟）
- `github.com/.../blob/...` 那种**网页地址**不能用，拿到的是 HTML，会报「解析出 0 个站点」
- 仓库必须是 public。私有仓的 raw 要带 token，App 拉不到

## 说明

**`4kvm-*`** — 同一套网页规则，换域名而已：

- 主站 `www.4kvm.tv`，备用 `www.4kvm.me`、`www.4kvm.net`、`www.4kvms.com`
- 网页规则站不参与聚合搜索（单站搜才出结果），所以多条并存不会把搜索结果刷成多份
- 播放地址由页面内嵌的 wasm 模块计算，客户端需要支持 wasm 播放页解析
- 免费线路以 1080 为主，4K 线路多为会员

**`tvbox4k-fish.json`** — 原样归档的第三方合集：

- 111 个站全部是 `type: 3` 加密 spider（`csp_KaiFan` 等），依赖 jar + ARM native 库
- 鸿蒙端无法执行，导入后站点会被全部过滤，只有直播源部分可用
- 留着是给安卓盒子上的影视仓用，或单纯做为备份

## 关于 4K

这类网页站的免费线路以 1080 为主。真要 4K，目前稳定能播的是内置醉影的「4K电影」分类（212 部，抽检约一半是真 3840×2160）。
