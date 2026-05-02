# API Key 与本地配置

`ppt-maker` 本身不需要 API key。它给 Agent 提供的是安全的 PPT 生产路由：HTML 展示、图片资产、可编辑 PPTX、固定模板填充或交付前验证。

只有当你选择的 Agent 或后端要调用外部服务时，API key 才会相关，例如：

- 大模型服务商
- 图片生成服务商
- PPTX/文档转换服务
- 托管自动化平台

## 规则

不要把真实 key 提交进这个仓库。

Git 里只放占位示例：

```bash
cp examples/local-config.example.txt .env
```

然后在本地编辑 `.env`：

```bash
OPENAI_API_KEY=your_real_key_here
ANTHROPIC_API_KEY=your_real_key_here
FAL_KEY=your_real_key_here
DASHSCOPE_API_KEY=your_real_key_here
```

`.env` 已被 Git ignore，只应留在本机。

## 给客户的说明

当 Agent 需要服务商 key 时，把这段给客户：

```text
这个项目不会自带 API key。请你自己注册对应服务商账号，生成 API key，并在自己的 Agent runtime 或本地 `.env` 文件里配置。不要把真实 key 粘贴到 GitHub issue、commit、README、截图或聊天记录里。配置完成后，让 Agent 只验证变量是否存在，不要打印 key 值。
```

## 给 Agent 的说明

```text
不要在这个仓库里寻找维护者自己的 API key。
这个仓库故意不包含真实 secret。
如果工作流需要服务商 key，请让用户把自己的 key 配置在本地 `.env`、环境变量、密钥管理器或目标 Agent 平台的 secret UI 里。
不要把真实 key 写入 tracked files。
不要在日志中打印 key 值。
验证 secret 时只检查变量是否存在。
```
