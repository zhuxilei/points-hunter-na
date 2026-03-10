# Daily Blog Post Workflow

## 写作与推送流程

### 1. 搜索新闻素材
```bash
# 搜索过去24小时的积分/里程/信用卡新闻
web_search: freshness=pd, query="credit card points transfer bonus airline miles hotel rewards March 2026"
```

### 2. 写文章
- 路径: `blog/posts/YYYY-MM-DD-daily-digest.html`
- 标题格式: `Chase转Avios 20% · Amex转Lifemiles 15% · Capital One转酒店30%`
- 日期: 写当天的日期（如3月9日就写Mar 9，不要写错）

### 3. 更新 index.html（两处都要改！）
**重点：根目录 `index.html` 和 `blog/index.html` 都要更新！**

在 `const posts = [` 开头添加新文章：

```javascript
{
  slug: "blog/posts/2026-03-09-daily-digest.html",  // 注意是 blog/posts/
  date: { en: "Mar 9, 2026", zh: "2026年3月9日" },
  tags: { en: ["Daily Digest", "Transfer Bonus"], zh: ["每日速递", "转分Bonus"] },
  featured: true,
  icon: "🔥",
  title: {
    en: "Chase 20% → Avios · Amex 15% → Lifemiles · Capital One 30% → Hotels",
    zh: "Chase转Avios 20% · Amex转Lifemiles 15% · Capital One转酒店30%"
  },
  excerpt: {
    en: "Chase UR → Avios 20% bonus through 3/31...",
    zh: "Chase UR转Avios 20%到3/31..."
  },
  readTime: "2 min read"
},
```

### 4. Git 提交与推送
**关键：Vercel 連接的是 `main` 分支，不是 `master`！**

```bash
git add blog/posts/YYYY-MM-DD-daily-digest.html index.html blog/index.html
git commit -m "Add daily digest Mar 9: ..."
git push origin main   # ← 推送到 main 分支！
```

### 5. 验证
```bash
# 等待约15秒后检查
curl -s "https://points-hunter-na.vercel.app/" | grep "Mar 9"
```

---

## ⚠️ 常见错误

| 错误 | 原因 | 解决 |
|------|------|------|
| 首页不显示新文章 | 只改了 blog/index.html 没改根目录 index.html | 两个文件都要改 |
| Vercel 不更新 | 推到了 master 而不是 main | `git push origin main` |
| 文章页404 | 路径错误 | 确认是 `blog/posts/` 而不是 `posts/` |

---

## 分支说明
- **GitHub Pages**: `master` 分支
- **Vercel**: `main` 分支 ← 重点！
- 每次推送要同时推送到两个分支或者只推 main（Vercel 是主站）
