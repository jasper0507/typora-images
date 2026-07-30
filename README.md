# typora-images

个人笔记图床仓库，配合 **Typora + PicGo-Core** 使用。图片上传后通过 **jsDelivr CDN** 访问。

| 项目 | 说明 |
|------|------|
| 用途 | Markdown / Typora 插图托管 |
| 可见性 | Public（公开，便于 CDN 直链） |
| 默认分支 | `main` |
| 图片目录 | [`img/`](./img/) |

## 链接格式

上传成功后，笔记中的图片地址形如：

```text
https://cdn.jsdelivr.net/gh/jasper0507/typora-images@main/img/<文件名>
```

等价关系：

| 类型 | URL |
|------|-----|
| jsDelivr（推荐） | `https://cdn.jsdelivr.net/gh/jasper0507/typora-images@main/img/xxx.png` |
| GitHub 原始地址 | `https://raw.githubusercontent.com/jasper0507/typora-images/main/img/xxx.png` |

两者指向同一文件；jsDelivr 负责加速访问，GitHub 负责存储。

若 jsDelivr 较慢，可尝试：

```text
https://fastly.jsdelivr.net/gh/jasper0507/typora-images@main/img/xxx.png
```

## 本地配置（PicGo-Core / Typora）

配置文件位置（Windows）：

```text
C:\Users\<用户名>\.picgo\config.json
```

Typora 自带 PicGo 路径示例：

```text
C:\Users\<用户名>\AppData\Roaming\Typora\picgo\win64\picgo.exe
```

关键配置字段：

```json
{
  "picBed": {
    "current": "github",
    "uploader": "github",
    "github": {
      "repo": "jasper0507/typora-images",
      "branch": "main",
      "token": "<GitHub Token，需 repo 权限>",
      "path": "img/",
      "customUrl": "https://cdn.jsdelivr.net/gh/jasper0507/typora-images@main"
    }
  }
}
```

| 字段 | 含义 |
|------|------|
| `repo` | `用户名/仓库名` |
| `branch` | 分支，默认 `main` |
| `token` | 有写权限的 GitHub Token（勿提交到仓库） |
| `path` | 仓库内存储路径，当前为 `img/` |
| `customUrl` | 返回链接前缀；填 jsDelivr 后笔记里自动用 CDN 地址 |

命令行测试上传：

```bash
picgo upload path/to/image.png
```

## 目录结构

```text
typora-images/
├── README.md
└── img/           # 图片存放目录（由 PicGo 自动写入）
    └── *.png
```

文件名由本地 PicGo 插件按时间戳规则生成（如 `YYYYMMDDHHmmss.png`），避免重名冲突。

## 使用注意

1. **本仓库仅作图床**，请勿提交 Token、密钥等敏感信息。
2. 仓库需保持 **Public**，jsDelivr 才能稳定拉取图片。
3. 新上传图片经 CDN 分发时，偶发短暂延迟，刷新或稍后再访问即可。
4. GitHub API 有频率限制，个人笔记插图通常足够；勿当作大流量图床。
5. 删除仓库内文件后，旧 Markdown 中的链接会失效；CDN 缓存也可能短暂残留。

## 许可

本仓库中的图片内容归上传者所有。代码/说明文档可按需自用。
