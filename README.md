# Jotvera models / 笺序本机 AI 模型

这是 Jotvera（笺序）的公开模型分发仓库。我们将上游已开放的模型文件整理为可校验的 `.jotvera-model` 安装包，保留原始许可证、来源和兼容性信息。这里没有声称重新训练这些模型。

## 在应用内安装

在包含此模型目录的新版本客户端中，打开 **设置 → 本机 AI → 预览模型 → 下载并使用**。

应用会下载对应系统的模型包，检查完整包哈希、发布签名和每个文件的哈希，完成本机文字与图片自检后再启用。网络中断可以稍后继续；自检失败会保留现有模型选择，并给出可重试的原因。离线导入仍可用于手动安装同一个完整包。

首个公开预览 Release 已发布：[`preview-2026.11.18`](https://github.com/makersns/jotvera-models/releases/tag/preview-2026.11.18)。MiniCPM 包已上传；Android 包正在上传到同一版本。模型二进制文件存放在 Release 附件中，不存放在 Git 历史中。

## 平台与验证范围

| 平台 | 模型与引擎 | 当前证据 |
| --- | --- | --- |
| macOS Apple Silicon / ARM64 | MiniCPM-V 4.7 1B，GGUF / llama.cpp | 同一组文件和 CPU 配置已进行真实文字、图片与退出测试；每次安装仍需本机自检。 |
| Windows x64 | 同一 MiniCPM GGUF 包，Windows 原生 llama.cpp 引擎 | 包格式、签名和目标匹配已校验；尚未完成 Windows 设备上的模型推理验证。 |
| Android ARM64 | 独立的 Qwen3-VL 2B / MNN 包 | 平台专用包已签名并通过格式校验，正在上传；不能使用上面的 GGUF 包替代。尚未完成 Android 设备推理验证。 |

客户端必须内置与包清单完全匹配的引擎构建。目标系统或引擎不匹配时，应用不会把包显示为可安装。Windows ARM64、macOS Intel 及其他目标不在本次包的声明范围内。

## MiniCPM 预览包

- 名称：MiniCPM-V 4.7 1B · 文字与图片预览版
- 版本：`2026.11.18-preview.1`
- 文件：`minicpm-v4.7-1b-gguf-cpu-preview-2026.11.18-preview.1.jotvera-model`
- 下载大小：1,782,187,572 字节；展开文件总大小：1,782,183,128 字节。安装过程中还需要临时下载、校验和安装空间；以客户端实时检查为准。
- 包文件 SHA-256：`9a9082d62d7448f059daf1c06fb37e10076793af2f721486037f792f013d109f`
- 签名清单摘要：`1924f476bdf3d78c9819daa38a7fe575b10235c6e2d8823ec945bbd962cdb895`
- CPU 配置：4 线程、4 GiB 模型内存预算、32,768 token 上下文、最多 8,192 token 输出。
- 引擎：`llama-52975342ff6b85127ff31930d39e36725fd08809-jotvera-ipc1`

上述 token 数是配置上限，不保证每次回答长度。已记录的最长输出为 3,892 token，模型自行结束；尚未实际覆盖完整 32,768 token 输入边界或 8,192 token 输出边界。

### 已知限制

这个版本属于**公开预览**，不是正式质量认证版本。测试观察到事实错误、长文偏短或重复、未严格遵守选区范围等问题。文字与图片自检仅证明本机能够加载并运行，不能证明所有回答准确，也不能代替具体任务的质量检查。

完整清单、公钥与固定摘要见 [models/minicpm-v4.7-1b](models/minicpm-v4.7-1b)。脱敏后的实际验证范围见 [validation](validation)。

## Android 专用 Qwen3-VL 2B 预览包

- 目标：Android ARM64，MNN CPU 引擎。
- 文件：`qwen3-vl-2b-mnn-android-preview-2026.11.18-preview.1.jotvera-model`
- 下载大小：1,475,269,427 字节；展开文件总大小：1,475,264,448 字节。
- 包 SHA-256：`740261509248c5718c1cbbf4978077740cb8dce7ec6f4ac6140d97a09edd2563`
- 签名清单摘要：`1d4ec2131e2249d8c7468ad4dc8adf820d6d3e0d6aea4682bde5b009d478613a`
- CPU 配置：4 线程、4 GiB 模型预算、4,096 token 上下文、最多 1,024 token 输出。手机配置与桌面包分别管理。
- 来源：[taobao-mnn 官方 Qwen3-VL 2B MNN 固定版本](https://huggingface.co/taobao-mnn/Qwen3-VL-2B-Instruct-MNN/tree/9e49ec71ded22500a997ed0f9961e1e92b85bbc9)。

15 个包内文件均已校验；官方转换模型字节保持不变。新增的 processor/template metadata 仅记录来源，不覆盖 MNN 实际读取的原始配置。上游转换模型卡没有提供精确转换器版本或转换所用原始 checkpoint，本仓库保留该溯源缺口，不宣称可完全复现转换。

签包时尚未完成 Android 设备或模拟器推理，因此该包明确标记为 `device-check-required` / `untested`。设备收到包后必须通过文字和图片自检。详见 [Android 包清单](models/qwen3-vl-2b-android) 与[验证范围](validation/android-qwen3-vl-source-preparation-20261118.json)。

## 来源与许可证

模型权重未被修改；Jotvera 增加了安装包封装、签名、完整性清单、平台配置与验证说明。

- [OpenBMB 官方 MiniCPM-V 4.7 1B GGUF](https://huggingface.co/openbmb/MiniCPM-V-4.7-1B-gguf/tree/e81247fa2eac0d99e43aeac55da199221959af15)
- [OpenBMB 固定版本 Apache-2.0 许可证](https://github.com/OpenBMB/MiniCPM-V/blob/4dbbb6c58b6f8a004d6689028417296719f0831a/LICENSE)
- [big_vision 固定版本 Apache-2.0 许可证](https://github.com/google-research/big_vision/blob/0127fb6b337ee2a27bf4e54dea79cff176527356/LICENSE)
- [Qwen3-VL 固定版本 Apache-2.0 许可证](https://github.com/QwenLM/Qwen3-VL/blob/96588727e44c78b25ba03ea03b8e12f7e64fd0da/LICENSE)
- [MNN 固定版本 Apache-2.0 许可证](https://github.com/alibaba/MNN/blob/40ad7e340cdf5cb29fe9d5f1f9eec794adbaef6d/LICENSE)

请保留包内及 [licenses](licenses) 中的原始许可证和 [NOTICE.md](NOTICE.md)。不同组件遵循各自附带的许可证；此仓库没有改变上游的授权条件。

## Verification

This repository distributes signed preview model data for Jotvera. The upstream weights are unchanged. A preview signature authorizes only the exact manifest digest listed beside its public key; it does not grant production certification. The client checks the full container hash, Ed25519 signature, per-file hashes, platform and engine build, then performs local text and image self-tests before activation.

The macOS CPU profile has real-device evidence. Windows package-format verification is **not** Windows inference evidence. Android requires its own MNN package and device verification. See the machine-readable package metadata and validation notes for the precise limits of each result.
