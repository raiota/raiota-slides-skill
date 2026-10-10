# raiota-slides

HTML でスライドを組むための個人用 Claude Code プラグイン。Catppuccin Latte 配色・M PLUS Rounded 1c・16 レイアウト。

配布は、個人用マーケットプレイス [raiota/claude-plugins](https://github.com/raiota/claude-plugins)（名前は `raiota`）から行う。このリポジトリはプラグイン本体だけを持ち、マーケットプレイスの目録は持たない。

## 導入（別の端末で使う）

Claude Code で次の 2 コマンドを実行する。

```
/plugin marketplace add raiota/claude-plugins
/plugin install raiota-slides@raiota
```

インストール結果に `Run /reload-plugins to activate.` と出たら、そのコマンドも実行する。

毎回コマンドを打たずに済ませたい場合は、`~/.claude/settings.json` に次を書いておく。まだマーケットプレイスを登録していない端末なら、起動時に自動で入る。

```json
{
  "extraKnownMarketplaces": {
    "raiota": {
      "source": {
        "source": "github",
        "repo": "raiota/claude-plugins"
      },
      "autoUpdate": true
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

`plugins/raiota-slides/.claude-plugin/plugin.json` の `version` を上げて push すると、マーケットプレイス `raiota` の自動更新で各端末に届く。`version` を上げないうちは、push しても各端末は今のバージョンのままになる。

すぐに反映したい端末では、次を実行する。

```
/plugin update raiota-slides@raiota
```

## 構成

```
plugins/
└── raiota-slides/
    ├── .claude-plugin/
    │   └── plugin.json       プラグインのメタデータ（version で配布を管理する）
    └── skills/
        └── raiota-slides/
            ├── SKILL.md      スライド作成の手順と規則
            ├── assets/       boilerplate・レイアウト・deck-stage.js・image-slot.js
            └── reference/    デザイントークン
```

変更したら `claude plugin validate plugins/raiota-slides` で JSON とスキルの妥当性を確認する。
