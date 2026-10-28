# Tiny File Vault (极简文件托管中心)

Tiny File Vault 是一个轻量级、高性能的私有文件托管与版本管理系统。专为飞牛 fnOS (FPK) 及 Docker 环境设计，适用于个人图床、静态网页托管、API 配置文件分发及软件包仓库。

## 核心特性

- **全格式支持**：完美托管 `md`、`json`、`html`、`png/jpg/webp/gif`、`txt`、`pdf`、`apk`、`fpk` 等格式。
- **自动版本管理**：同名文件覆盖上传自动生成历史版本，支持随时预览、下载或一键回滚。
- **在线预览与编辑**：内置 Markdown 渲染与代码语法高亮，支持在浏览器内直接编辑文本或代码并保存为新版本。
- **剪贴板秒传**：支持 `Ctrl + V` 直接粘贴截图或文本，自动生成文件并上传至当前目录。
- **目录与权限管理**：支持多级虚拟目录、跨目录搜索、批量 ZIP 打包下载与鉴权。数据全部存储在本地。
- **极简前端**：Vue 3 + Tailwind CSS 构建，无冗余依赖，自带暗黑模式与自定义交互弹窗。

## 部署方式

### 方式一：Docker Compose 部署

创建一个 `docker-compose.yml` 文件：

```yaml
services:
  file-vault:
    image: ccr.ccs.tencentyun.com/hhxs2025/file-vault:latest
    container_name: file-vault
    restart: unless-stopped
    ports:
      - "18080:8080"
    volumes:
      - ./data:/data
    environment:
      - ADMIN_USER=admin
      - ADMIN_PASS=admin123
      - DATA_DIR=/data
      - MAX_SIZE_MB=2048