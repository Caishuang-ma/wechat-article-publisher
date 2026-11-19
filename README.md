# WeChat Article Publisher

一个面向 Codex 的中文工作流 Skill，用于把已经完成的 Markdown 或文章正文整理为飞书发布稿，生成并插入配图，再通过壹伴导入微信公众号并协助完成发布。

## 能做什么

- 将本地 Markdown 或完整正文整理到飞书文档
- 删除仅供写作研究使用的“主要资料”等尾部区块
- 清理粘贴产生的多余空格、空行和异常段落间距
- 默认生成一张题图和两张正文配图，并插入语义合适的位置
- 通过壹伴将完整飞书稿导入微信公众号
- 检查标题、作者、正文、图片、封面和文末内容
- 在正式发布前停下来请求确认，并把微信扫码验证交给用户

## 安装

### 当前项目使用

将仓库克隆到项目的 Skill 目录：

```bash
mkdir -p .agents/skills
git clone https://github.com/Caishuang-ma/wechat-article-publisher.git \
  .agents/skills/wechat-article-publisher
```

### 当前用户的所有项目使用

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/Caishuang-ma/wechat-article-publisher.git \
  ~/.agents/skills/wechat-article-publisher
```

安装完成后开启一个新的 Codex 会话，让 Skill 被重新发现。

## 使用

显式调用：

```text
$wechat-article-publisher

请把这篇文章处理成微信公众号草稿：
/absolute/path/to/article.md

先不要正式发布，做到发布前让我确认。
```

也可以直接提出自然语言请求，例如：

```text
把这篇 Markdown 整理到飞书，生成三张配图，再通过壹伴导入公众号。
正式发布前让我确认。
```

建议同时说明：

- 文章文件、正文或文档链接
- 目标公众号账号（存在多个账号时）
- 只准备草稿，还是继续到正式发布
- 可选的配图数量或视觉风格

## 工作流

```text
Markdown/正文
  → 飞书发布稿
  → 清理研究资料和多余空白
  → 生成并插入配图
  → 壹伴导入一次
  → 导入后验收
  → 设置封面
  → 用户确认
  → 微信扫码与发布结果核验
```

完整规则见 [`SKILL.md`](SKILL.md) 和 [`references/publishing-flow.md`](references/publishing-flow.md)。

## 依赖与边界

该 Skill 描述工作流，不包含账号、密钥或登录信息。实际执行通常需要：

- 可用的飞书文档能力，例如 `lark-doc`
- 图片生成能力，例如 `imagegen`
- 可操作已登录网页的浏览器能力，例如 `ego-browser`
- 已安装并登录的壹伴插件和微信公众号后台

对外发布属于不可自动假定的动作。即使用户一开始要求“发布”，Skill 仍会在真正点击发布前再次确认，并保留登录、扫码和验证环节给用户处理。

## 许可证

[MIT](LICENSE)
