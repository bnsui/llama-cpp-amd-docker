# llama.cpp AMD Docker Images (Auto-built)

这是一个全自动构建的项目，旨在为 [llama.cpp](https://github.com/ggml-org/llama.cpp) 提供专用于 AMD 平台（ROCm 和 Vulkan）的 Docker 镜像。

## 💡 特性
* **极致轻量且快速**：基于官方最新 Release 预编译的二进制文件直接打包，不包含冗长的编译过程。
* **双版本支持**：提供基于 `ROCm` 和 `Vulkan` 的两个独立镜像。
* **自动同步更新**：每小时自动检测官方发布，第一时间同步构建并推送到 GitHub Container Registry (GHCR) 和 Docker Hub。

## 🐳 获取镜像

**Docker Hub:**
* ROCm 版本: `docker pull maharajah/llama-cpp:rocm-latest`
* Vulkan 版本: `docker pull maharajah/llama-cpp:vulkan-latest`

**GitHub Container Registry (GHCR):**
* ROCm 版本: `docker pull ghcr.io/bnsui/llama-cpp-amd-docker:rocm-latest`
* Vulkan 版本: `docker pull ghcr.io/bnsui/llama-cpp-amd-docker:vulkan-latest`

## 🚀 使用方法
镜像默认的 ENTRYPOINT 是 `llama-server`。你可以通过挂载本地模型文件并在命令后追加参数来运行。

```bash
# 运行 Vulkan 版本示例
docker run --rm -it \
  --device /dev/dri \
  -v /path/to/your/models:/models \
  -p 8080:8080 \
  maharajah/llama-cpp:vulkan-latest \
  -m /models/your-model.gguf --host 0.0.0.0
```
