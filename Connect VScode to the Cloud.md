
# VS Code 与 GitHub 云端连接及操作指南

**摘要**：本文档详细总结了如何在 VS Code 中建立与 GitHub 的连接，以及在修改代码或文件名称后如何通过“命令行 (Terminal)”和“图形界面 (GUI)”两种方式将变动同步到云端。

---

## 第一部分：建立连接 (Initialize & Connect)

**场景**：本地已有一个项目文件夹（例如 `12_Nocturne_AI`），需要将其上传到 GitHub 上新建的空仓库(注意:要同时在github上面建好一个空仓库)。

### 方式 A：终端命令行 (Terminal) —— *最稳定、推荐*

1. 在 VS Code 打开项目文件夹，使用快捷键 `Ctrl` + `~` 打开终端。
2. 初始化本地仓库：
   ```bash
   git init
   ```
3. 将所有文件添加到暂存区：
   ```bash
   git add .
   ```
4. 提交文件到本地仓库（备注为 "Initial commit"）：
   ```bash
   git commit -m "Initial commit"
   ```
5. **关键步骤**：关联远程 GitHub 仓库（请替换为你的真实 URL）：
   ```bash
   git remote add origin https://github.com/hanxiangli666/你的仓库名.git
   ```
6. 推送到云端主分支：
   ```bash
   git branch -M main
   git push -u origin main
   ```

### 方式 B：VS Code 图形界面 (GUI) —— *纯鼠标操作*

1. 点击左侧侧边栏的 **源代码管理 (Source Control)** 图标。
2. 点击蓝色的 **"Initialize Repository" (初始化仓库)** 按钮。
3. 在输入框填写 "Initial commit"，点击上方的 **提交 (Commit)** / **勾号 (✓)**。
4. 按 `Ctrl` + `Shift` + `P`，输入 `Add Remote`，选择 **"Git: Add Remote..."**。
5. 粘贴 GitHub 仓库链接，回车。
6. 输入远程名称：`origin`，回车。
7. 回到源代码管理面板，点击 **"Publish Branch" (发布分支)** 按钮完成上传。

---

## 第二部分：修改代码后上传 (Update & Sync)

**场景**：日常开发中，修改了代码内容（如 `main.py`），需要保存并同步到云端。

### 方式 A：终端命令行

1. *(可选)* 查看当前状态：
   ```bash
   git status
   ```
2. **暂存 (Stage)** 所有改动：
   ```bash
   git add .
   ```
3. **提交 (Commit)** 并填写备注：
   ```bash
   git commit -m "Updated main logic"
   ```
4. **推送 (Push)** 到云端：
   ```bash
   git push origin main
   ```

### 方式 B：VS Code 图形界面

1. 点击左侧 **源代码管理** 图标，查看 "Changes" 列表。
2. **暂存**：点击 "Changes" 栏右侧的 **+ 号** (Stage All Changes)。
3. **提交**：在输入框填写备注（如 "Fixed bug"），点击 **提交 (Commit)** 按钮。
4. **推送**：点击蓝色的 **"Sync Changes" (同步更改)** 按钮。

---

## 第三部分：修改文件名/移动文件后上传 (Rename & Move)

**场景**：重命名了文件（如 `API.txt` -\> `env.txt`）或移动了文件夹。

### 方式 A：终端命令行

Git 会自动识别重命名操作，无需特殊命令，操作流程与普通修改一致。

1. 在资源管理器中重命名文件。
2. **执行标准三步曲**：
   ```bash
   git add .
   git commit -m "Renamed files"
   git push origin main
   ```

### 方式 B：VS Code 图形界面

1. 在左侧资源管理器重命名文件。
2. 进入 **源代码管理** 面板。
   * *注：可能会看到“删除旧文件”和“新增新文件”两个记录，这是正常的。*
3. **一键暂存**：点击 "Changes" 栏旁边的 **+ 号**。
   * *此时 VS Code 通常会自动识别并合并显示为 **R (Renamed)** 状态。*
4. **提交**：输入备注，点击提交。
5. **推送**：点击 **"Sync Changes"**。

---
## 第四部分: 导入别人的仓库进行学习
**关联了一个远程仓库**
我们需要把它的“发货地址”改成**你自己**的 GitHub 仓库。请按照以下步骤操作：

### 第一步：在 GitHub 上新建空仓库

1.  去 GitHub 网站，点击右上角 **+** -\> **New repository**。
2.  仓库名输入：**`micrograd`**。
3.  **不要**勾选 Initialize with README/.gitignore（因为你本地已经有了）。
4.  点击 **Create repository**。

### 第二步：修改“发货地址” (在 VS Code 终端输入)

请依次运行以下 3 条命令：

1.  **删除旧的关联** (断开与原作者仓库的连接)：

    ```powershell
    git remote remove origin
    ```

2.  **添加新的关联** (连到你的新仓库)：
    *(请把下面的链接换成你刚才新建的仓库链接)*

    ```powershell
    git remote add origin https://github.com/hanxiangli666/你的仓库名.git
    ```

3.  **改名并推送** (把 master 改为 main 并上传)：

    ```powershell
    git branch -M main
    git push -u origin main
    ```

-----

### 🎉 预期结果
刷新你的 GitHub 页面，你会发现代码都在里面了。然后你就可以去你的**个人主页 README**，把项目表格里的 Micrograd 链接更新为这个新仓库的链接了！
## 附录：常用建议

* **什么时候用 GUI？**
  适合日常简单的提交、重命名文件，或者需要直观对比代码差异（Diff）时。
* **什么时候用 命令行？**
  适合第一次配置环境、解决冲突、或者 GUI 报错无法处理时。
* **重要提醒**：
  修改文件名时，如果只是修改了大小写（如 `api.py` -\> `API.py`），Windows 系统可能无法识别。建议先改为临时名字（如 `temp.py`）提交一次，再改为最终名字 `API.py` 提交第二次。

