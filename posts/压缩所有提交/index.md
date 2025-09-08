# 压缩所有提交


想把 **当前分支的所有提交** 压缩成一个提交，但是分支里有一些 **Merge Commit（本地和远程的合并提交）**,也就是说，历史不是线性的，不能直接用普通 `git rebase -i`。

---

## 🔑 关键点

1. **Merge Commit** 有两个父节点，如果想压缩所有提交，需要 **抛弃历史，只保留当前文件状态**。
2. **安全做法**：创建一个全新的孤儿分支（`--orphan`），把当前工作区内容提交成一个 commit，然后强制推送覆盖原分支。

---

## 步骤

### 1️⃣ 创建孤儿分支

```bash
git checkout --orphan temp_branch
```

* `--orphan` → 新建一个没有历史的分支
* 此时 HEAD 是新分支，没有任何提交

---

### 2️⃣ 添加当前文件

```bash
git add -A
```

* 把工作区里所有文件添加到暂存区

---

### 3️⃣ 创建一个提交

```bash
git commit -m "压缩所有提交为一个提交"
```

* 当前分支现在只有 **一个提交**，保留了所有内容

---

### 4️⃣ 替换原分支

```bash
git branch -M main
```

* 把孤儿分支重命名为 `main`（或你的目标分支名）

---

### 5️⃣ 强制推送到远程

```bash
git push origin main --force
```

* `--force` 会覆盖远程历史
* 所以远程的 merge commit 和所有旧提交都会被删除，只保留你现在的单一提交

---

## ✅ 总结

* **普通 squash / rebase** 不能处理 merge commit
* **孤儿分支 + 一次提交 + force push** 是最安全的彻底压缩方法
* 适合博客仓库或 Pages 部署仓库，保留最新内容即可

---


---

> 作者: [Jason](https://github.com/actforjason)  
> URL: https://actforjason.github.io/posts/%E5%8E%8B%E7%BC%A9%E6%89%80%E6%9C%89%E6%8F%90%E4%BA%A4/  

