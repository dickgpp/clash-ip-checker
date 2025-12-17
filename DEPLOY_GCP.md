# 部署到 Google Cloud Platform (GCP) 指南

本项目基于 Docker 构建，支持部署到 Google Cloud 的多种服务。推荐使用 **Cloud Run** (Serverless, 按需付费) 或 **Compute Engine** (VM, 类似传统服务器)。



## Compute Engine (GCE)

如果你需要**持久化缓存**，或者希望通过 Docker Compose 管理，可以使用 VM。

### 1. 创建 VM 实例

在 GCP 控制台创建一个实例（推荐 "Container Optimized OS" 或 Ubuntu）。
*   机器类型: `e2-micro` (免费层级) 或 `e2-small` 即可。
*   防火墙: 勾选 "Allow HTTP traffic"，并在网络设置中放行 8000 端口。

### 2. 部署

SSH 登录到 VM，然后拉取代码并运行：

```bash
# 安装 Docker & Git (如果使用 Ubuntu)
sudo apt-get update && sudo apt-get install -y docker.io docker-compose git

# 克隆代码
git clone https://github.com/tombcato/clash-ip-checker.git
cd clash-ip-checker

# 运行
sudo docker-compose up -d --build
```

### 3. 访问

访问 `http://[External_IP]:8000/ipcheck`。

---

## 常见问题

### 端口配置
我们在 `entrypoint.sh` 中配置了 `uvicorn ... --port ${PORT:-8000}`。Cloud Run 会自动注入 `PORT` 环境变量（通常是 8080），应用会自动适配。

### 内存不足
如果遇到 Clash 启动失败或检测过程中崩溃，请尝试增加内存限制（GCE 升级机型或 Cloud Run 增加 `--memory 2Gi`）。
