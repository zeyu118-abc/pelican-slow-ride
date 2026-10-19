# 发布到 GitHub Pages

这份指南把「白鹈鹕的午后骑行」发布成一个可在线访问的 GitHub Pages 站点。全程只需要 GitHub 账号；懂一点 Git 的话也可以用命令行发布。

## 发布前

建议先做两件小事：

1. 如果想修改仓库名，建议使用小写英文和连字符，例如 `pelican-slow-ride`。当前仓库名已经是 `pelican-slow-ride`。
2. 如果已经知道最终的 Pages 地址，可以在 `README.md` 顶部补上一行在线预览链接。当前已填入本项目地址。

`LICENSE` 已使用 GitHub 账号 `zeyu118-abc` 作为版权人；如果你希望换成别的名字，可以直接修改。

`.nojekyll` 是空白文件，用于关闭 GitHub Pages 的 Jekyll 处理。它不是必须的，但对纯静态站点更省心。

## 方式 A：直接在 GitHub 网页发布（推荐）

### 1. 创建仓库

1. 登录 GitHub，打开 <https://github.com/new>。
2. 填写 **Repository name**，例如 `pelican-slow-ride`。
3. 选择 **Public**。免费的 GitHub Pages 通常要求仓库公开。
4. **不要**勾选 “Add a README file”“Add .gitignore”“Choose a license”，因为项目里已经准备好了这些文件。
5. 点击 **Create repository**。

### 2. 上传文件

1. 在新仓库页面点击 **Add file → Upload files**。
2. 把本项目里的这些内容拖进页面：
   - `index.html`
   - `assets/` 文件夹
   - `README.md`
   - `PUBLISH.md`
   - `LICENSE`
   - `.gitignore`
   - `.nojekyll`（Windows 资源管理器里可能被隐藏；看不到也没关系，可以用后面的“手动创建”步骤补上）
3. 确认 `index.html` 在仓库根目录，而不是在某个子文件夹里。
4. 在下方填写提交信息，例如 `feat: publish pelican slow ride`，点击 **Commit changes**。

如果网页上传没有带上 `.nojekyll`，可以手动创建：**Add file → Create new file**，文件名填 `.nojekyll`，内容留空，提交即可。没有它站点一般也能正常显示。

### 3. 开启 GitHub Pages

1. 进入仓库的 **Settings**（设置）。
2. 左侧点击 **Pages**。
3. 在 **Build and deployment** 下，将 **Source** 选为 **Deploy from a branch**。
4. **Branch** 选择 `main`，目录选择 `/(root)`，点击 **Save**。
5. 回到 **Pages** 页面等待 1–3 分钟，刷新后会显示站点地址。

地址通常是：

```text
https://USERNAME.github.io/REPO/
```

把 `USERNAME` 换成你的 GitHub 用户名，`REPO` 换成仓库名。

> 如果仓库名是 `USERNAME.github.io`，地址会直接是 `https://USERNAME.github.io/`。

### 4. 完善仓库首页

1. 在仓库首页右侧点击 **About** 旁的齿轮图标。
2. 填写 **Description**，例如：
   `A white pelican riding a bicycle — a single-file animated webpage.`
3. 在 **Website** 填入你的 Pages 地址。
4. 在 **Topics** 里添加几个标签，例如：
   `animation`、`svg`、`css`、`html`、`github-pages`、`illustration`、`pelican`
5. 可选：在 **Settings → General → Social preview** 上传 `assets/preview.png`，作为分享卡片图片。

## 方式 B：用 Git 命令行发布

先在 GitHub 上创建一个**空仓库**（仍然不要勾选自动生成 README），然后在项目文件夹中打开 PowerShell：

```powershell
# 如果你还没有配置过 Git 身份
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"

git init
git add .
git commit -m "feat: publish pelican slow ride"
git branch -M main

# 将下面两个占位符换成你的用户名和仓库名
git remote add origin https://github.com/USERNAME/REPO.git
git push -u origin main
```

推送成功后，按上面的步骤在 **Settings → Pages** 中开启 Pages。如果你的默认分支不叫 `main`，在 Pages 设置里选择实际分支即可。

### 创建仓库时误加了 README 怎么办

最简单的做法是删除刚刚创建的仓库，重新建一个不勾选 README 的仓库。也可以直接在网页上使用 **Add file → Upload files** 上传本项目文件；若本地已经执行过 `git init`，可以使用下面的命令合并远程的初始提交：

```powershell
git pull origin main --allow-unrelated-histories
# 如果 README 或 LICENSE 出现冲突，保留本项目的版本并解决冲突
git add .
git commit -m "merge: combine with initial repository files"
git push -u origin main
```

## 更新页面

### 网页上传方式

1. 进入 GitHub 仓库，打开要修改的文件。
2. 点击铅笔图标编辑，或重新通过 **Add file → Upload files** 上传替换文件。
3. 提交后，GitHub Pages 会自动重新部署。刷新页面时建议使用 `Ctrl+F5` 强制刷新。

### 命令行方式

```powershell
git add .
git commit -m "update: refresh pelican illustration"
git push
```

## 可选：绑定自己的域名

如果你有自己的域名：

1. 在仓库 **Settings → Pages → Custom domain** 中填写域名。
2. 到域名注册商处添加 GitHub Pages 要求的 DNS 记录。
3. 等 DNS 生效后，开启 **Enforce HTTPS**。

具体 DNS 记录会因“根域名还是 www 子域名”而不同，建议照着 GitHub 官方文档操作：

<https://docs.github.com/zh/pages/configuring-a-custom-domain-for-your-github-pages-site>

## 常见问题

### 访问 Pages 地址出现 404

- 确认 `index.html` 在仓库根目录，没有放进子文件夹。
- 确认 **Settings → Pages** 里选择的是 `main` 分支和 `/(root)`。
- Pages 首次发布可能需要等 1–3 分钟。
- 查看仓库 **Actions** 里是否有 `pages build and deployment` 正在运行。

### 页面空白或样式错乱

- 用浏览器开发者工具（F12）查看 Console 有没有报错。
- 确认上传时保留了 `assets` 等目录结构。
- 如果只是图片没显示，检查 Markdown 中路径的大小写：`assets/preview.png`。

### 更新后线上还是旧页面

- GitHub Pages 需要一点时间重新构建。
- 使用 `Ctrl+F5` 或无痕窗口重新打开。
- 确认提交已经推送到 Pages 使用的分支。

### 音乐/铃声没有响

车铃使用 Web Audio，需要一次真实的点击或按键才能启动，这是浏览器的自动播放策略。先点一下页面或按 `B` 即可。

### 动画一开始没有动

如果你在系统中开启了“减少动态效果”（Reduce Motion），页面会默认暂停。点击左下角播放按钮即可继续。

## 发布检查清单

- [ ] `index.html` 在仓库根目录
- [ ] `assets/preview.png` 可正常显示
- [ ] `LICENSE` 已替换版权人
- [ ] Settings → Pages 已选择 `main` + `/(root)`
- [ ] Pages 地址能打开页面
- [ ] 手机宽度下检查布局
- [ ] 仓库 About 已填写描述和在线地址
- [ ] 可选：已设置 Topics 和 Social preview

发布完成后，就可以把 `https://USERNAME.github.io/REPO/` 分享给朋友了。
