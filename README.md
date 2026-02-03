# 🤖 本地大模型部署指南

<div align="center">

<img src="images/ollama.png" width="120" alt="LLM Logo">

**一站式本地大模型部署教程**

> 基于 Ollama 在 Jetson 设备上轻松部署 DeepSeek、Qwen 等大语言模型，享受完全本地化、隐私安全的 AI 体验

[![文档状态](https://img.shields.io/badge/docs-v1.0-blue)](./docs/deepseek-setup.md)
[![License](https://img.shields.io/badge/license-MIT-green)]()

[快速开始](#-快速开始) • [特性](#-特性) • [文档](#-文档) • [FAQ](#-常见问题)

</div>

---

## 📖 项目简介

本项目提供了在本地 Jetson 设备上部署大语言模型的完整教程，涵盖从基础概念到实战部署的全流程。通过本教程，你可以：

- 🚀 快速搭建本地 DeepSeek 大模型
- 🐋 使用 Ollama 管理多个大模型
- 🔄 将 Safetensors 格式转换为 GGUF 格式并导入 Ollama
- 🌐 通过 Open WebUI 实现友好的 Web 交互界面
- 🐳 使用 Docker 简化部署流程

## ✨ 特性

- ✅ **零基础友好** - 详细的概念解释和步骤说明
- ✅ **多平台支持** - 支持 macOS、Windows 和 Linux
- ✅ **格式转换** - 支持 Safetensors 转 GGUF 格式
- ✅ **完全本地化** - 无需联网，保护隐私
- ✅ **开源免费** - 所有工具均为开源项目
- ✅ **可扩展性** - 支持多种大模型切换使用

## 🎯 支持的模型

| 模型 | 提供方 | 说明 |
|------|--------|------|
| DeepSeek-R1 | DeepSeek | 最新深度学习模型，超越 ChatGPT-4o |
| Qwen2/Qwen2.5 | 阿里云 | 多模态语言模型，支持文本和图像处理 |
| LLaMA3 | Meta AI | 大型语言模型，高效自然语言处理 |
| Phi-3 | 微软 | 小型语言模型，低资源消耗 |
| LLaVA-Phi3 | 微软+社区 | 多模态模型，支持图像识别 |

## 🚀 快速开始

### 环境要求

- **操作系统**: macOS / Windows / Linux
- **内存**: 建议 8GB 及以上
- **磁盘空间**: 至少 10GB 可用空间

### 三步快速部署

1. **安装 Ollama**
   ```bash
   curl -fsSL https://ollama.com/install.sh | sh
   ```

2. **拉取 DeepSeek 模型**
   ```bash
   ollama pull deepseek-r1:1.5b
   ```

3. **运行模型**
   ```bash
   ollama run deepseek-r1:1.5b
   ```

## 📚 文档

- 📖 [完整教程](./docs/deepseek-setup.md) - 从零开始的详细部署指南
- 🔄 [格式转换](./docs/model-format-conversion.md) - Safetensors 转 GGUF 格式
- 🐳 [Docker 部署](./docs/deepseek-setup.md#搭建web服务) - 使用 Docker 部署 Web 界面
- 📋 [模型列表](./docs/deepseek-setup.md#附录推荐模型) - 推荐使用的模型列表

## 🔧 常用工具

| 工具 | 用途 |
|------|------|
| [Ollama](https://ollama.com/) | 本地大模型运行容器 |
| [Open WebUI](https://github.com/open-webui/open-webui) | Web 交互界面 |
| [Docker](https://www.docker.com/) | 容器化部署平台 |
| [Portainer](https://www.portainer.io/) | Docker 容器管理工具 |

## 📝 更新日志

- **2025-02-05**: 更新 Ollama 文档，修正本地运行地址
- **2025-02-03**: 移除 DeepSeek 对 Ubuntu 22 版本系统的安装建议
- **2025-02-02**: 更新 Ollama 部署方式

## ❓ 常见问题

**Q: 需要什么硬件配置？**

A: 建议至少 8GB 内存，更大的参数集模型需要更多内存和 GPU 支持。

**Q: 可以离线使用吗？**

A: 可以，模型下载后完全在本地运行，无需联网。

**Q: 支持哪些操作系统？**

A: 支持 macOS、Windows 和 Linux 主流发行版。

---

<div align="center">

**Enjoy building your local LLM! 🚀**

[⬆ 返回顶部](#-本地大模型部署指南)

</div>
