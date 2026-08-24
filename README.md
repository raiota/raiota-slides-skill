# raiota marketplace

raiota の個人用 Claude Code プラグインを配布するマーケットプレイス。

## 収録プラグイン

| プラグイン      | 内容                                                                             |
| --------------- | -------------------------------------------------------------------------------- |
| `raiota-slides` | HTML スライドのテンプレート。Catppuccin Latte 配色・M PLUS Rounded 1c・22 レイアウト |

## 導入（別の端末で使う）

Claude Code で次の 2 コマンドを実行する。

```
/plugin marketplace add raiota/raiota-slides-skill
/plugin install raiota-slides@raiota
```

インストール結果に `Run /reload-plugins to activate.` と出たら、そのコマンドも実行する。

毎回コマンドを打たずに済ませたい場合は、`~/.claude/settings.json` に次を書いておくと起動時に自動で入る。

```json
{
  "extraKnownMarketplaces": {
    "raiota": {
      "source": {
        "source": "github",
        "repo": "raiota/raiota-slides-skill"
      }
    }
  },
  "enabledPlugins": {
    "raiota-slides@raiota": true
  }
}
```

## 使い方

インストールすると `raiota-slides` スキルが有効になり、「スライドを作って」「LT の資料」などの依頼で自動的に呼ばれる。明示的に呼ぶ場合は次のとおり。

```
/raiota-slides:raiota-slides
```

## 更新

このリポジトリに push したあと、各端末で以下を実行する。

```
/plugin marketplace update raiota
```

## 構成

```
.
├── .claude-plugin/
│   └── marketplace.json          マーケットプレイスの目録
└── plugins/
    └── raiota-slides/
        ├── .claude-plugin/
        │   └── plugin.json       プラグインのメタデータ
        └── skills/
            └── raiota-slides/
                ├── SKILL.md      スライド作成の手順と規則
                ├── assets/       boilerplate・レイアウト・deck-stage.js
                └── reference/    デザイントークン
```

変更したら `claude plugin validate .` で JSON とスキルの妥当性を確認する。
