## 目录

- [目录](#目录)
- [获取 Cookie 的方法](#获取-cookie-的方法)
  - [Firefox](#firefox)
  - [Chrome/Chromium](#chromechromium)
- [获取腾讯云函数（SCF）授权（ID/KEY）的方法](#获取腾讯云函数scf授权idkey的方法)
- [配置相关](#配置相关)
  - [配置文件路径](#配置文件路径)
  - [在线填写表单获取配置](#在线填写表单获取配置)
  - [单用户配置参考](#单用户配置参考)
  - [多用户配置参考](#多用户配置参考)

## 获取 Cookie 的方法

以 PC 端浏览器举例（推荐使用 Firefox/Chrome/Chromium Edge）

最终 Cookie 是这样的（为了演示方便换了行，实际只有一行）

```text
_uuid=D2282D0F-257B-845A-BDF5-C770ED288F4001440infoc; buvid3=BF17608E-FB87-4F49-A922-56FD2E284D6F18534infoc;
fingerprint=5502cd4fe9637738de04bd9c3d1bdbc5;
buvid_fp=BF17608E-FB87-4F49-A922-56FD2E284D6F18534infoc;
SESSDATA=21607773%2C1631089673%2C71a42%2A31; bili_jct=dd92c55a6d67041ce2f3fb1650889ea8;
DedeUserID=521268093; DedeUserID__ckMd5=47d541f04b605da9;
sid=ivie73r8; fingerprint3=792b32adfecbe31a4aca53ab7be1ad76;
fingerprint_s=bb6736758e7344a295c2ed6070cc642e;
buvid_fp_plain=BF17608E-FB87-4F49-A922-56FD2E284D6F18534infoc;
CURRENT_FNVAL=80; blackside_state=1; rpdid=|(kmJYYJ)lkR0J'uYu)llkJYJ; _dfcaptcha=a46d7562a42065d43a88c053e283e876;
LIVE_BUVID=AUTO8016188357987702; bsource=search_baidu; PVID=2
```

### Firefox

任意方式进入 b 站（搜索，收藏夹，地址访问等）
按 F12 （或者右键 --> 检查）打开开发者工具，切换到`网络` ( `network` )  
点击重新载入（或者按 F5，Ctrl + R 等）刷新页面

![firefox-network](./images/firefox-network.png)

点击某一个请求（通常为 `nav` ）

![firefox-net-bnav](./images/firefox-net-bnav.png)

### Chrome/Chromium

任意方式进入 b 站（搜索，收藏夹，地址访问等）  
按 F12 （或者右键 --> 检查）打开开发者工具，切换到 `网络` ( `network` )  
点击重新载入（或者按 F5，Ctrl + R 等）刷新页面  
点击某一个请求（通常为 nav ）

![chrome-net-bnav](./images/chrome-net-bnav.png)

## 获取腾讯云函数（SCF）授权（ID/KEY）的方法

获取 key 参考[腾讯云权限管理](https://console.cloud.tencent.com/cam/capi)

![image-20210725112752944](images/get-scf-id.png)

## 配置相关

### 配置文件路径

- 全局配置（可配置多个用户）：`config/config.json`
- 单用户配置：`与 index.js (ts) 同目录/config/config.json`。如 `dist`

所有配置都登记在 [`interface/Config.ts`](/src/interface/Config.ts) 文件中  
**解释：**

- `number`: 数字 例如：123。
- `string`: 字符串 例如：ojbk。
- `boolean`: 布尔值 `true` 或者 `false`。
- `[]`: 数组 例如：`number[]` 具体可以是 `[1,2,3]`。
- `[number, number]`: 长度为 2 且必须为数字的数组，例如：`[6, 15]`
- `targetLevel?: number;` `?` 表示 `targetLevel` 是可选的配置。

### 在线填写表单获取配置

**可能新增更新不及时**

<https://catlair.gitee.io/bili-tools-docs-deploy/>

![docs-add-config](images/docs-add-config.png)

![docs-get-config](images/docs-get-config.png)

### 单用户配置参考

```json
{
  "function": {
    "silver2Coin": false,
    "liveSignTask": false,
    "addCoins": false,
    "mangaSign": false,
    "shareAndWatch": false,
    "supGroupSign": false,
    "judgement": true,
    "liveSendMessage": false,
    "charging": false,
    "getVipPrivilege": false
  },
  "dailyRunTime": "19:19:19-23:23:23",
  "apiDelay": [20, 50],
  "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.141 Safari/537.36",
  "cookie": "哔站完整cookie，至少含有三要素",
  "message": {
    "email": {
      "from": "发件邮箱",
      "to": "收件邮箱",
      "pass": "发件邮箱授权码",
      "host": "例如smtp.163.com",
      "port": 465
    }
  },
  "stayCoins": 0,
  "targetCoins": 5,
  "targetLevel": 6,
  "coinRetryNum": 6,
  "upperAccMatch": true,
  "customizeUp": [],
  "chargeUpId": 0,
  "chargePresetTime": 31,
  "sls": {
    "name": "bilitool_scf_demo",
    "region": "ap-chengdu",
    "description": "干什么的"
  }
}
```

注：

- `sls` 字段是实现随机运行需要的内容（函数名和函数地域）
- `json` 不支持注释，所以千万不要注释

### 多用户配置参考

```json
{
  "message": {}, // 可以省略
  "account": [{}, {}, {}] // {} 就是上面的单用户配置
}
```
