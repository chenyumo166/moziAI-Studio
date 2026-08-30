---
language:
  - zh
license: other
tags:
  - moziAI
  - llama.cpp
  - GGUF
  - local-deployment
  - webui
task_categories:
  - text-generation
  - image-text-to-text
base_model:
  - moziAI/moziAI-35B
  - moziAI/moziAI-27B
pipeline_tag: text-generation
---

# moziAI-Studio 🚀

> **一键部署本地大模型的管理软件** —— 让 moziAI-35B / moziAI-27B 在 Windows / macOS / Linux 上**解压即用**。

`moziAI-Studio` 是一款「解压免安装」的本地 AI 模型管理软件：WebUI + FastAPI + llama.cpp 一体化，把复杂的模型部署变成**可视化一键操作**。无需命令行、无需手动配置环境，双击即可自动完成硬件检测、参数优化、模型下载、llama.cpp 部署与推理服务启动。

- 🌟 **傻瓜化一键部署**：零命令行操作，解压即用
- 🧠 **硬件自动适配**：自动识别显卡厂商与显存，匹配最优推理后端与参数
- 🔒 **模态锁定**：下载/部署/升级期间锁定页面，防止设置错乱
- 💾 **参数配置持久化**：页面改参数 → 自动同步 llama.cpp 启动配置 → 下次启动即生效
- 🖥️ **三平台统一体验**：Windows / macOS / Linux

---

## ✨ 核心功能

| 功能 | 说明 |
|------|------|
| **解压免安装** | 下载 zip 解压即用，自动打开浏览器 |
| **一键部署** | 6 步向导：部署路径 → 选择模型 → 推理框架 → 参数配置 → 服务管理 → 自动部署 |
| **硬件自动检测** | 自动识别显卡（型号/厂商/显存）、磁盘空间、端口占用 |
| **推理后端自动适配** | AMD→Vulkan / NVIDIA→CUDA / Intel→Vulkan / Linux AMD→HIP·ROCm / macOS→Metal |
| **单/双模型启动模式** | 按显存自动推荐，防爆显存死机 |
| **参数保存 → 启动生效** | 上下文/温度/视觉/GPU 等参数自动写入 llama.cpp 启动配置 |
| **模型下载管理** | GGUF 断点续传、暂停/取消、进度实时刷新 |
| **服务管理** | 一键启停推理服务，开机自启动 |
| **版本检查与升级** | 多源检查（GitHub → 魔搭 → HF 自动降级），软件内一键升级 |
| **外部调用** | OpenAI 兼容 API，Python 示例 + 防火墙引导 |

---

## 💻 系统要求

| 部署方式 | 显存要求 |
|---------|---------|
| moziAI-27B（单模型） | ≥ 16 GB |
| moziAI-35B（单模型） | ≥ 20 GB |
| 双模型同时启动 | ≥ 36 GB（推荐 42 GB+） |

| 平台 | 架构 | 显卡后端 |
|------|------|---------|
| Windows 10/11 | x64 | NVIDIA CUDA / AMD Vulkan / Intel Vulkan |
| macOS 11+ | Apple Silicon / Intel | Metal |
| Linux | x64 | NVIDIA CUDA / AMD HIP·ROCm / Intel Vulkan |

> 无独立显卡（核显/纯 CPU）也可运行，性能取决于 CPU 与内存。显存不足会自动提示并阻止启动，避免爆显存死机。

---

## 🚀 快速开始

> ⚠️ **核心提示**：MoziAI 的最佳推理能力需要**同时下载 3 个文件**——主模型、视觉投影、聊天模板。缺失任何一个都会损失对应能力（缺主模型无法推理、缺视觉投影丧失图像理解、缺聊天模板则失去 MoziAI 身份与思考链）。

### 📦 模型三件套（3 个文件 = 100% 激活最佳推理能力）

| 文件 | 必要性 | 作用 |
|------|--------|------|
| 主模型 `.gguf` | **必选** | 模型权重，核心推理能力 |
| 视觉投影 `mmproj.gguf` | **必选** | 多模态视觉理解，不载入则丧失图像能力 |
| 聊天模板 `chat-template.json` | **必选** | 注入 MoziAI 身份 + 七维思考 + LOOP 机制指令 |

