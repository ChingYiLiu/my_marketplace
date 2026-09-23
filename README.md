# My Marketplace

這個 repository 提供兩個 plugin：

- `family-comic`：根據家庭情境與內附風格參考圖製作六格漫畫。
- `engineering-portfolio-extractor`：將經核准的工程概念重新實作為可公開的作品集案例。

兩個工具共用 `plugins/<plugin-name>/skills/` 下的 skill，但各自讀取不同的 marketplace 與 plugin 設定檔。以下範例在其他 repository 啟用 `family-comic`；如需另一個 plugin，將名稱改為 `engineering-portfolio-extractor`。使用 GitHub 來源前，先將本 repository 的變更推送到 GitHub。

## Claude Code

Claude Code 讀取本 repository 的 `.claude-plugin/marketplace.json`，並從各 plugin 的 `.claude-plugin/plugin.json` 與 `skills/` 載入內容。在**使用 plugin 的 repository** 建立 `.claude/settings.json`：

```json
{
  "extraKnownMarketplaces": {
    "my-marketplace": {
      "source": {
        "source": "github",
        "repo": "ChingYiLiu/my_marketplace"
      }
    }
  },
  "enabledPlugins": {
    "family-comic@my-marketplace": true
  }
}
```

Claude Code 在專案受信任後讀取這份設定。也可以在 Claude Code 執行 `/plugin marketplace add ChingYiLiu/my_marketplace`，再執行 `/plugin install family-comic@my-marketplace`。

## Codex

Codex 讀取本 repository 的 `.agents/plugins/marketplace.json`，並從各 plugin 根目錄的 `plugin.json` 與 `skills/` 載入內容。先在使用者的環境註冊 marketplace 並安裝 plugin：

```sh
codex plugin marketplace add ChingYiLiu/my_marketplace
codex plugin add family-comic@my-marketplace
```

接著在**使用 plugin 的 repository** 建立 `.codex/config.toml`：

```toml
[plugins."family-comic@my-marketplace"]
enabled = true
```

Codex 只在受信任的專案載入專案設定。若要停用已安裝的 plugin，將 `enabled` 改為 `false`；若要啟用另一個 plugin，先安裝它，再新增對應的 `[plugins."<plugin-name>@my-marketplace"]` 區塊。Codex 不讀取 Claude Code 的 `.claude/settings.json`。

更新 plugin 後，請同步調整該 plugin 的 `.claude-plugin/plugin.json` 與根目錄 `plugin.json` 版本號，讓已安裝的使用者取得新版本。
