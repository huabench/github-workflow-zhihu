<div align="right">
  <a href="README.md">
    [English]
  </a>
</div>

<div align="center">
  <h1> 自动生成知乎徽章 </h1>
</div>
<p align="center">
  <a href="https://www.zhihu.com/people/kong-zhong-ji-qi-ren-qian-yan">
    <img src="https://img.shields.io/badge/3843-blue?logo=zhihu&logoColor=blue&label=Follower&labelColor=white&color=blue"></a>
  <a href="https://www.zhihu.com/people/kong-zhong-ji-qi-ren-qian-yan">
    <img src="https://img.shields.io/badge/1308-blue?logo=zhihu&logoColor=blue&label=Voteup&labelColor=white&color=blue"></a>
  <a href="https://www.zhihu.com/people/kong-zhong-ji-qi-ren-qian-yan">
    <img src="https://img.shields.io/badge/551-blue?logo=zhihu&logoColor=blue&label=Thanked&labelColor=white&color=blue"></a>
</p>

## 介绍

此 GitHub 工作流程生成显示知乎用户资料相关指标的徽章。这些徽章直观地展示了关注者数量、赞同数量和感谢数量等指标。

上面徽章中链接的知乎账户属于我工作的实验室。实验室的 GitHub 主页链接是 [https://github.com/WestlakeIntelligentRobotics](https://github.com/WestlakeIntelligentRobotics)。

## 特点

- **关注者徽章**：显示知乎用户的关注者数量。
- **赞同徽章**：显示知乎用户回答得到的赞同总数。
- **喜欢徽章**：显示知乎用户因回答而收到的喜欢总数。

## 用法

### 编写 README.md 文件

复制提供的徽章，并粘贴到你的 README.md 文件中。以下是一个示例：


```markdown
<div align="center">
  <h1> 我的知乎数据 </h1>
</div>
<p align="center">
  <a href="https://www.zhihu.com/people/your_zhihu_username">
    <img src="https://img.shields.io/badge/3843-blue?logo=zhihu&logoColor=blue&label=Follower&labelColor=white&color=blue"></a>
  <a href="https://www.zhihu.com/people/your_zhihu_username">
    <img src="https://img.shields.io/badge/1308-blue?logo=zhihu&logoColor=blue&label=Voteup&labelColor=white&color=blue"></a>
  <a href="https://www.zhihu.com/people/your_zhihu_username">
    <img src="https://img.shields.io/badge/551-blue?logo=zhihu&logoColor=blue&label=Thanked&labelColor=white&color=blue"></a>
</p>
```

将 your_zhihu_username 替换为您在徽章 URL 中的真实知乎用户名。不用担心徽章上的数字，它们将在运行工作流程后更新为新检索到的数据。

### 添加源代码和工作流程文件

1. **添加 Python 脚本**：从 `src` 目录中复制 `generate_zhihu_badge.py` 脚本到您的项目中。
2. **复制 YAML 文件**：从您的 GitHub 存储库的 `.github/workflows` 目录中复制 `zhihu_follower.yml` 文件到您项目中的相同目录。此 YAML 文件定义了用于更新知乎关注者徽章的工作流程。


### Workflow文件说明

```yaml
name: Update Zhihu Follower Badge

on:
  # schedule:
  #   # 每天在 UTC 时间 00:00 运行
  #   - cron: '0 0 * * *'
  workflow_dispatch:
    # 手动触发

jobs:
  update-badge:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.x'

    - name: Install dependencies
      run: pip install -r requirements.txt

    # 从知乎获取关注者数量并生成徽章
    - name: Generate Zhihu Follower Badge
      run: python src/generate_zhihu_badge.py
      env:
        ZHIHU_USERNAME: your_zhihu_username
      
    - name: Commit and push if changed
      run: |
        git config --global user.email "action@github.com"
        git config --global user.name "GitHub Action"
        git add -A
        git commit -m "Update Zhihu Follower Badge" -a || exit 0
        git push

```

在 YAML 文件中定义的工作流程可以通过 `workflow_dispatch` 事件手动触发，或者如果取消注释 `schedule` 部分，则每天的 24:00 自动运行一次。 它包含一个名为 `update-badge` 的单个作业，在 `ubuntu-latest` 环境上运行。

**运行工作流程**：此工作流程通过 `workflow_dispatch` 事件手动触发。在 GitHub 存储库的 Actions 选项卡中，选择工作流程，然后单击“Run workflow”按钮来触发。

欲了解更多详情，请参阅[GitHub Actions 文档](https://docs.github.com/en/actions)。

## 许可证

本项目根据 MIT 许可证获得许可 - 有关详情，请参阅 LICENSE 文件。