> 📌 三件套可在软件内「模型配置 → 选择模型 → 下载模型」中**一次勾选整体下载**，自动放入对应模型目录；下载支持断点续传、暂停/取消。聊天模板为 Jinja 格式（`chat-template.json`）。

### 🪟 Windows（一键启动）

1. 下载 `moziAI-Studio-V1.0-win-x64.zip` 并解压
2. **双击 `moziAI-Studio.exe` 启动本软件**（软件本体，自动打开浏览器）
3. 浏览器自动打开 `http://127.0.0.1:19090`，按向导完成部署



> 💡 **exe 与启动器关系**：`moziAI-Studio.exe` 就是软件本体（内置完整后端+前端），**Windows 标准启动方式为直接双击 exe**——无黑窗、自动打开浏览器 WebUI，并**自动在桌面创建「moziAI-Studio」快捷方式**（仅首次创建一次）；`.vbs`（无黑窗）/`.bat`（带日志窗口）为兼容旧版的可选启动器，最终启动的仍是 exe。

### 🍎 macOS / 🐧 Linux

1. 下载对应平台安装包（由 GitHub Actions CI 三平台矩阵构建）
2. 执行启动脚本：`start-moziAI-Studio.command`（macOS）/ `start-moziAI-Studio.sh`（Linux）
3. 浏览器打开 `http://127.0.0.1:19090`
4. macOS 若被 Gatekeeper 拦截：右键 → 打开

### 💻 源码运行

```bash
cd bin/backend
pip install -r requirements.txt
python run_app.py    # 自动打开浏览器
```

---

## 🔌 外部调用（OpenAI 兼容 API）

| 模型 | API 地址 | 默认端口 |
|------|---------|---------|
| moziAI-35B | `http://127.0.0.1:19091/v1/chat/completions` | 19091 |
| moziAI-27B | `http://127.0.0.1:19092/v1/chat/completions` | 19092 |

```python
import requests

resp = requests.post(
    "http://127.0.0.1:19091/v1/chat/completions",
    json={
        "model": "moziAI-35B",
        "messages": [{"role": "user", "content": "你好！"}],
        "max_tokens": 512,
    },
)
print(resp.json()["choices"][0]["message"]["content"])
```

> 管理端 WebUI 服务端口 19090（`/api` 共 25 个管理接口），与模型推理端口相互独立。

---

## 🧩 配套模型

| 模型 | 量化 | 文件 | 视觉 |
|------|------|------|------|
| moziAI-35B | Q4_K_M | `moziAI-35B-Q4_K_M.gguf`（15.5 GB） | ✅ `mmproj.gguf` |
| moziAI-27B | Q4_K_M | `moziAI-27B-Q4_K_M.gguf` | ✅ `mmproj.gguf` |

每模型含**三件套**：GGUF 权重 + 视觉投影 `mmproj.gguf` + 对话模板 `chat-template.json`，模型下载支持断点续传。

---

## 🏗️ 技术架构

```
浏览器 WebUI（Vue3 + Vite） ──HTTP(19090)──► FastAPI 后端（25 管理 API）
                                              │ 生成启动参数
                                              ▼
                            llama.cpp 推理服务（llama-server）
                            Vulkan / CUDA / HIP / Metal 自动适配
                            35B → 19091   27B → 19092
```

- **前端**：Vue 3 + Vite + Vue Router + Pinia + Element Plus
- **后端**：FastAPI + Uvicorn + PyYAML + psutil + huggingface_hub
- **推理**：llama.cpp（llama-server）
- **打包**：PyInstaller 单文件；CI 三平台矩阵自动构建

---

## 📄 许可证

本模型采用**自定义限制性许可证**：

✅ **允许** — 免费商业使用、复制和分发
❌ **禁止** — 二次开发、转售售卖、再许可
📋 **要求** — 保留原始版权声明，注明来源：moziAI-27B

本模型按「原样」提供，不提供任何形式的保证。模型输出仅供参考，不构成投资建议。使用者需自行承担使用风险。

详细条款请参阅 [LICENSE](LICENSE) 文件。

## 🌐 官方信息

| 平台 | 地址 |
|------|------|
| GitHub |https://github.com/chenyumo166/moziAI-Studio/ |


---

**moziAI-Studio V1.0** · 一键部署moziAI-35B/27B本地大模型，让 AI 触手可及 🚀
