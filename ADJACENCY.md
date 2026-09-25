# 隣接関係 — huhito と hiedanoare

> **huhito は「身元と所在」を保証する。**
> **hiedanoare は「記録と編纂」を保証する。**
> 二人は同一の対象（生成物・エージェント）を異なる側面から見守る。

## 位相（Topology）

```text
生成物（repo, skill, agent, deploy...）
        │
        ├── huhito  ──→  名札・台帳・居所（WHERE / WHO）
        │                    ↓
        │               koseki.ledger.jsonl
        │                    ↑
        └── hiedanoare ──→  記録・日誌・気づき（WHAT / WHEN / WHY）
                             ↓
                        llm-wiki / errors.db
```

| 軸 | huhito | hiedanoare |
|---|---|---|
| **対象** | 生成物の身分証・住所 | 生成物の行動・変化の記録 |
| **問い** | 「これは何者で、今どこにいるか」 | 「これはいつ、何を、なぜ行ったか」 |
| **出力** | `id.koseki.json` + `ledger` | `recap` / `journal` / `insight` / `errors.db` |
| **時間感覚** | 状態のスナップショット | 時系列のストーリー |
| **失敗時** | 所在不明・幽霊登録 | 記録漏れ・文脈喪失 |

## 境界での相互作用

### 1. 出生（CREATE → REGISTER → LOG）

新しい repo が生成されたとき：

1. **huhito** が `git remote` と `ll` を照合し、名札を発行・台帳に登録
2. **hiedanoare** が `log` エントリを作成：「X が生まれた（ huhito 登録 #v123 ）」

### 2. 引っ越し（MOVE → UPDATE → JOURNAL）

clone 場所が変わったとき：

1. **huhito** が `moved_from` を更新し、ledger の `path` を修正
2. **hiedanoare** が `journal` に記録：「X の居住場所が A → B に変更（ huhito 追跡 ）」

### 3. 不整合検出（MISMATCH → ALERT → INSIGHT）

`git remote` と台帙が食い違ったとき：

1. **huhito** が `dirty` フラグを立て、issue / alert を発行
2. **hiedanoare** が `insight` を作成：「所在追跡で不整合発見。原因調査の記録。」

### 4. 消滅（DELETE → ARCHIVE → MEMORIAL）

repo が削除されたとき：

1. **huhito** が status を `archived` に更新
2. **hiedanoare** が `recap` を作成：「X の活動を総括し、除籍の理由を記録」

## 連携フロー

```textn[huhito] 検出イベント ──┬── 名札・台帳更新
                         │
                         └── hiedanoare へ通知 ──→ [hiedanoare] 記録
                                   ↓
                             「huhito-event: <type> <id> <details>」
                                   ↓
                          llm-wiki ingest / errors-ledger add
```

## 禁止領域

| huhito がやらないこと | hiedanoare がやらないこと |
|---|---|
| 日誌・recap の作成・編纂 | 名札の書き換え・ID の付与 |
| llm-wiki の query / ingest | ファイル移動・rename の実行 |
| エラーの解決・修正 | 台帳の勝手な更新 |

## 結論

**huhito は戸籍係。hiedanoare は記録係。**
戸籍係が「誰がどこにいるか」を正しく保てば、記録係は「誰が何をしたか」を正しく綴れる。
逆に、記録係が活動の痕跡を残せば、戸籍係は名無しの生成物を「あの日の記録」から逆引きして身元を明かすことができる。

二人は隣接し、互いの空白を埋め合う。
