# README 内容同步检查清单

> 用于维护 README.md 和 README.zh-CN.md 内容一致性的检查清单

## 使用说明

每当更新 `SKILL.md` 或 `README.md` 时，使用此清单确保中文版本同步更新。

---

## 同步流程

### 1. 源文档优先原则
```
SKILL.md (技术规范) → README.md (英文用户指南) → README.zh-CN.md (中文翻译)
```

### 2. 更新顺序
1. 先更新英文 README.md
2. 再更新中文 README.zh-CN.md
3. 最后更新此检查清单（如需要）

---

## 内容核对表

### 基本信息
- [ ] 标题一致（# Cursor Controller Skill）
- [ ] GitHub 链接正确（指向 cursor-controller）
- [ ] OpenClaw 徽章链接有效

### 项目说明横幅
- [ ] 英文："This is an OpenClaw Agent Skill"
- [ ] 中文："这是一个 OpenClaw Agent Skill"
- [ ] 都说明是纯文档项目
- [ ] 都指向 SKILL.md

### 安装部分
- [ ] Prerequisites 说明 Cursor CLI 安装
- [ ] 都说明是复制 SKILL.md 文档
- [ ] 三种安装选项完整（Project/Global/Clone）
- [ ] Clone 命令使用正确的仓库名

### 快速开始
- [ ] 说明 agent 命令来自 Cursor CLI
- [ ] 包含 Cursor CLI 文档链接
- [ ] 示例命令一致

### 认证部分
- [ ] 浏览器认证说明
- [ ] API Key 认证说明
- [ ] 故障排除提示

### 常见用例
- [ ] 代码任务示例
- [ ] 代码审查示例
- [ ] CI/CD 集成示例

### 工作模式
- [ ] Agent 模式
- [ ] Plan 模式
- [ ] Ask 模式

### 高级功能 ⭐ 重点检查
- [ ] **Sandbox 模式** - 沙盒控制
- [ ] **Max 模式** - 最大令牌使用
- [ ] **模型选择** - gpt-5.2, claude-3-5-sonnet 等
- [ ] **批处理** - 循环处理多个文件

### Cloud Agent
- [ ] 云端任务说明
- [ ] 访问链接

### 会话管理
- [ ] agent ls
- [ ] agent resume
- [ ] agent --resume

### 安全与注意事项 ⭐ 重点检查
- [ ] **安全说明** - sudo 密码处理
- [ ] **速率限制** - API 限制警告

### 页脚
- [ ] 文档链接
- [ ] 贡献说明
- [ ] 许可证信息

---

## 自动化检查命令

### 检查行数差异
```bash
wc -l README.md README.zh-CN.md
```

### 检查章节数量
```bash
echo "English sections: $(grep -c '^##' README.md)"
echo "Chinese sections: $(grep -c '^##' README.zh-CN.md)"
```

### 检查关键术语
```bash
# 检查功能关键词
grep -n "sandbox\|max-mode\|model" README.md
grep -n "沙盒\|Max 模式\|模型" README.zh-CN.md

# 检查安全相关
grep -n "security\|password\|rate limit" README.md
grep -n "安全\|密码\|速率" README.zh-CN.md
```

### 验证链接
```bash
# 检查 GitHub 链接
grep -n "github.com/Edison-A-N" README.md README.zh-CN.md
```

---

## 翻译术语表

| 英文 | 中文 | 说明 |
|------|------|------|
| OpenClaw Agent Skill | OpenClaw Agent Skill | 保持英文 |
| documentation-only | 纯文档 | - |
| standalone tool | 独立工具 | - |
| Cursor CLI | Cursor CLI | 保持英文 |
| Advanced Features | 高级功能 | - |
| Sandbox Mode | 沙盒模式 | - |
| Max Mode | Max 模式 | 保持英文 |
| Model Selection | 模型选择 | - |
| Batch Processing | 批处理 | - |
| Security & Notes | 安全与注意事项 | - |
| Rate Limits | 速率限制 | - |
| Cloud Agent | Cloud Agent | 保持英文 |

---

## 常见问题

### Q: 英文和中文行数不一致怎么办？
A: 中文版本通常会多几行（因为中文字符可能导致换行），这是正常的。关键是章节数量要一致。

### Q: 发现内容不同步怎么办？
A: 1. 以英文 README.md 为准
   2. 更新中文 README.zh-CN.md
   3. 更新此检查清单（如有新增内容）

### Q: 如何确保不遗漏更新？
A: 每次修改 README 后：
1. 运行上面的自动化检查命令
2. 逐条核对内容核对表
3. 对比章节数量

---

## 版本历史

| 日期 | 版本 | 说明 |
|------|------|------|
| 2026-03-06 | v1.0 | 初始版本，包含 T1-T7 所有更新 |

---

*最后更新: 2026-03-06*
