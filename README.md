# Clash IP Checker 🛡️

一个基于 **Clash Meta (Mihomo)** 和 **FastAPI** 的高性能订阅 IP 检测工具。
专为筛选高质量节点设计，提供 Web 可视化界面和 API 订阅转换服务。

> **功能亮点**: 极速检测 (API Mode) | 智能缓存 | 自动队列 | Docker 部署 | 隐私安全

---

## ⚡ 核心功能

*   **Web 可视化面板**: 现代化的 Vue/Tailwind 界面，实时显示检测进度和日志。
    *   👉 **访问地址**: `http://127.0.0.1:8000/ipcheck`
*   **API 订阅转换**: 直接生成带检测结果的订阅链接，兼容 Clash 客户端。
    *   👉 **订阅格式**: `http://127.0.0.1:8000/check?url=[原始订阅链接]`
*   **智能缓存系统**:
    *   基于内容 MD5 的去重缓存 (1小时有效期)。
    *   **任务复用**: 多个用户同时请求相同订阅时，共享同一个检测任务，不仅省流且零等待。
*   **队列保护**: 内置任务队列限制 (默认 10 并发)，防止服务器过载。
*   **Clean Output**: 自动屏蔽垃圾节点，重命名优质节点 (包含 emoji 评级、地区、运营商信息)。

## 🚀 快速开始

### 使用 Docker Compose (推荐)

最简单的部署方式。只需一条命令：

```bash
# 1. 克隆代码
git clone https://github.com/tombcato/clash-ip-checker.git
cd clash-ip-checker

# 2. 启动服务
docker-compose up -d --build
```

启动后，访问 **[http://127.0.0.1:8000/ipcheck](http://127.0.0.1:8000/ipcheck)** 即可使用。

### 部署到 Google Cloud (GCP)

支持 **Cloud Run** (Serverless) 和 **Compute Engine** (VM) 部署。
详见部署指南：[📄 DEPLOY_GCP.md](./DEPLOY_GCP.md)

---

## 🛠️ 配置说明 (`core/config.py`)

可通过环境变量或修改 `config.yaml` 调整行为：

| 环境变量 | 默认值 | 说明 |
| :--- | :--- | :--- |
| `MAX_QUEUE_SIZE` | `10` | 最大并发检测任务数。超过限制时将降级为只下载不检测。 |
| `MAX_AGE` | `3600` | 缓存有效期 (秒)。 |
| `CLASH_API_URL` | `http://127.0.0.1:9090` | 内部 Mihomo 控制接口地址。 |

---

## 🔒 隐私与免责

*   **数据隐私**: 本工具仅作为网络连接性测试用途。您的订阅内容仅在服务器内存/缓存中短暂停留（默认1小时），之后会被彻底清除。我们绝不向任何第三方分享您的配置。
*   **免责申明**: 本项目按“现状”提供，开发者不对因使用本工具导致的任何后果（如流量消耗、账号封禁等）负责。请务必遵守当地法律法规。
*   **开源协议**: MIT License.

---
*Built with ❤️ by Antigravity*
