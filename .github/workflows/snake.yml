# GitHub Action 名稱
name: Generate snake animation

# 這個 Action 的觸發時機
on:
  # 允許手動從 Actions 頁面觸發
  workflow_dispatch:
  
  # 定時觸發：這裡設定為每 12 小時執行一次
  schedule:
    - cron: "0 */12 * * *" # 您可以根據需求調整時間

# 定義工作流程
jobs:
  build:
    # 在最新的 Ubuntu 環境上執行
    runs-on: ubuntu-latest
    
    steps:
      # 第一步：簽出 (Checkout) 您的儲存庫程式碼
      - uses: actions/checkout@v3

      # 第二步：產生貪吃蛇動畫
      # 使用 platane/snk@v3 這個別人寫好的 Action
      - name: generate snake.svg
        uses: platane/snk@v3
        with:
          # 您的 GitHub 使用者名稱
          github_user_name: ${{ github.repository_owner }}
          
          # 指定輸出的 SVG 檔案路徑
          # 格式：<輸出目錄>/<檔名>.svg
          outputs: dist/github-contribution-grid-snake.svg

      # 第三步：將生成的檔案推送到 output 分支
      # 使用 crazy-max/ghaction-github-pages@v3 來部署
      - name: push snake.svg to the output branch
        uses: crazy-max/ghaction-github-pages@v3
        with:
          # 指定要部署的分支名稱
          target_branch: output
          # 指定要部署的來源目錄
          build_dir: dist
        env:
          # GitHub Token，用於授權推送
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
