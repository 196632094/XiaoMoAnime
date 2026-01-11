# XiaoMoAnime
# 部署指南 (Deployment Guide)

本文档介绍如何通过 Python 直接部署或使用 Docker 容器部署本项目。

## 目录
- [环境要求](#环境要求)
- [方式一：Python 直接部署](#方式一python-直接部署)
- [方式二：Docker 部署](#方式二docker-部署)
- [常见问题](#常见问题)

---

## 环境要求

- **操作系统**: Windows / Linux / macOS
- **Python**: 3.9 或更高版本
- **FFmpeg**: 必须安装并添加到系统环境变量（用于视频合并）

---

## 方式一：Python 直接部署

适用于开发调试或不希望使用 Docker 的环境。

### 1. 安装基础工具

确保已安装 `Python` 和 `FFmpeg`。
- **Windows**: 下载安装包安装 Python，下载 FFmpeg 解压并将 bin 目录加入 Path。
- **Linux (Ubuntu/Debian)**:
  ```bash
  sudo apt-get update
  sudo apt-get install python3 python3-pip ffmpeg
  ```

### 2. 安装依赖

在项目根目录下运行：

```bash
pip install -r requirements.txt
```

> **注意**: 如果遇到 `gevent` 或 `eventlet` 安装错误，请检查 `requirements.txt` 是否包含这些库。本项目推荐使用 `threading` 模式，已移除对这些库的强制依赖。

### 3. 运行应用

```bash
python app.py
```

启动成功后，访问浏览器：
- 地址: `http://localhost:5000`

---

## 方式二：Docker 部署 (推荐)

适用于生产环境或希望环境隔离的用户。

### 1. 安装 Docker

请确保已安装 Docker 和 Docker Compose。

### 2. 启动服务

在项目根目录下（包含 `docker-compose.yml` 的目录）运行：

上传 `docker-compose.yml` 文件到服务器，运行：


### 3. 数据持久化

容器配置了以下挂载卷，确保数据不会因重启丢失：
- `./downloads`: 下载的视频文件
- 如需更改挂载下载目录，修改 `docker-compose.yml` 中的 `xiaomo_data`改为你的存储目录
- `./logs`: 运行日志
- `./config`: 配置文件（如 `settings.json`）

### 4. 访问服务

启动完成后，访问：
- 地址: `http://localhost:5000`

---

## 常见问题

### 1. 视频无法合并
- 检查 **FFmpeg** 是否安装正确。
- Python 部署模式下，在终端输入 `ffmpeg -version` 确认是否有输出。
- Docker 模式下，镜像内已预装 FFmpeg，无需额外配置。
