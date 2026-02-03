# 🔄 Safetensors 格式转换为 GGUF 格式并导入 Ollama

本文档介绍如何将 HuggingFace 格式的 safetensors 模型转换为 GGUF 格式，并导入到 Ollama 中使用。

## 📋 前置知识

- **Safetensors**: HuggingFace 推出的安全张量格式，用于存储模型权重
- **GGUF**: llama.cpp 使用的模型格式，支持量化压缩，适合本地部署
- **Ollama**: 本地大模型运行工具，支持 GGUF 格式模型

---

## 📥 1. 克隆 llama.cpp

```bash
git clone https://github.com/ggerganov/llama.cpp
cd llama.cpp
```

## 🔧 2. 构建虚拟环境

```bash
conda create -n llamacpp python=3.10
conda activate llamacpp
```

## 📦 3. 安装 llama.cpp 依赖环境

C++ 和 Python 环境二选一即可，建议两个都安装。

### 1) 编译 C++ 环境

量化需要使用 C++ 工具。

```bash
cd llama.cpp
mkdir build
cd build
cmake ..
make -j
```

### 2) 安装 Python 环境

模型转换需要使用 Python 脚本。

```bash
conda activate llamacpp
pip install -r requirements.txt
```

## 🔄 4. 模型转换

### Python 方式

从 safetensors 格式转换为 GGUF 格式（Q8_0 量化）：

```bash
cd llama.cpp
python convert_hf_to_gguf.py ../your_model_path \
    --outfile /your_output_path/model.gguf \
    --outtype q8_0
```

转换 safetensors 模型为 Ollama 格式（F16）：

```bash
python convert_hf_to_gguf.py ../qwen2-vl-2b --outtype f16
```

### C++ 方式

注意：此方式需要先编译 llama.cpp，然后在 `build/bin` 路径下操作。

<img width="1138" alt="量化工具" src="https://github.com/user-attachments/assets/0cfa43af-5f2d-4482-a6c1-594c285a003e" />

Q8_0 量化：

```bash
llama.cpp/build/bin/llama-quantize ../qwen2-vl-2b/qwen2-vl-2B-F16.gguf q8_0
```

Q4_0 量化：

```bash
llama.cpp/build/bin/llama-quantize ../qwen2-vl-2b/qwen2-vl-2B-F16.gguf q4_0
```

模型转换成功：

<img width="1082" alt="转换成功" src="https://github.com/user-attachments/assets/a3e24aa4-7d2f-4302-a1a7-fac4cf895c33" />

获得多个 GGUF 文件：

<img width="515" alt="GGUF文件" src="https://github.com/user-attachments/assets/4d134d3c-9b21-4a85-9764-262c5d183b57" />

---

## 📥 5. 模型导入 Ollama

### 创建 Modelfile

```bash
echo '/path/to/your_model.gguf' > Modelfile
```

### 创建（导入）模型

```bash
ollama create model_name -f /path/to/Modelfile
```

成功输出示例：

```text
(llamacpp) jetson@jetson-orin-nx-super:~/qwen2-vl-2b$ ollama create qwen2-vl-2b -f Modelfile
gathering model components
copying file sha256:1709aa285974b03259b129f2d5bd819beee9a44a0c3d79ca82291fe41838e3d7 100%
parsing GGUF
using existing layer sha256:1709aa285974b03259b129f2d5bd819beee9a44a0c3d79ca82291fe41838e3d7
writing manifest
success
```

### 查看已导入的模型

```bash
ollama list
```

输出示例：

```text
(llamacpp) jetson@jetson-orin-nx-super:~/qwen2-vl-2b$ ollama list
NAME                  ID              SIZE      MODIFIED
qwen2-vl-2b:latest    41a2703169aa    1.8 GB    20 seconds ago
```

## 🎯 运行模型

```bash
ollama run qwen2-vl-2b
```

---

## 📚 附录：量化类型说明

| 类型 | 说明 | 大小 | 精度 |
|------|------|------|------|
| F16 | 全精度 FP16 | 100% | 最高 |
| Q8_0 | 8-bit 量化 | ~50% | 高 |
| Q4_0 | 4-bit 量化 | ~25% | 中等 |
| Q4_K_M | 4-bit K-quantization | ~25% | 中等 |
