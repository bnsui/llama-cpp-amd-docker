# llama.cpp AMD Docker Images (Auto-built)

这是一个全自动构建的项目，旨在为 [llama.cpp](https://github.com/ggml-org/llama.cpp) 提供专用于 AMD 平台（ROCm 和 Vulkan）的 最新版 Docker 镜像。

## 💡 特性
* **极致轻量且快速**：基于官方最新 Release 预编译的二进制文件直接打包，比官方docker镜像更新快。
* **双版本支持**：提供基于 `ROCm` 和 `Vulkan` 的两个独立镜像，可以直接用作Backend，比如：gpustack等。
* **自动同步更新**：每小时自动检测官方发布，第一时间同步构建并推送到 GitHub Container Registry (GHCR) 和 Docker Hub。
[English](#english) | [中文](#简体中文)

---

<h2 id="english">English</h2>

This is an automated build project providing Docker images tailored for AMD platforms (**ROCm** and **Vulkan**) for [llama.cpp](https://github.com/ggml-org/llama.cpp).

### 💡 Features
* **Extremely Lightweight**: Built directly from the official pre-compiled release binaries. No bloated compilation environments. Pure Ubuntu base.
* **Dual Versions**: Provides independent images for `ROCm` and `Vulkan`.
* **Auto-Sync**: Checks for official releases hourly and automatically builds and pushes to both **Docker Hub** and **GitHub Container Registry (GHCR)**.

## 🚀 使用方法
镜像默认的 ENTRYPOINT 是 `llama-server`。你可以通过挂载本地模型文件并在命令后追加参数来运行。如果使用的是gpustack，只要在后台的llama.cpp中增加后端(分rocm和vulkan)版本，拉取选择latest版本即可。
### 🐳 Getting the Images
You can pull the images from either Docker Hub or GHCR. The tags directly correspond to the official llama.cpp release tags (e.g., `b8683`).

**From Docker Hub:**
* ROCm: `docker pull maharajah/llama-cpp:rocm-latest`
* Vulkan: `docker pull maharajah/llama-cpp:vulkan-latest`

**From GitHub Container Registry (GHCR):**
* ROCm: `docker pull ghcr.io/bnsui/llama-cpp-amd-docker:rocm-latest`
* Vulkan: `docker pull ghcr.io/bnsui/llama-cpp-amd-docker:vulkan-latest`

### 🚀 Usage

The default `ENTRYPOINT` is `llama-server`. You can run it by mounting your local model directory and appending arguments.

**Example: Running Vulkan Version**
```bash
# 纯docker运行 Vulkan 版本示例
docker run --rm -it \
  --device /dev/dri \
  -v /path/to/your/models:/models \
  -p 8080:8080 \
  maharajah/llama-cpp:vulkan-latest \
  -m /models/your-model.gguf --host 0.0.0.0
```

**Example: Running ROCm Version**
*Note: ROCm requires both `/dev/kfd` and `/dev/dri`.*
```bash
docker run --rm -it \
  --device /dev/kfd \
  --device /dev/dri \
  -v /path/to/your/models:/models \
  -p 8080:8080 \
  maharajah/llama-cpp:rocm-latest \
  -m /models/your-model.gguf --host 0.0.0.0
```

---

<h2 id="简体中文">简体中文</h2>

这是一个全自动构建的项目，旨在为 [llama.cpp](https://github.com/ggml-org/llama.cpp) 提供专用于 AMD 平台（**ROCm** 和 **Vulkan**）的 Docker 镜像。

### 💡 特性
* **极致轻量且干净**：基于纯净版 Ubuntu 底座，直接提取官方最新 Release 预编译二进制文件进行打包。不包含冗长的编译环境。
* **双版本支持**：提供基于 `ROCm` 和 `Vulkan` 的两个独立镜像。
* **自动同步更新**：每小时自动检测官方发布，第一时间同步构建并双重推送到 **Docker Hub** 和 **GitHub Packages (GHCR)**。

### 🐳 获取镜像

您可以从 Docker Hub 或 GHCR 拉取镜像。镜像标签（Tag）与官方 llama.cpp 的发布版本号完美对应（例如 `b8683`）。

**从 Docker Hub 拉取:**
* ROCm 版本: `docker pull maharajah/llama-cpp:rocm-latest`
* Vulkan 版本: `docker pull maharajah/llama-cpp:vulkan-latest`

**从 GitHub Container Registry (GHCR) 拉取:**
* ROCm 版本: `docker pull ghcr.io/bnsui/llama-cpp-amd-docker:rocm-latest`
* Vulkan 版本: `docker pull ghcr.io/bnsui/llama-cpp-amd-docker:vulkan-latest`

### 🚀 使用方法

镜像默认的入口点（ENTRYPOINT）是 `llama-server`。您可以通过挂载本地模型文件夹，并在命令末尾追加参数来运行服务。

**运行 Vulkan 版本示例:**
```bash
docker run --rm -it \
  --device /dev/dri \
  -v /path/to/your/models:/models \
  -p 8080:8080 \
  maharajah/llama-cpp:vulkan-latest \
  -m /models/your-model.gguf --host 0.0.0.0
```

**运行 ROCm 版本示例:**
*注意：ROCm 环境需要同时挂载 `/dev/kfd` 和 `/dev/dri` 设备。*
```bash
docker run --rm -it \
  --device /dev/kfd \
  --device /dev/dri \
  -v /path/to/your/models:/models \
  -p 8080:8080 \
  maharajah/llama-cpp:rocm-latest \
  -m /models/your-model.gguf --host 0.0.0.0
```
