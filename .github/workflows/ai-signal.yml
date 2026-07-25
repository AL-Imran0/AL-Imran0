name: Update AI Signal (Claude API)

on:
  schedule:
    - cron: "0 6 * * *"   # daily at 06:00 UTC
  workflow_dispatch: {}     # allows manual "Run workflow" trigger too

permissions:
  contents: write

jobs:
  update-signal:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo
        uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: "20"

      - name: Generate today's signal via Claude API
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
        run: node scripts/generate_signal.mjs

      - name: Commit updated signal.json
        run: |
          git config user.name "github-actions[bot]"
          git config user.email "github-actions[bot]@users.noreply.github.com"
          git add data/signal.json
          git diff --quiet --cached || git commit -m "chore: refresh AI signal"
          git push
