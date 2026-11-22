# fastls-fingerprints

[English documentation](https://fasttls.github.io/en/ecosystem/)

本仓库用于存放 FastTLS 指纹数据及其采集和验证记录，目前尚未发布数据包或 Go 模块。

## 普通用户如何使用

直接使用 [Fastls](https://fasttls.github.io/fastls/)、[Python](https://fasttls.github.io/python/) 或 [Node](https://fasttls.github.io/node/) 的内置配置入口。配置由 [imitate](https://github.com/FastTLS/imitate) 生成。可用配置通过所安装版本的 List/list_profiles()/listProfiles() 查询。

需要离线 Bundle 时，由固定版本 imitate 的导出工具生成，再按 [Fastls 离线注册指南](https://fasttls.github.io/fastls/profiles) 加载；当前没有可以直接 pip/npm/go install 的 fastls-fingerprints 数据包。

## 每日维护与已发布数据（2026-11-22）

`imitate v0.1.3` 包含 Chrome **158.0.8127.37**、Edge **158.0.4370.33** 和 Firefox **160.0.1** 的 Windows 配置，数据修订为 `browser-8ee4c22c6b779cbb`。使用规范 ID `chrome/158/windows`、`edge/158/windows`、`firefox/160/windows`；既有默认 selector 保持兼容，不保证默认别名选中这批实测版本。三个服务也支持显式的 `chrome158`、`edge158`、`firefox160` 名称。

[每日维护工作流](https://github.com/FastTLS/imitate/blob/v2/.github/workflows/browser-maintenance.yml)于北京时间 **10:17**（02:17 UTC）检查官方稳定版。每产品采集三个 TLS/H1/H2 场景、各五个独立冷进程；验证原始观察、完整 Spec 和六项在线/离线回放后，独立采用任务正常快进提交至默认分支。采集任务只读；采用任务具有受限的内容写权限。失败保留证据，不移动标签、不强制覆盖分支；可从已完成的可信运行恢复采用。版本与输入未变时复用已验证证据，仍导出快照。

验证范围仅为 Windows x64 冷导航：Chrome 为 en-US 有界面最小化；Edge 为 en-US 窗口移至屏幕外并使用软件图形模式；Firefox 为 zh-CN 无头。Chromium 扩展成员和参数的比较不证明随机顺序分布等价；恢复连接、ECH、其它系统、H3 和整个浏览器行为未获认证，ML-DSA 仍仅为声明能力。浏览器签名、完整版本及适用的官方摘要均在采集阶段核验；Chrome 本地 SHA256 不冒充厂商摘要。

**源库采用与用户升级是两步。** 每日任务不会自动发布新的 Go 模块、Python／npm 包或服务二进制，也不会在导入、创建会话或请求时下载更新。Python **0.7.3**、Node **0.16.3**、Fetch **v0.3.2**、RPC **v0.3.3**、MITM **v0.1.4** 和 fcurl **v0.2.2** 固定本批模块；旧安装须升级或使用已有 `ProfileStore` 显式导入、核对摘要、固定及回滚 Bundle。原始采集报告和离线快照见 [Actions 记录](https://github.com/FastTLS/imitate/actions/workflows/browser-maintenance.yml)；固定模块来源见 [v0.1.3](https://github.com/FastTLS/imitate/releases/tag/v0.1.3)。Bundle 对应固定版本，不代表未来数据自动更新。

```sh
go get github.com/FastTLS/fastls@v0.2.1
go get github.com/FastTLS/imitate@v0.1.3
go run github.com/FastTLS/imitate/cmd/imitate-export@v0.1.3 -output fingerprints.json
```

Go 导出的完整目录由 Go 的离线 Provider 加载；Python／Node 的 ProfileStore 使用 Actions 单产品候选中的 ProfileBundle v1，不直接导入完整目录快照。

Python／Node 的正式包自带原生库和固定数据，普通安装无需 Go。手动采集入口仍保留：[Firefox](https://github.com/FastTLS/imitate/blob/v2/tools/firefox/README.md)、[Chrome／Edge](https://github.com/FastTLS/imitate/blob/v2/tools/chromium/README.md)、[维护及恢复说明](https://github.com/FastTLS/imitate/blob/v2/tools/maintenance/README.md)。

## 数据发布要求与限制

未来每份产物须记录生成器/规范/数据修订、来源和授权、SHA-256、生成步骤与证据范围。浏览器规范 ID 为 product/version/platform[/variant]。库/客户端配置可为项目定义的参数基线，不得冒充第三方产品的真实采集。

配置可解析、一次请求成功、JA3 相同均不能证明完整浏览器一致性。未经核对的个人信息、Cookie、密钥、私有目标或原始抓包不得公开。历史本地导出和旧别名仅供迁移追溯，不是当前支持承诺。

## 协议与反馈

本仓库新增的 FastTLS 说明文档采用 [Apache-2.0](LICENSE)，见 [NOTICE](NOTICE)。未来导入的采集数据和第三方素材须逐项确认授权，不自动由本说明授予权利。[问题反馈](https://github.com/FastTLS/fastls-fingerprints/issues)。
## 使用边界与免责声明

仅在拥有权限的系统、数据和网络上使用，并遵守适用法律、服务条款及隐私要求。软件按许可证约定以“现状”提供，不承诺可用性、特定用途适用性、第三方服务放行、匿名性或与真实浏览器完全一致。浏览器名称和版本用于描述配置，不表示获得相应厂商认证或背书。部署方负责访问控制、密钥和个人信息保护、请求限额及数据备份；担保排除与责任限制以随附许可证及适用法律为准。本说明不改变许可证授予的权利或新增许可限制。
