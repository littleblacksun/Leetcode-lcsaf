# 上传与 README 维护说明

当需要把当前 Leetcode 学习项目同步到 GitHub，并依据最新笔记更新仓库首页时，按以下规则执行。

## 目标仓库

- 远程地址：`https://github.com/littleblacksun/Leetcode-lcsaf.git`
- 目标分支：`main`

## 推送当前项目

1. 在项目根目录确认状态：`git status`。若工作区干净，先使用 `git pull --rebase origin main` 同步远程分支，再开始编辑。
2. 若工作区已有待提交修改，不要丢弃或暂存后强制同步；完成检查、提交后再执行 rebase 同步。
3. 检查将要提交的内容，避免上传 `.reasonix/`、`.obsidian/workspace.json`、密钥或其他本机临时文件。
4. 更新 `README.md`（规则见下文），然后执行：

   ```powershell
   git add -A
   git commit -m "Update LeetCode study notes"
   git pull --rebase origin main
   git push origin main
   ```

5. rebase 出现冲突时，解决冲突、`git add <文件>`，再执行 `git rebase --continue`；不要使用强制推送。
6. 推送后运行 `git status -sb`，确认工作区干净且 `main` 与 `origin/main` 已同步。

## GitHub 图片显示兼容

Obsidian 的双中括号图片嵌入语法（`!` 后接 `[[figure/image.png]]`）不是标准 Markdown，GitHub 会把它当作普通文本显示。为了同时兼容 Obsidian 与 GitHub，笔记中的图片必须使用标准 Markdown 语法。

1. 将 Obsidian 图片嵌入改为标准链接。例如：

   ```md
   <!-- 不要使用 Obsidian 的双中括号图片嵌入：GitHub 不会渲染 -->

   <!-- 使用：Obsidian 与 GitHub 都能显示 -->
   ![题目截图](./figure/Pasted%20image%2020260828113445.png)
   ```

2. 图片路径相对于当前 Markdown 文件书写，统一使用 `/`。路径中有空格时使用 `%20`，例如 `Pasted%20image.png`；其他 URL 特殊字符也应进行百分号编码。
3. 图片文件必须实际位于仓库中并被 Git 跟踪。`figure/` 目录不要加入 `.gitignore`。
4. 推送前检查是否仍有 Obsidian 图片嵌入，并检查图片链接是否存在：

   ```powershell
   rg -n --glob '*.md' --glob '!.reasonix/**' '!\[\[[^\]]+\]\]'
   ```

   上述命令应没有输出；随后使用 GitHub 网页预览已修改的 Markdown，确认图片正常显示。

## README.md 更新规则

根据当前目录中的 Leetcode Markdown 笔记维护 README。每次更新前扫描项目中的 `.md` 文件；不要为不存在的文档创建链接，也不要把 `.reasonix/` 中的内部附件或规则文件列入导航。

README 应保持简洁、可爱、可直接导航：

- 保留仓库名称与“跟着灵茶山艾府刷题”的学习说明。
- 使用 emoji、短句、分隔线和清晰的层级，让首页轻松但不过度花哨。
- 提供“刷题路线”入口，以及滑动窗口、二分算法、数据结构、链表、二叉树、网格图、回溯、动态规划的总览入口。
- 每个链接使用相对 Markdown 路径，例如 `[滑动窗口](./01-滑动窗口/滑动窗口-总览.md)`，确保 GitHub 网页中可直接点击。
- 若目录出现新的题型或新增笔记，在 README 中追加对应入口；删除或重命名笔记时同步修正链接。
- 可加入一个小型进度区、学习打卡提示或“持续更新中”文案，但不要虚构题量、日期或完成进度。

## 推荐 README 结构

```md
# 🌱 Leetcode-lcsaf

> 跟着灵茶山艾府刷题的学习记录。慢慢积累，也要一直进步 ✨

## 🧭 刷题导航

- [🗺️ 刷题路线](./00-刷题路线.md)
- [🪟 滑动窗口](./01-滑动窗口/滑动窗口-总览.md)
- [🔍 二分算法](./02-二分算法/二分算法-总览.md)
- [🧰 数据结构](./03-数据结构/数据结构-总览.md)
- [🔗 链表](./04-链表/链表-总览.md)
- [🌳 二叉树](./05-二叉树/二叉树-总览.md)
- [🧩 网格图](./06-网格图/网格图-总览.md)
- [🪄 回溯](./07-回溯/回溯-总览.md)
- [💡 动态规划](./08-动态规划/动态规划-总览.md)

---

_持续更新中，今天也一起 AC 吧！_ 🐣
```
