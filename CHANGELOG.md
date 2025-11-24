## 2025-11-24

Fork Google Gemini-cli以支持bun运行环境

### 设置上游仓库 (Upstream)

告诉你的本地 Git，Google 的官方仓库在哪里，以便日后同步更新。

```bash
# 1. 进入目录
cd gemini-cli

# 2. 添加官方仓库为 'upstream' (上游)
git remote add upstream https://github.com/google-gemini/gemini-cli.git

# 3. 验证一下 (你应该能看到 origin 和 upstream 两个远程源)
git remote -v
# 输出应该类似：
# origin    https://github.com/wiajs/gemini-cli.git (你的)
# upstream  https://github.com/google-gemini/gemini-cli.git (官方的)
```

### 创建bun分支

`git checkout -b bun`

### 提交代码

```bash
git add .
git commit -m "feat: setup environment for bun runtime"
git push -u origin bun
```

### 合并 Google 新版本

```bash
# 1. 切回主分支
git checkout main

# 2. 从 Google 官方拉取最新代码到本地 main
git pull upstream main

# 3. 将本地 main 同步到你自己的 GitHub 仓库 (可选)
git push origin main

# 4. 切回你的 Bun 分支
git checkout bun

# 5. 【关键】将主分支的更新合并进你的功能分支
git merge main
# 或者使用 rebase (更高级，保持提交记录整洁)
# git rebase main

```

### node-pty

bun安装node-pty很慢，暂时屏蔽，考虑使用 bun的$替代

```json
  "trustedDependencies": [
    "node-pty",
    "@lydell/node-pty",
    "@lydell/node-pty-win32-x64",
    "esbuild"
  ],  
  "optionalDependencies": {
    "@lydell/node-pty": "1.1.0",
    "@lydell/node-pty-darwin-arm64": "1.1.0",
    "@lydell/node-pty-darwin-x64": "1.1.0",
    "@lydell/node-pty-linux-x64": "1.1.0",
    "@lydell/node-pty-win32-arm64": "1.1.0",
    "@lydell/node-pty-win32-x64": "1.1.0",
    "node-pty": "^1.0.0"
  },
```
