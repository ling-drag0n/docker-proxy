# 一键把DockerHub镜像搬运到GitHub 容器注册表 (GHCR.IO)

## 项目简介

本项目通过 GitHub Actions **自动将DockerHub镜像搬运到GitHub容器注册表 (GHCR.IO)**，避免镜像被封禁或撤回，确保你的镜像资源安全可靠。  
你可以免费使用 GitHub 提供的 **每月 2000 分钟**的私有仓库运行时长，或者使用公有仓库，享受**无限制的运行时长**。同时，配合 **南京大学开源镜像站**，加速国内拉取 GHCR.IO 镜像的速度。

## 使用步骤

### 1. 克隆项目到你的 GitHub 仓库

请不要使用 Fork！因为 Fork 仓库运行 GitHub Actions 会受到运行时长限制。使用以下方法通过 Git 导入项目：

1. 点击此链接进入 GitHub 的导入页面：[GitHub 导入页面](https://github.com/new/import)
2. 在 "Your old repository’s clone URL" 一栏中输入：  
   ```
   https://github.com/foss-android/dockerhub2ghcr.io.git
   ```
3. 根据提示完成项目导入。

### 2. 手动触发 GitHub Actions

#### 步骤：

1. 进入你的 GitHub 仓库，在页面顶部找到并点击 “**Actions**” 选项卡。

2. 在左侧栏中，找到 "**DockerHub 镜像复制到 GHCR.IO**" 的工作流名称，点击它。

3. 在右上角点击 "**Run workflow**" 按钮（运行工作流）。这将会弹出参数输入框。

4. 你需要在弹出的输入框中填写以下参数：
   - **dockerhub_image**：DockerHub 镜像名称（默认是 `nginx`），如 `alpine` 或 `python`。
   - **tag**：镜像的标签，默认是 `latest`。可以填写 `1.19` 或其他指定版本。
   - **ghcr_image**：你希望推送到 GHCR.IO 的镜像名称，可以自己定义一个，比如 `myimage`。

5. 填写好参数后，点击 "**Run workflow**" 按钮。GitHub Actions 会开始自动运行，将你指定的 DockerHub 镜像同步到 GHCR.IO。

#### 参数填写示例：

- **dockerhub_image**: `nginx`
- **tag**: `latest`
- **ghcr_image**: `my-nginx`

完成后，GitHub Actions 会自动拉取 DockerHub 镜像，并推送到 GHCR.IO。

### 3. 国内加速镜像拉取

为了加速国内的镜像下载速度，可以使用南京大学的开源镜像站。你只需要在拉取镜像时，将 `ghcr.io` 替换为 `ghcr.nju.edu.cn`：

```bash
docker pull ghcr.nju.edu.cn/<your-username>/<your-image>:<tag>
```

这样可以大幅提升国内环境下从 GHCR.IO 拉取镜像的速度。

## 优势

- **防止镜像撤回或封禁**：同步到 GHCR.IO 私有仓库，即使镜像被撤回也不会影响使用。
- **免费使用 GitHub 容器服务**：每月 2000 分钟的免费私有仓库运行时长，或公有仓库无限制时长。
- **国内镜像站加速**：使用南京大学镜像站，让国内拉取 GHCR.IO 镜像更快更稳定。
