# 强制规则：Git自动提交

## 提交时机
- 完成重要任务后
- 系统迭代后
- 用户明确说“commit”或调用 /commit 技能

## 提交规范
```bash
git add [具体文件]   # 不使用 git add -A
git commit -m "[类型]: [简短描述]"
```

类型：
- content：内容相关
- system：系统优化
- memory：记忆库更新
- task：任务管理
- iteration：系统迭代

## 禁止操作
- 禁止 force push
- 禁止 amend 非自己的 commit
- 禁止 git add -A
- 必须等用户说“commit”才能提交
