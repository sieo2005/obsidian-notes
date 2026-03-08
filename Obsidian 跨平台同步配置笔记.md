# Obsidian 跨平台同步配置笔记

## 背景需求
- **设备**：Windows PC + iPhone
- **目标**：实现 Obsidian 笔记跨设备同步
- **尝试过的方案**：
  - AList WebDAV ❌（配置复杂，405错误）
  - Google Drive ❌（Obsidian不支持直接连接）
  - Git + GitHub ✅（最终成功方案）

---

## 最终方案：Git + GitHub 同步

### 一、Windows 端配置

#### 1. 安装 Obsidian Git 插件
- 社区插件市场搜索 **Obsidian Git**
- 安装并启用

#### 2. 插件核心设置

**自动同步设置**：

| 设置项 | 推荐值 |
|--------|--------|
| Auto commit-and-sync interval | 5（分钟）|
| Auto commit-and-sync after stopping file edits | ✅ 开启 |
| Push on commit-and-sync | ✅ 开启 |
| Pull on startup | ❌ 关闭 |

**提交信息设置**：
- Commit message：`vault backup: {{date}}`
- Date format：`YYYY-MM-DD HH:mm:ss`

#### 3. 连接 GitHub 仓库

**创建 GitHub 仓库**：
1. 访问 `github.com` → New repository
2. Repository name：`obsidian-notes`
3. 选择 Private（私有）或 Public（公开）
4. 勾选 Add a README file
5. 点击 Create

**创建 Personal Access Token**：
1. GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Generate new token (classic)
3. Note：`Obsidian Sync`
4. Expiration：No expiration
5. 勾选 **repo**（完整控制私有仓库）
6. 生成并复制 token（`ghp_xxxxxxxx`）

**配置本地 Git**：

```powershell
# 进入 Obsidian 库文件夹
cd "G:\我的云端硬盘\codex作品\第二大脑"

# 初始化 Git（如未初始化）
git init

# 添加远程仓库（token嵌入URL）
git remote add origin https://sieo2005:ghp_你的Token@github.com/sieo2005/obsidian-notes.git

# 添加文件并提交
git add .
git commit -m "first commit"

# 推送（本地是master分支）
git push -u origin master