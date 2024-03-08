<div align="center">
  <h1> GitHub Workflow for Generating Zhihu Badge </h1>
</div>
<p align="center">
  <a href="https://www.zhihu.com/people/6a90e389b176a5cd201ec3860c8adbd7">
    <img src="https://img.shields.io/badge/3843-blue?logo=zhihu&logoColor=blue&label=Follower&labelColor=white&color=blue"></a>
  <a href="https://www.zhihu.com/people/6a90e389b176a5cd201ec3860c8adbd7">
    <img src="https://img.shields.io/badge/1308-blue?logo=zhihu&logoColor=blue&label=Voteup&labelColor=white&color=blue"></a>
  <a href="https://www.zhihu.com/people/6a90e389b176a5cd201ec3860c8adbd7">
    <img src="https://img.shields.io/badge/551-blue?logo=zhihu&logoColor=blue&label=Thanked&labelColor=white&color=blue"></a>
</p>

## Introduction

This GitHub Workflow generates Zhihu badges displaying various metrics related to a Zhihu user's profile. These badges visually represent metrics such as follower count, voteup count, and thanked count.

## Features

- **Follower Badge**: Displays the number of followers a Zhihu user has.
- **Voteup Badge**: Displays the total number of votes received by a Zhihu user's answers.
- **Thanked Badge**: Displays the total number of times a Zhihu user has been thanked for their answers.

## Usage

### Writing the README.md File

Copy the provided badges and paste them into your README.md file. Here's an example:

```markdown
<div align="center">
  <h1> My Zhihu Profile Metrics </h1>
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

Replace `your_zhihu_username` with your actual Zhihu username in the badge URLs. Don't worry about the numbers on the badges; they will be updated with the newly retrieved data after running the workflow.

### Adding Source Code and Workflow File

1. **Add Python Script**: Copy the `generate_zhihu_badge.py` script from the `src` directory to your project.
2. **Copy YAML File**: Copy the `update_zhihu_follower_badge.yml` file in the `.github/workflows` directory of your GitHub repository to the same directory in your project. This YAML file defines the workflow for updating the Zhihu Follower Badge.

### Workflow Explanation

```yaml
name: Update Zhihu Follower Badge

# schedule:
  #   # 每天 UTC 时间00:00 运行
  #   - cron: '0 0 * * *'
  
on:
  workflow_dispatch:
    # Manually triggered

jobs:
  update-badge:
    runs-on: ubuntu-latest

    steps:
      # Checkout repository code
      - name: Checkout repository
        uses: actions/checkout@v2

      # Generate Zhihu Follower Badge
      - name: Generate Zhihu Follower Badge
        run: python generate_zhihu_badge.py

      # Commit and push if changed
      - name: Commit and push if changed
        run: |
          git config --global user.email "action@github.com"
          git config --global user.name "GitHub Action"
          git add -A
          git commit -m "Update Zhihu Follower Badge" -a || exit 0 # Exit if no changes
          git push
```

The workflow defined in the YAML file can be triggered manually using the `workflow_dispatch` event or automatically run at 24:00 every day if you uncomment the `schedule` section. It consists of a single job named `update-badge` that runs on the `ubuntu-latest` environment.

**Run Workflow**: This workflow is triggered manually using the workflow_dispatch event. Navigate to the Actions tab of your GitHub repository, select the workflow, and click the "Run workflow" button to trigger it.

For more details, refer to the [GitHub Actions documentation](https://docs.github.com/en/actions).

## License

This project is licensed under the MIT License - see the LICENSE file for details.
