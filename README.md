# .github/workflows/snake.yml
name: Generate Snake

on:
  schedule:
    # Chạy vào 00:00 UTC mỗi ngày
    - cron: "0 0 * * *"
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    # Vẫn giữ quyền truy cập
    permissions: 
      contents: write
      
    steps:
      - uses: actions/checkout@v2
      
      # GỌI ACTION VÀ TẠO FILE SVG
      - uses: platane/snk@v3 # <--- CHUYỂN SANG DÙNG @v3 HOẶC @v2
        id: snake-gif
        with:
          github_user_name: kietuanphuoc84tv
          # Gộp hai outputs lại, dùng cú pháp cũ nhưng đảm bảo action nhận diện
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark
            
      # Đẩy các file SVG đã tạo lên branch 'dist'
      - uses: crazy-max/ghaction-github-pages@v2
        with:
          target_branch: dist
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
