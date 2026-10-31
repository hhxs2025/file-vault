# 📁 File Vault (Tiny File Vault)

**File Vault** 是一款专为fnOS打造的现代化、极简私有文件托管中心。告别臃肿的网盘，在这里你可以像操作本地硬盘一样，安全、高效地管理你的数字资产。

> **💡 核心理念**：零外部依赖、极速秒开、数据完全私有、支持多版本控制。

![File Vault 预览图](https://f.hhxs2026.top:8888/f/imgs/file-vault1.webp)

---

## ✨ 核心特性

- 🚀 **桌面级控制台**：全新侧边栏布局，实时统计文件总数、目录数与占用空间。
- 📂 **原生目录系统**：支持新建多层级文件夹、快捷面包屑导航与一键重命名。
- ⚡ **极速代码预览**：内置零依赖的高亮引擎，压缩的单行 JSON 文件自动美化展开，完美支持 HTML、JSON、Markdown 等文本的在线预览与编辑。
- 🔄 **文件版本控制**：同名文件上传自动生成历史版本，随时一键回滚，修改不翻车。
- 🔒 **分享管理中心**：支持“公开/私有”属性切换，可生成带时效、带提取码、带下载次数限制的临时分享链接（可作为个人图床或 API 分发站）。
- 🗂️ **高级批量操作**：列表勾选模式，支持文件/目录一键批量打包下载（ZIP）与批量删除。
- 📋 **剪贴板秒传**：随手截图或复制文本，按 `Ctrl+V` 即可快速保存至当前目录。
- 🛡️ **安全私有**：自带高强度管理员登录鉴权，支持安全登出，数据完全留在自己手中。

---

## 🚀 快速部署

### 方式一：Docker Compose 部署（推荐）

在任意安装了 Docker 的服务器上，创建 `docker-compose.yml` 文件：

```yaml
services:
  file-vault:
    image: ccr.ccs.tencentyun.com/hhxs2025/file-vault:1.1
    container_name: file-vault
    restart: unless-stopped
    ports:
      - "8080:8080" # 前面的 8080 可改为你想要的宿主机端口
    volumes:
      - ./data:/data # 数据目录，保存所有上传的文件和 SQLite 数据库
    environment:
      - ADMIN_USER=admin
      - ADMIN_PASS=admin123 # 强烈建议修改为强密码
      - DATA_DIR=/data
      - MAX_SIZE_MB=2048
```

启动服务：

```bash
docker compose up -d
```

访问 `http://你的IP:8080` 即可进入控制台。

### 方式二：飞牛 fnOS 原生安装

本项目已完美适配飞牛 FPK 打包规范。在飞牛应用中心安装时，系统会自动弹窗让你配置：
1. **访问端口**（向导变量 `${wizard_app_port}`）
2. **管理员密码**（向导变量 `${wizard_app_pass}`）

应用数据将被安全地存储在飞牛的系统目录 `${TRIM_PKGVAR}` 中。

---

## ⚙️ 环境变量说明

| 变量名 | 默认值 | 说明 |
| :--- | :--- | :--- |
| `ADMIN_USER` | `admin` | 控制台登录用户名 |
| `ADMIN_PASS` | `admin123` | 控制台登录密码（**请务必修改**） |
| `DATA_DIR` | `/data` | 数据库与文件存储的物理路径 |
| `MAX_SIZE_MB` | `2048` | 单个文件上传的最大限制（单位：MB） |

---

## 🛠️ 本地开发与构建

如果你需要修改源码并自行构建镜像：

```bash
# 1. 克隆代码
git clone https://github.com/yourname/file-vault.git
cd file-vault

# 2. 构建镜像
docker build -t file-vault:local .

# 3. 运行
docker run -d -p 8080:8080 -v $(pwd)/data:/data --name file-vault file-vault:local
```

**技术栈**：
- 后端：Python 3.11 + FastAPI + SQLite3
- 前端：纯原生 HTML / CSS / JavaScript（零外部依赖，无 CDN 阻塞）

---

## 📝 更新日志

### v1.1.0 (2026-10-30)
- **✨ 交互与 UI 全面焕新**
  - 新增桌面级侧边栏布局与空间统计。
  - 支持新建真正的空文件夹与面包屑导航。
  - 全新引入列表勾选模式，支持全选、批量打包下载（ZIP）与批量删除。
- **🔒 安全与分享机制升级**
  - 新增文件“公开/私有”属性切换。
  - 支持生成带时效、提取码、下载限制的临时分享链接。
  - 重构鉴权体系，升级为带时效的 Session 状态。
- **⚡ 性能与预览优化**
  - 移除所有外部 CDN 依赖，实现控制台极速秒开。
  - 内置轻量级高亮引擎，支持 JSON 自动美化展开。
- **🛠️ 底层修复**
  - **[重要]** 增加数据库自动迁移逻辑，完美兼容 1.0.0 老版本数据库无损升级。
  - 修复批量删除文件夹时遗留空记录的问题。

---

## ⚠️ 免责声明

本项目仅供个人学习与私有化部署使用。请勿用于任何违反当地法律法规的用途。请务必在公网暴露时设置强密码，并建议配合反代工具（如 Nginx、Lucky）开启 HTTPS 访问。

## 📄 开源协议

[MIT License](LICENSE)