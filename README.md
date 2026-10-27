# fastls-fingerprints

[English documentation](https://fasttls.github.io/en/ecosystem/)

本仓库用于存放 FastTLS 指纹数据及其采集和验证记录，目前尚未发布数据包或 Go 模块。

## 普通用户如何使用

直接使用 [Fastls](https://fasttls.github.io/fastls/)、[Python](https://fasttls.github.io/python/) 或 [Node](https://fasttls.github.io/node/) 的内置配置入口。配置由 [imitate](https://github.com/FastTLS/imitate) 生成。可用配置通过所安装版本的 List/list_profiles()/listProfiles() 查询。

需要离线 Bundle 时，由固定版本 imitate 的导出工具生成，再按 [Fastls 离线注册指南](https://fasttls.github.io/fastls/profiles) 加载；当前没有可以直接 pip/npm/go install 的 fastls-fingerprints 数据包。

## 数据发布要求与限制

未来每份产物须记录生成器/规范/数据修订、来源和授权、SHA-256、生成步骤与证据范围。浏览器规范 ID 为 product/version/platform[/variant]。库/客户端配置可为项目定义的参数基线，不得冒充第三方产品的真实采集。

配置可解析、一次请求成功、JA3 相同均不能证明完整浏览器一致性。未经核对的个人信息、Cookie、密钥、私有目标或原始抓包不得公开。历史本地导出和旧别名仅供迁移追溯，不是当前支持承诺。

## 协议与反馈

本仓库新增的 FastTLS 说明文档采用 [Apache-2.0](LICENSE)，见 [NOTICE](NOTICE)。未来导入的采集数据和第三方素材须逐项确认授权，不自动由本说明授予权利。[问题反馈](https://github.com/FastTLS/fastls-fingerprints/issues)。
## 使用边界与免责声明

仅在拥有权限的系统、数据和网络上使用，并遵守适用法律、服务条款及隐私要求。软件按许可证约定以“现状”提供，不承诺可用性、特定用途适用性、第三方服务放行、匿名性或与真实浏览器完全一致。浏览器名称和版本用于描述配置，不表示获得相应厂商认证或背书。部署方负责访问控制、密钥和个人信息保护、请求限额及数据备份；担保排除与责任限制以随附许可证及适用法律为准。本说明不改变许可证授予的权利或新增许可限制。
