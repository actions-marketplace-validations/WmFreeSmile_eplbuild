# EPL 编译工具 GitHub Action

这个 GitHub Action 可以帮助你在 CI/CD 流程中自动编译 EPL (Embedded Procedural Language) 源文件（`.e`）为 COFF (Common Object File Format) 目标文件（`.o`）。

## 快速开始

将以下代码添加到你的 GitHub Actions 工作流配置文件中：

```yaml
steps:
  - name: Checkout code
    uses: actions/checkout@v3
  
  - name: Compile EPL file
    uses: WmFreeSmile/elbuild@v1
    with:
      file: src/main.e  # 你的 EPL 源文件路径
      output: build/main.o  # 输出的 COFF 文件路径
```

## 输入参数

| 参数名   | 描述                     | 是否必需 | 默认值 |
|----------|--------------------------|----------|--------|
| `file`   | EPL 源文件路径 (*.e)     | 是       | 无     |
| `output` | 输出的 COFF 文件路径 (*.o) | 是       | 无     |

## 示例工作流

下面是一个完整的 GitHub Actions 工作流示例，展示如何使用这个 Action 编译 EPL 项目：

```yaml
name: Build EPL Project

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: windows-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Compile EPL files
        uses: WmFreeSmile/elbuild@v1
        with:
          file: src/main.e
          output: build/main.o

      - name: Upload compiled object file
        uses: actions/upload-artifact@v3
        with:
          name: compiled-objects
          path: build/*.o
```

## 自定义与扩展

这个 Action 使用 Node.js 实现，你可以根据需要修改源代码来扩展功能：

1. 克隆这个仓库：`git clone https://github.com/WmFreeSmile/elbuild.git`
2. 修改 `index.js` 文件添加新功能
3. 提交更改并发布新版本

## 技术支持

如果你在使用过程中遇到问题，请在 GitHub 仓库中提交 Issues：[https://github.com/WmFreeSmile/elbuild/issues](https://github.com/WmFreeSmile/elbuild/issues)

## 贡献

欢迎贡献代码！请遵循以下步骤：

1. Fork 这个仓库
2. 创建你的特性分支：`git checkout -b feature/new-feature`
3. 提交你的更改：`git commit -m 'Add some feature'`
4. 将分支推送到 GitHub：`git push origin feature/new-feature`
5. 提交 Pull Request

## 许可证

本项目采用 MIT 许可证，详情请参阅 [LICENSE](LICENSE) 文件。