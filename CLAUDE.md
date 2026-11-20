# モデルの使い分け

Fable は使わない。難しい判断だけ Opus 5.5 を高 effort（xhigh）で使う。

| 作業 | 担当 | モデル / effort |
|---|---|---|
| 検索・grep・ファイル探索 | `searcher` サブエージェント | haiku / low |
| レビュー | `reviewer` サブエージェント | haiku / medium |
| テスト・lint・ビルド | `checker` サブエージェント | haiku / low |
| 計画（plan モード） | メイン（opusplan） | opus / xhigh |
| 実装 | メイン（opusplan の実行時） | sonnet / medium |
| 難しい判断 | `decision-maker` サブエージェント | opus / xhigh |

## decision-maker を呼ぶ条件

- 実装方針の候補が2つ以上あり、どれを選ぶか決まらない
- 同じ不具合を2回修正しても解決しない
- スキーマ、公開API、データ移行など取り消しにくい変更の直前
- 性能・セキュリティ・保守性のトレードオフを伴う設計

上記に当たらない作業では decision-maker を呼ばない。
