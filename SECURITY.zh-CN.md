# 安全策略

## API Key

这个仓库不能包含真实 API key、token、cookie、私有 endpoint 或客户密钥。

`ppt-maker` 本身不需要 API key。它是一个路由和边界约束 plugin。如果下游 Agent 要调用大模型、图片模型、PPTX 生成器或托管服务，用户必须在 Git 之外配置自己的密钥。

真实密钥建议放在：

- 本地 `.env` 文件，且被 Git ignore
- shell 环境变量
- macOS Keychain、1Password 或其他密钥管理器
- GitHub Actions repository secrets（如果之后加入 CI）
- 目标 Agent 平台自己的 secret/config UI

提交到 Git 的文件只能放占位示例，例如 `examples/local-config.example.txt`。

## 发布前检查

推送前跑一次密钥扫描：

```bash
rg -n "sk-|ghp_|gho_|api[_-]?key|secret|token|password|BEGIN [A-Z ]*PRIVATE KEY" .
git status --short --ignored .env
```

预期结果：

- tracked files 里没有真实密钥值
- 本地 `.env` 显示为 ignored

## 如果密钥已经提交

1. 立刻在服务商后台吊销泄露的 key。
2. 从仓库移除密钥。
3. 轮换所有相关凭据。
4. 把 public Git history 当作已经被复制处理。
