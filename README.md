# Investing rules and skills

ClaudeとCodexの両方で利用する、投資プロジェクトの共通ルールとSkillを管理するリポジトリです。

## 構成

```text
investing/
├── README.md
├── rules.md
└── skills/
    ├── stock-analysis/
    │   └── SKILL.md
    ├── earnings-calendar/
    │   ├── SKILL.md
    │   └── agents/openai.yaml
    ├── economic-indicator-preview/
    │   └── SKILL.md
    ├── portfolio-price-check/
    │   ├── SKILL.md
    │   └── agents/openai.yaml
    ├── market-change-analysis/
    │   ├── SKILL.md
    │   └── agents/openai.yaml
    └── reliable-source-search/
        └── SKILL.md
```

## ファイルの役割

### `rules.md`

投資プロジェクト全体で常に適用するルールです。投資対象、情報源、数値取得、マネックス証券の利用、推測と事実の区別など、個別の作業手順ではない恒常的な方針を記載します。

### `skills/*/SKILL.md`

ClaudeとCodexで共有する作業手順です。

| Skill | 役割 |
|---|---|
| `stock-analysis` | 企業概要、決算、セクター、個別材料、株価・テクニカルを調べ、銘柄分析を作成する |
| `earnings-calendar` | マネックス証券から米国株保有銘柄を取得し、今後1か月の決算予定を確認する |
| `economic-indicator-preview` | CPI、雇用統計、FOMCなどの発表前に、市場予想と注目点を整理する |
| `portfolio-price-check` | マネックス証券の米国株保有残高から、取得できる価格・評価損益情報を確認する |
| `market-change-analysis` | 市場の変動理由を、マクロ、セクター、個別材料の順に調査する |
| `reliable-source-search` | Web検索で利用する情報源と、確認できない場合の扱いを定める |

### `skills/*/agents/openai.yaml`

OpenAI／Codex用の設定です。Skill一覧に表示する名称・説明、Codexでの呼び出し例、自動起動の可否を設定します。

Claudeでは使用しないため、Claude側はこのファイルを無視して構いません。共有リポジトリに置いたままで問題ありません。

## 明示的な呼び出し

| Skill | Claude | Codex |
|---|---|---|
| 決算カレンダー | `/earnings-calendar` | `$earnings-calendar` |
| ポートフォリオ価格確認 | `/portfolio-price-check` | `$portfolio-price-check` |
| 市場変動要因分析 | `/market-change-analysis` | `$market-change-analysis` |

`stock-analysis`、`economic-indicator-preview`、`reliable-source-search` は、依頼内容が該当する場合に使用します。

## 共通化の方針

- `SKILL.md` にはClaude・Codex固有のツール名をできるだけ書かず、「Web検索」「Webページを直接開いて本文を確認」のような共通表現を使います。
- Claude固有の呼び出し方は `/`、Codex固有の呼び出し方は `$` とし、明示起動するSkillでは両方を記載します。
- OpenAI／Codexだけで必要な設定は `agents/openai.yaml` に分離します。
- 口座情報はマネックス証券プラグインから取得し、取得できない項目を推測や一般Web検索で補完しません。
